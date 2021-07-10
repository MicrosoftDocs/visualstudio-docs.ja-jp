---
title: 'チュートリアル: 開発マシンを Bridge to Kubernetes と接続する'
ms.technology: vs-azure
ms.date: 03/24/2021
ms.topic: tutorial
description: Visual Studio で Bridge to Kubernetes を使用してお使いの開発用コンピューターを Kubernetes クラスターに接続します。
keywords: Bridge to Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, コンテナー
monikerRange: '>=vs-2019'
ms.author: ghogen
author: ghogen
manager: jmartens
ms.openlocfilehash: b8d6c98d2e2146ad57871b74cd2d522ed2b04259
ms.sourcegitcommit: 0499d813d5c24052c970ca15373d556a69507250
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "113046119"
---
# <a name="tutorial-use-bridge-to-kubernetes-to-connect-your-clusters-and-your-development-computers"></a>チュートリアル: Bridge to Kubernetes を使用してお使いのクラスターとお使いの開発用コンピューターを接続する

このチュートリアルでは、Bridge to Kubernetes を使用して、お使いの Kubernetes クラスターと、お使いの開発用コンピューターで実行されているコードの間で、トラフィックをリダイレクトする方法を説明します。 

また、このガイドでは、Kubernetes クラスター上の複数のマイクロサービスを含む大規模なサンプル アプリケーションをデプロイするためのスクリプトも提供します。

Bridge to Kubernetes の詳細については、「[Bridge to Kubernetes のしくみ](overview-bridge-to-kubernetes.md)」の記事を参照してください。

## <a name="prerequisites"></a>前提条件

- Kubernetes クラスター
- Windows 10 上で実行されている [Visual Studio 2019][visual-studio] バージョン 16.7 Preview 4 以降。
- [Bridge to Kubernetes 拡張機能がインストールされていること][btk-extension]

## <a name="about-the-data"></a>データについて

