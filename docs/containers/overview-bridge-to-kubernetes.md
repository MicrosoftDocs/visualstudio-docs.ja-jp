---
title: Bridge to Kubernetes のしくみ
ms.technology: vs-azure
ms.date: 11/19/2020
ms.topic: conceptual
description: Bridge to Kubernetes を使用して開発用コンピューターを Kubernetes クラスターに接続するプロセスについて説明します
keywords: Bridge to Kubernetes, Docker, Kubernetes, Azure, コンテナー
monikerRange: '>=vs-2019'
manager: jmartens
author: ghogen
ms.author: ghogen
ms.openlocfilehash: 838589e0dd81232de25b88989d621a07fb22f972
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2021
ms.locfileid: "112043056"
---
# <a name="how-bridge-to-kubernetes-works"></a>Bridge to Kubernetes のしくみ

Bridge to Kubernetes を使用すると、開発用のコンピューター上でコードの実行とデバッグを行いながら、残りのアプリケーションやサービスが置かれている Kubernetes クラスターとの接続を保つことができます。 たとえば、多数のサービスやデータベースが相互に依存している大規模なマイクロサービス アーキテクチャがある場合、開発用コンピューター上のそれらの依存関係をレプリケートするのは困難な場合があります。 さらに、内部ループの開発中にコードを変更するたびにコードをビルドして Kubernetes クラスターにデプロイすると、遅くなり、時間がかかり、デバッガーで使用するのが難しくなることがあります。

Bridge to Kubernetes を使用すると、代わりに開発用コンピューターとクラスターの間に直接接続が作成されることにより、コードをビルドしてクラスターにデプロイする必要がなくなります。 デバッグ中に開発用コンピューターをクラスターに接続すると、Docker または Kubernetes の構成を作成することなく、完全なアプリケーションのコンテキストで、サービスを迅速にテストおよび開発できます。

Bridge to Kubernetes では、接続された Kubernetes クラスターと開発用コンピューターの間でトラフィックがリダイレクトされます。 このトラフィックのリダイレクトにより、開発用コンピューター上のコードと、Kubernetes クラスターで実行されているサービスは、同じ Kubernetes クラスター内に存在するかのように通信できます。 Bridge to Kubernetes には、開発用コンピューターの Kubernetes クラスター内のポッドに利用できる環境変数とマウントされたボリュームをレプリケートする方法も用意されています。 開発用コンピューター上の環境変数およびマウントされたボリュームにアクセスできると、それらの依存関係を手動でレプリケートすることなく、コードの作業をすばやく行うことができます。

> [!WARNING]
> Bridge to Kubernetes は、開発およびテストのシナリオでのみ使用することを目的としています。 アクティブに使用されている運用クラスターまたはライブ サービスでの使用は意図されておらず、サポートされていません。

現在サポートされている機能と、Bridge to Kubernetes の今後のロードマップに関する情報は、[Bridge to Kubernetes のロードマップ](https://github.com/microsoft/mindaro/projects/1)を参照してください。

## <a name="using-bridge-to-kubernetes"></a>Bridge to Kubernetes の使用

Visual Studio で Bridge to Kubernetes を使用するには、*ASP.NET と Web 開発* ワークロードと [Bridge to Kubernetes 拡張機能][btk-extension]がインストールされている Windows 10 で実行されている [Visual Studio 2019][visual-studio] バージョン 16.7 Preview 4 以降が必要です。 Bridge to Kubernetes を使用して Kubernetes クラスターへの接続を確立するときに、クラスター内の既存のポッドとの間でやり取りされるすべてのトラフィックを開発用コンピューターにリダイレクトするかどうかを選択できます。

> [!NOTE]
> Bridge to Kubernetes を使用するときは、開発用コンピューターにリダイレクトするサービスの名前の指定を求められます。 このオプションを利用して、リダイレクト用のポッドを簡単に見分けることができます。 Kubernetes クラスターと開発用コンピューターの間のすべてのリダイレクトは、ポッドを対象としています。

クラスターへの接続が確立された Bridge to Kubernetes では、次のことが行われます。

* ユーザーは、クラスター上で置き換えるサービス、コードに使用する開発用コンピューター上のポート、1 回限りのアクションとしてのコードに対する起動タスクを構成するよう求められます。
* クラスター上のポッド内のコンテナーが、開発用コンピューターにトラフィックをリダイレクトするリモート エージェント コンテナーに置き換えられます。
* 開発用コンピューターからのトラフィックを、クラスター内で実行されるリモート エージェントに転送するために、開発用コンピューター上で [kubectl port-forward][kubectl-port-forward] を実行します。
* リモート エージェントを使用してクラスターから環境情報を収集します。 この環境情報には、環境変数、表示可能なサービス、ボリューム マウント、シークレット マウントが含まれます。
* 開発用コンピューター上のサービスが、クラスター上で実行されているかのように同じ変数にアクセスできるよう、Visual Studio の環境が設定されます。
* クラスター上のサービスが開発用コンピューター上のローカル IP アドレスにマップされるように、hosts ファイルが更新されます。 開発用コンピューター上で実行されているコードは、これらの hosts ファイルのエントリを通じて、クラスター内で実行されている別のサービスに要求を送信できるようになります。 Bridge to Kubernetes がクラスターに接続するときに、hosts ファイルを更新できるよう、開発用コンピューター上の管理者アクセス権が求められます。
* 開発用コンピューター上でコードの実行とデバッグが開始されます。 必要な場合は、Bridge to Kubernetes によって開発用コンピューターで必要なポートを現在使用しているサービスまたはプロセスが停止され、ポートが解放されます。

クラスターへの接続が確立された後、ユーザーは、コンテナー化を使用せずに、コンピューター上でネイティブにコードを実行してデバッグすることができ、コードではクラスターの残りの部分と直接対話できます。 リモート エージェントが受信するネットワーク トラフィックは、ネイティブに実行されているコードがそのトラフィックを受け入れて処理できるよう、接続時に指定されたローカル ポートにリダイレクトされます。 ご利用のクラスターにある環境変数、ボリューム、シークレットは、開発用コンピューター上で実行されているコードから利用できるようになります。 また、Bridge to Kubernetes によって開発用コンピューターに追加された hosts ファイルのエントリとポート転送により、コードでは、クラスター側のサービス名を使用して、クラスター上で実行されているサービスにネットワーク トラフィックを送信することができます。そのトラフィックは、クラスターで実行されているサービスに転送されます。 接続されている間は常に、開発用コンピューターとクラスターの間でトラフィックがルーティングされます。

さらに、Bridge to Kubernetes には、`KubernetesLocalProcessConfig.yaml` ファイルを介して、開発コンピューター上のクラスター内のポッドで使用できる環境変数とマウントされたファイルをレプリケートする方法が用意されています。 このファイルを使用して、新しい環境変数やボリューム マウントを作成することもできます。

> [!NOTE]
> クラスターへの接続が行われている間 (それに加えて 15 分間)、Bridge to Kubernetes により、ローカル コンピューター上で管理者権限を使用して *EndpointManager* という名前のプロセスが実行されます。

> [!NOTE]
> 複数のサービスを使用して並列デバッグできますが、デバッグするサービスと同じ数の Visual Studio インスタンスを起動する必要があります。 サービスが異なるポート上でローカル待機するようにし、別々に構成し、デバッグします。 このシナリオでは、分離はサポートされていません。

## <a name="additional-configuration-with-kuberneteslocalprocessconfigyaml"></a>KubernetesLocalProcessConfig.yaml を使用した追加の構成

`KubernetesLocalProcessConfig.yaml` ファイルを使用すると、クラスター内のポッドからアクセスできる環境変数とマウントされたファイルをレプリケートすることができます。 Bridge to Kubernetes の開発に Visual Studio を使用する場合は、KubernetesLocalConfig.yaml ファイルが、リダイレクトするサービスのプロジェクト ファイルと同じディレクトリに配置されている必要があります。 追加の構成オプションの詳細については、「[Bridge to Kubernetes を構成する][using-config-yaml]」を参照してください。

## <a name="using-routing-capabilities-for-developing-in-isolation"></a>分離して開発するためのルーティング機能の使用

既定では、Bridge to Kubernetes によって 1 つのサービスのすべてのトラフィックが開発用コンピューターにリダイレクトされます。 また、ルーティング機能を使用して、サブドメインから開発用コンピューターに提供されるサービスにのみ、要求をリダイレクトするオプションもあります。 これらのルーティング機能により、Bridge to Kubernetes を使用して分離して開発し、クラスター内の他のトラフィックの中断を回避することができます。

次のアニメーションは、同じクラスターで作業している 2 人の開発者を示しています。

![分離を示すアニメーション GIF](media/bridge-to-kubernetes/btk-graphic-isolated.gif)

分離した作業を有効にすると、Bridge to Kubernetes では、Kubernetes クラスターへの接続だけでなく、次のことが行われます。

* Kubernetes クラスターで Azure Dev Spaces が有効になっていないことを確認します。
* 選択したサービスを同じ名前空間内のクラスターにレプリケートし、*routing.visualstudio.io/route-from=SERVICE_NAME* ラベルと *routing.visualstudio.io/route-on-header=kubernetes-route-as:GENERATED_NAME* 注釈を追加します。
* Kubernetes クラスター上の同じ名前空間でルーティング マネージャーを構成し、開始します。 ルーティング マネージャーによって、名前空間でルーティングを構成するときに、ラベル セレクターを使用して *routing.visualstudio.io/route-from=SERVICE_NAME* ラベルと *routing.visualstudio.io/route-on-header=kubernetes-route-as:GENERATED_NAME* 注釈が検索されます。

Bridge to Kubernetes によって、Kubernetes クラスター上で Azure Dev Spaces が有効になっていることが検出されると、Bridge to Kubernetes を使用する前に Azure Dev Spaces を無効にするように求められます。

ルーティング マネージャーによって、起動時に次のことが行われます。

* サブドメインの *GENERATED_NAME* を使用し、名前空間に含まれるすべてのイングレス (ロード バランサー イングレスを含む) を複製します。
* 各サービス用に、*GENERATED_NAME* サブドメインで複製されたイングレスに関連付けられたエンボイ ポッドを作成します。
* 分離して作業しているサービス用の追加のエンボイ ポッドを作成します。 これで、サブドメインを指定した要求を開発用コンピューターにルーティングすることができます。
* サブドメインを持つサービスのルーティングを処理するために、各エンボイ ポッド用のルーティング規則を構成します。

次の図は、Bridge to Kubernetes がクラスターに接続する前の Kubernetes クラスターを示しています。

![Bridge to Kubernetes なしのクラスターの図](media/bridge-to-kubernetes/kubr-cluster.svg)

次の図は、分離モードで Bridge to Kubernetes が有効な同じクラスターを示しています。 重複したサービスと、分離によるルーティングをサポートするエンボイ ポッドを確認できます。

![Bridge to Kubernetes が有効なクラスターの図](media/bridge-to-kubernetes/kubr-cluster-devcomputer.svg)

*GENERATED_NAME* サブドメインが指定された要求がクラスターで受信されると、要求に *kubernetes-route-as=GENERATED_NAME* ヘッダーが追加されます。 エンボイ ポッドによって、クラスター内の適切なサービスへの要求のルーティングが処理されます。 分離して作業されているサービスに要求がルーティングされると、その要求はリモート エージェントによって開発用コンピューターにリダイレクトされます。

*GENERATED_NAME* サブドメインが指定されていない要求がクラスターで受信されると、要求にヘッダーが追加されません。 エンボイ ポッドによって、クラスター内の適切なサービスへの要求のルーティングが処理されます。 置き換えられるサービスに要求がルーティングされる場合、その要求はリモート エージェントではなく元のサービスにルーティングされます。

> [!IMPORTANT]
> クラスター上の各サービスでは、追加の要求を行うときに *kubernetes-route-as=GENERATED_NAME* ヘッダーを転送する必要があります。 たとえば、*serviceA* で要求が受信されると、*serviceB* に要求が行われてから応答が返されます。 この例では、*serviceA* から要求の *kubernetes-route-as=GENERATED_NAME* ヘッダーが *serviceB* に転送される必要があります。 [ASP.NET][asp-net-header] などの一部の言語には、ヘッダーの伝達を処理するメソッドが用意されている場合があります。

クラスターから切断すると、既定では、Bridge to Kubernetes によってすべてのエンボイ ポッドおよび重複しているサービスが削除されます。

> [!NOTE]
> ルーティング マネージャーの展開とサービスは、名前空間で実行されたままになります。 展開とサービスを削除するには、名前空間に対して次のコマンドを実行します。
>
> ```azurecli
> kubectl delete deployment routingmanager-deployment -n NAMESPACE
> kubectl delete service routingmanager-service -n NAMESPACE
> ```

## <a name="diagnostics-and-logging"></a>診断とログ記録

Bridge to Kubernetes を使用してクラスターに接続しているときは、クラスターからの診断ログが、開発用コンピューターの *TEMP* ディレクトリの *Bridge to Kubernetes* フォルダーに記録されます。

## <a name="rbac-authorization"></a>RBAC 承認

Kubernetes には、ユーザーとグループのアクセス許可を管理するためのロールベースのアクセス制御 (RBAC) が用意されています。 詳細については、[Kubernetes のドキュメント](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)を参照してください。RBAC 対応クラスターのアクセス許可を設定するには、YAML ファイルを作成し、`kubectl` を使用してクラスターに適用します。 

クラスターでアクセス許可を設定するには、次のような *permissions.yml* などの YAML ファイルを作成または変更します。`<namespace>` には独自の名前空間を使用し、アクセスが必要なサブジェクト (ユーザーおよびグループ) を使用します。

```yml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: bridgetokubernetes-<namespace>
  namespace: development
subjects:
  - kind: User
    name: jane.w6wn8.k8s.ginger.eu-central-1.aws.gigantic.io
    apiGroup: rbac.authorization.k8s.io
  - kind: Group
    name: dev-admin
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: admin
  apiGroup: rbac.authorization.k8s.io
```

次のコマンドを使用してアクセス許可を適用します。

```cmd
kubectl -n <namespace> apply -f <yaml file name>
```

## <a name="limitations"></a>制限事項

Bridge to Kubernetes には次の制限があります。

* Bridge to Kubernetes を正常に接続するために、1 つのポッドには、そのポッドで実行されているコンテナーが 1 つだけ与えられます。
* 現時点では、Bridge to Kubernetes ポッドは、Linux コンテナーである必要があります。 Windows コンテナーはサポートされていません。
* ホスト ファイルを編集する目的で開発コンピューターで実行するには、管理者特権が Bridge to Kubernetes に必要になります。
* Azure Dev Spaces が有効なクラスターでは、Bridge to Kubernetes を使用できません。

### <a name="bridge-to-kubernetes-and-clusters-with-azure-dev-spaces-enabled"></a>Azure Dev Spaces が有効な Bridge to Kubernetes とクラスター

Azure Dev Spaces が有効なクラスターでは、Bridge to Kubernetes を使用できません。 Azure Dev Spaces が有効なクラスターで Bridge to Kubernetes を使用する場合は、クラスターに接続する前に Azure Dev Spaces を無効にする必要があります。

## <a name="next-steps"></a>次のステップ

Bridge to Kubernetes を使用してローカル環境の開発用コンピューターをクラスターに接続する方法については、「[Bridge to Kubernetes を使用する](bridge-to-kubernetes.md)」を参照してください。

[asp-net-header]: https://www.nuget.org/packages/Microsoft.AspNetCore.HeaderPropagation/
[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-latest&preserve-view=true
[bridge-to-kubernetes-vs]: bridge-to-kubernetes.md
[kubectl-port-forward]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
[visual-studio]: https://visualstudio.microsoft.com/downloads/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[using-config-yaml]: configure-bridge-to-kubernetes.md