このチュートリアルでは、Bridge to Kubernetes を使用して、任意の Kubernetes クラスターに簡単な TODO サンプル アプリケーションのマイクロサービス バージョンを開発します。 Visual Studio を使用する、この [TODO アプリのサンプル アプリケーション][todo-app-github]は、[TodoMVC](http://todomvc.com) が提供しているコードから採用しています。 

 これらの手順は、どの Kubernetes クラスターでも使用できます。 したがって、Kubernetes クラスター上で実行されている自分独自のアプリケーションが既にある場合でも、以下の手順に従い、自分独自のサービスの名前を使用できます。

この TODO アプリケーションのサンプルは、永続ストレージを提供するフロントエンドとバックエンドで構成されています。 この拡張サンプルでは、統計コンポーネントを追加し、特に次のいくつかのマイクロサービスにアプリケーションを分割しています。

- フロントエンドで database-api を呼び出し、TODO 項目を永続化および更新する。
- database-api サービスでが Mongo データベースに依存し、TODO 項目を永続化する。
- フロントエンドが RabbitMQ キューに、追加、完了および削除イベントを書き込む。
- 統計ワーカーが RabbitMQ キューからイベントを受け取り、Redis キャッシュを更新する。
- 統計 API が、フロントエンドが表示するキャッシュ済みの統計を公開する。

この拡張 TODO アプリケーションは、全体で相関する 6 つのコンポーネントで構成されています。


## <a name="check-the-cluster"></a>クラスターを確認する

コマンド プロンプトを開き、`kubectl` がインストールされていることを確認し、パスで使用するクラスターが使用可能で準備ができていることを確認して、そのクラスターにコンテキストを設定します。

```cmd
kubectl cluster-info
kubectl config use-context {context-name}
```

ここで {context-name} は、todo-app サンプルで使用するクラスターのコンテキスト名です。

## <a name="deploy-the-application"></a>アプリケーションの配置

[mindaro リポジトリ](https://github.com/Microsoft/mindaro)をクローンし、現在の作業フォルダーが *samples/todo-app* の状態でコマンド ウィンドウを開きます。

このサンプル用の名前空間を作成します。

```cmd
kubectl create namespace todo-app
```

次に、配置マニフェストを適用します。

```cmd
kubectl apply -n todo-app -f deployment.yaml
```

これは、`LoadBalancer` 型のサービスを使用してフロントエンドを公開する単純な展開です。 すべてのポッドが実行され、`frontend` サービスの外部 IP が使用可能になるまで待機します。

MiniKube を使用してテストする場合は、`minikube tunnel` を使用して外部 IP を解決する必要があります。 AKS または別のクラウドベースの Kubernetes プロバイダーを使用している場合は、外部 IP が自動的に割り当てられます。 次のコマンドを使用して `frontend` サービスを監視し、それが起動して実行されるまで待機します。

```output
kubectl get service -n todo-app frontend --watch

NAME       TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
frontend   LoadBalancer   10.0.245.78   20.73.226.228   80:31910/TCP   6m26s
```

外部 IP およびローカル ポート (PORT(S) 列の最初の数字) を使用してアプリケーションを参照します。

```
http://{external-ip}:{local-port}
```

ブラウザーで実行中のアプリをテストします。 todo 項目を追加、完了、削除すると、統計ページが期待されるメトリックで更新されることに着目してください。

## <a name="connect-to-your-cluster-and-debug-a-service"></a>クラスターに接続してサービスをデバッグする

Visual Studio で *samples\todo-app\database-api\database-api.csproj* を開きます。 次のように、プロジェクトで起動設定のドロップダウンから **[Bridge to Kubernetes]** を選択します。

![Bridge to Kubernetes を選択する](media/bridge-to-kubernetes/choose-bridge-to-kubernetes.png)

*[Bridge to Kubernetes]* の横にある開始ボタンをクリックします。 **[Create profile for Bridge to Kubernetes]\(Bridge to Kubernetes のプロファイルの作成\)** ダイアログで、次の手順を実行します。

- お使いのクラスターの名前を選択します。
- お使いの名前空間として *todo-app* を選択します。
- リダイレクトするサービスとして *database-api* を選択します。
- 以前自分のブラウザーの起動に使用したのと同じ URL (http://{external-ip}:{local-port}) を選択します。

![Bridge to Kubernetes クラスターを選択する](media/bridge-to-kubernetes/configure-bridge-debugging.png)

分離して実行するかどうかを選択します。つまり、変更しても、クラスターを使用している他のユーザーは影響を受けません。 影響を受ける各サービスのコピーに要求をルーティングし、他のすべてのトラフィックは通常どおりルーティングすることで、この分離モードは達成されます。 この実行方法の詳細については、「[Bridge to Kubernetes のしくみ][btk-overview-routing]」を参照してください。

**[OK]** をクリックします。 *database-api* サービスに対する Kubernetes クラスター内のすべてのトラフィックが、お使いの開発用コンピューターで実行されているお使いのアプリケーションのバージョンにリダイレクトされます。 Bridge to Kubernetes ではまた、アプリケーションからのすべての送信トラフィックが、Kubernetes クラスターにルーティングされます。

> [!NOTE]
> *EndpointManager* が管理者特権で実行して hosts ファイルを変更することを許可するように求められます。

`database-api` サービスに接続していることがステータス バーに表示されたら、開発用コンピューターに接続されています。

![接続された開発用コンピューター](media/bridge-to-kubernetes/development-computer-connected.png)

> [!NOTE]
> 以降の起動時には、 **[Create profile for Bridge to Kubernetes]\(Bridge to Kubernetes のプロファイルの作成\)** ダイアログは表示されません。 これらの設定は、プロジェクトのプロパティの **[デバッグ]** で更新します。

開発用コンピューターが接続されると、置き換えているサービスのトラフィックの、開発用コンピューターに対するリダイレクトが開始されます。

> [!NOTE]
> 別の Kubernetes サービスでテストするなど、後でデバッグ プロファイルを編集する場合は、 **[デバッグ]**  >  **[Debug Properties]\(デバッグのプロパティ\)** を選択し、 **[変更]** ボタンをクリックします。

## <a name="set-a-break-point"></a>ブレーク ポイントを設定する

MongoHelper.cs を開き、CreateTask メソッドの 68 行目の任意の場所をクリックして、そこに自分のカーソルを置きます。 *F9* キーを押すか、 **[デバッグ]**  >  **[ブレークポイントの設定/解除]** の順に選択してブレークポイントを設定します。

パブリック URL (フロントエンド サービスの外部 IP アドレス) を開き、サンプル アプリケーションに移動します。 サービスを再開するには、**F5** キーを押すか、 **[デバッグ]**  >  **[続行]** の順にクリックします。

ブレークポイントがある行に自分のカーソルを置き、**F9** キーを押して、ブレークポイントを削除します。

> [!NOTE]
> 既定では、デバッグ タスクを停止すると、開発用コンピューターも Kubernetes クラスターから切断されます。 この動作は、 **[ツール]**  >  **[オプション]** の **[Kubernetes Debugging Tools]\(Kubernetes デバッグ ツール\)** セクションで **[Disconnect after debugging]\(デバッグ後に切断する\)** を `false` に変更すると変更できます。 この設定を更新した後は、デバッグを停止して開始するとき、開発用コンピューターは接続されたままになります。 開発用コンピューターをクラスターから切断するには、ツール バーの **[切断]** ボタンをクリックします。
>
>![Kubernetes のデバッグ オプションのスクリーンショット](media/bridge-to-kubernetes/kubernetes-debugging-options.png)

## <a name="additional-configuration"></a>追加構成

Bridge to Kubernetes では、ルーティング トラフィックを処理し、追加の構成なしで環境変数をレプリケートできます。 ConfigMap ファイルなど、Kubernetes クラスターのコンテナーにマウントされているファイルをダウンロードする必要がある場合、`KubernetesLocalProcessConfig.yaml` を作成し、開発用コンピューターにそれらのファイルをダウンロードできます。 詳細については、[Bridge to Kubernetes 向けの追加の構成に KubernetesLocalProcessConfig.yaml を使用する][kubernetesLocalProcessConfig-yaml]方法に関するページを参照してください。

## <a name="using-logging-and-diagnostics"></a>ログ記録と診断の使用

診断ログは、開発用コンピューターの *TEMP* ディレクトリの `Bridge to Kubernetes` ディレクトリにあります。

## <a name="next-steps"></a>次のステップ

Bridge to Kubernetes のしくみについて説明します。

> [!div class="nextstepaction"]
> [Bridge to Kubernetes のしくみ](overview-bridge-to-kubernetes.md)

[todo-app-github]: https://github.com/Microsoft/mindaro
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[visual-studio]: https://www.visualstudio.com/vs/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[kubernetesLocalProcessConfig-yaml]: configure-bridge-to-kubernetes.md
[btk-overview-routing]: overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation
