---
title: ネットワーク ベース インストールを作成する
description: 企業内に Visual Studio を展開するためのネットワーク インストール ポイントを作成する方法について説明します。
ms.date: 08/06/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 4CABFD20-962E-482C-8A76-E4012052F701
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 1d18d3a3de423cc63569911bbe49477b5e6f5f26
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180297"
---
# <a name="create-a-network-installation-of-visual-studio"></a>Visual Studio のネットワーク インストールを作成する

通常、企業の管理者はクライアント ワークステーションに展開するためのネットワーク インストール ポイントを作成します。 Visual Studio は、初期インストールのファイルとすべての製品の更新プログラムが単一のファイルにキャッシュされるように設計されています。 (このプロセスは_レイアウトの作成_とも呼ばれています。)

これは、最新のサービスの更新プログラムに更新されていない場合でも、クライアント ワークステーションが同じネットワークの場所を使用してインストールを管理できるようにするためです。

 > [!NOTE]
 > 複数のエディションの Visual Studio を企業内で利用している場合 (たとえば、Visual Studio Professional と Visual Studio Enterprise の両方)、エディションごとに個別のネットワーク インストール共有を作成する必要があります。

## <a name="download-the-visual-studio-bootstrapper"></a>Visual Studio ブートストラップをダウンロードする

必要な Visual Studio のエディションをダウンロードします。 必ず **[保存]** をクリックし、 **[フォルダーを開く]** をクリックします。

セットアップ実行可能ファイル&mdash;具体的にはブートストラップ ファイル&mdash;は、次のいずれかになります。

::: moniker range="vs-2017"

|エディション | ダウンロード|
|-------------|-----------------------|
|Visual Studio Enterprise | [**vs_enterprise.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=15&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2017) |
|Visual Studio Professional | [**vs_professional.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=15&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2017) |

その他にサポートされているブートストラップとして、[vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe)、[vs_feedbackclient.exe](https://aka.ms/vs/15/release/vs_feedbackclient.exe)、[vs_teamexplorer.exe](https://aka.ms/vs/15/release/vs_teamexplorer.exe)、[vs_testagent.exe](https://aka.ms/vs/15/release/vs_testagent.exe)、[vs_testcontroller.exe](https://aka.ms/vs/15/release/vs_testcontroller.exe)、[vs_testprofessional.exe](https://aka.ms/vs/15/release/vs_testprofessional.exe) が含まれます。

::: moniker-end

::: moniker range="vs-2019"

|エディション | ダウンロード|
|-------------|-----------------------|
|Visual Studio Enterprise | [**vs_enterprise.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
|Visual Studio Professional | [**vs_professional.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |

他にサポートされているブートストラップには、[vs_buildtools.exe](https://aka.ms/vs/16/release/vs_buildtools.exe)、[vs_teamexplorer.exe](https://aka.ms/vs/16/release/vs_teamexplorer.exe)、[vs_testagent.exe](https://aka.ms/vs/16/release/vs_testagent.exe)、[vs_testcontroller.exe](https://aka.ms/vs/16/release/vs_testcontroller.exe) があります。

::: moniker-end

## <a name="create-an-offline-installation-folder"></a>オフライン インストール フォルダーを作成する

このステップを実行するにはインターネット接続が必要です。 すべての言語およびすべての機能を持つオフライン インストールを作成するには、次の例のいずれかのコマンドを使用します。

   > [!IMPORTANT]
   > Visual Studio の完全なレイアウトには、少なくとも 35 GB のディスク領域が必要で、ある程度ダウンロードに時間がかかります。 インストールするコンポーネントのみでレイアウトを作成する方法の詳細については、「[ネットワーク レイアウトをカスタマイズする](#customize-the-network-layout)」セクションをご覧ください。
   >
   > [!TIP]
   > コマンドをダウンロード ディレクトリから実行していることを確認してください。 通常は、Windows 10 を実行するコンピューター上の `C:\Users\<username>\Downloads` です。

- Visual Studio Enterprise の場合、以下を実行します。

  ```vs_enterprise.exe --layout c:\vsoffline```

- Visual Studio Professional の場合、以下を実行します。

  ```vs_professional.exe --layout c:\vsoffline```

## <a name="modify-the-responsejson-file"></a>response.json file を変更する

response.json を変更し、セットアップの実行時に使用される既定値を設定できます。  たとえば、特定のワークロード セットが自動的に選択されるように `response.json` ファイルを構成できます。
詳細については、「[Automate Visual Studio installation with a response file](automated-installation-with-response-file.md)」 (応答ファイルで Visual Studio インストールを自動化する) を参照してください。

## <a name="copy-the-layout-to-a-network-share"></a>ネットワーク共有にレイアウトをコピーする

他のコンピューターから実行できるようにネットワーク共有でレイアウトをホストします。

次の例では、[xcopy](/windows-server/administration/windows-commands/xcopy/) を使用します。 必要に応じて、[robocopy](/windows-server/administration/windows-commands/robocopy/) を使用することもできます。  

::: moniker range="vs-2017"

例:

```cmd
xcopy /e c:\vsoffline \\server\products\VS2017
```

::: moniker-end

::: moniker range="vs-2019"

```cmd
xcopy /e c:\vsoffline \\server\products\VS2019
```

::: moniker-end

> [!IMPORTANT]
> エラーを防ぐには、レイアウト パス全体が 80 文字未満であることを確認してください。

## <a name="customize-the-network-layout"></a>ネットワーク レイアウトをカスタマイズする

ネットワーク レイアウトはいくつかの方法でカスタマイズできます。 [言語ロケール](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)、[ワークロード、コンポーネント、推奨の依存関係または任意の依存関係](workload-and-component-ids.md)からなる特定のセットのみを含む部分的レイアウトを作成できます。 これは、一部のワークロードだけをクライアント ワークステーションに展開することがわかっている場合に便利です。 レイアウトをカスタマイズするための一般的なコマンド ライン パラメーターには次のようなものがあります。

* `--add` は[ワークロードまたはコンポーネント ID](workload-and-component-ids.md) を指定します。 <br>`--add` を使用すると、`--add` で指定されたワークロードとコンポーネントだけがダウンロードされます。  `--add` を使用しない場合、すべてのワークロードとコンポーネントがダウンロードされます。
* `--includeRecommended` は指定したワークロード ID のすべての推奨コンポーネントを含めます。
* `--includeOptional` は指定したワークロード ID のすべての推奨コンポーネントと任意コンポーネントを含めます。
* `--lang` は[言語ロケール](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)を指定します。

次に、レイアウトを部分的にカスタマイズする例をいくつか紹介します。

* 1 つの言語に対して、すべてのワークロードとコンポーネントをダウンロードするには、以下を実行します。

    ```cmd
    vs_enterprise.exe --layout C:\vsoffline --lang en-US
    ```

* 複数の言語に対して、すべてのワークロードとコンポーネントをダウンロードするには、以下を実行します。

    ```cmd
    vs_enterprise.exe --layout C:\vsoffline --lang en-US de-DE ja-JP
    ```

* すべての言語に対して、1 つのワークロードをダウンロードするには、以下を実行します。

    ```cmd
    vs_enterprise.exe --layout C:\vsoffline --add Microsoft.VisualStudio.Workload.Azure --includeRecommended
    ```

* 3 つの言語に対して、2 つのワークロードと 1 つのオプション コンポーネントをダウンロードするには、以下を実行します。

    ```cmd
    vs_enterprise.exe --layout C:\vsoffline --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended --lang en-US de-DE ja-JP
    ```

* 2 つのワークロードとその推奨コンポーネントのすべてをダウンロードするには:

    ```cmd
    vs_enterprise.exe --layout C:\vsoffline --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended
    ```

* 2 つのワークロードとそのすべての推奨コンポーネントと任意コンポーネントをダウンロードするには、次を実行します。

    ```cmd
    vs_enterprise.exe --layout C:\vsoffline --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeOptional
    ```

::: moniker range="vs-2017"

### <a name="new-in-version-153"></a>バージョン 15.3 での新機能

::: moniker-end

::: moniker range="vs-2019"

### <a name="save-your-layout-options"></a>レイアウト オプションの保存

::: moniker-end

レイアウト コマンドを実行すると、(ワークロードや言語などの) 指定したオプションが保存されます。 後続のレイアウトコマンドには、それ以前のすべてのオプションが含まれます。  英語のみ対象の 1 つのワークロードを含むレイアウトの例を示します。

```cmd
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
```

レイアウトを新しいバージョンに更新したい場合、追加のコマンド ライン パラメーターを指定する必要はありません。 このレイアウト フォルダーに保存されている以前の設定が、後続のすべてのレイアウト コマンドで使用されます。  次のコマンドは、既存の部分的レイアウトを更新します。

```cmd
vs_enterprise.exe --layout c:\VSLayout
```

追加のワークロードを追加したい場合は、次のようなコマンドを使用します。 この場合、Azure のワークロードとローカライズされた言語を追加します。  これで、Managed Desktop と Azure の両方がこのレイアウトに含まれるようになります。  これらのすべてのワークロードに、英語とドイツ語の言語リソースが含まれています。 レイアウトは利用可能な最新バージョンに更新されます。

```cmd
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
```

既存のレイアウトを完全なレイアウトに更新したい場合は、次の例に示すように all オプションを使用します。

```cmd
vs_enterprise.exe --layout c:\VSLayout --all
```

## <a name="deploy-from-a-network-installation"></a>ネットワーク インストールから展開する

管理者はインストール スクリプトの一部として Visual Studio をクライアント ワークステーションに展開することができます。 あるいは、管理者権限を持つユーザーは共有から直接セットアップを実行し、自分のコンピューターに Visual Studio をインストールできます。

* ユーザーは次のコマンドを実行してインストールできます。 <br>

    ```cmd
    \\server\products\VS\vs_enterprise.exe
    ```

* 管理者は次のコマンドを実行することで、無人モードでインストールできます。

    ```cmd
    \server\products\VS\vs_enterprise.exe --quiet --wait --norestart
    ```

> [!IMPORTANT]
> エラーを防ぐには、レイアウト パス全体が 80 文字未満であることを確認してください。
>
> [!TIP]
> バッチ ファイルの一部として実行するとき、`--wait` オプションを利用すると、`vs_enterprise.exe` プロセスはインストールの完了を待ち、それから終了コードを返します。
>
> これは、企業の管理者が完了したインストールに追加のアクション (たとえば、[成功したインストールにプロダクト キーを適用する](automatically-apply-product-keys-when-deploying-visual-studio.md)など) を実行したい場合に便利ですが、そのインストールからのリターン コードを処理するにはインストールが終了するまで待つ必要があります。
>
> `--wait` を使用しない場合、インストールが完了する前に `vs_enterprise.exe` プロセスが終了し、インストール操作の状態を表していない不正確な終了コードが返されます。

レイアウトからインストールする場合、インストールされる内容はレイアウトから取得されます。 ただし、レイアウトに含まれないコンポーネントを選択した場合は、インターネットから取得されます。  Visual Studio のセットアップでレイアウトにない内容がダウンロードされないようにするには、`--noWeb` オプションを使用します。 `--noWeb` が使用されていて、インストール対象として選択されている内容がレイアウトにない場合、セットアップは失敗します。

> [!IMPORTANT]
> `--noWeb` オプションを使っても、Visual Studio のセットアップで更新プログラムのチェックが行われなくなることはありません。 詳細については、「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」ページをご覧ください。

### <a name="error-codes"></a>エラー コード

`--wait` パラメーターを使用した場合、操作の結果に応じて、`%ERRORLEVEL%` 環境変数は次のいずれかの値に設定されます。

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

## <a name="update-a-network-install-layout"></a>ネットワーク インストール レイアウトを更新する

製品の更新プログラムが利用できるようになったら、[ネットワーク インストール レイアウトを更新し](update-a-network-installation-of-visual-studio.md)、更新されたパッケージを組み込むことが推奨されます。

## <a name="how-to-create-a-layout-for-a-previous-visual-studio-release"></a>以前の Visual Studio リリースのレイアウトを作成する方法

::: moniker range="vs-2017"

> [!NOTE]
> [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) で入手可能な Visual Studio ブートストラップを使用すると、それを実行したときに利用できる最新の Visual Studio リリースをダウンロードしてインストールできます。
>
> そのため、Visual Studio *ブートストラップ*を今日ダウンロードし、今日から 6 か月後に実行すると、そのブートストラップの実行時点での最新の Visual Studio リリースがインストールされます。
>
> しかし、*レイアウト*を作成し、そのレイアウトからインストールする場合、レイアウト内に存在する特定のバージョンの Visual Studio がインストールされます。 新しいバージョンがオンラインに存在するとしても、レイアウトに存在するバージョンの Visual Studio が取得されます。

::: moniker-end

::: moniker range="vs-2019"

> [!NOTE]
> [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads) で入手可能な Visual Studio ブートストラップを使用すると、それを実行したときに利用できる最新の Visual Studio リリースをダウンロードしてインストールできます。
>
> そのため、Visual Studio *ブートストラップ*を今日ダウンロードし、今日から 6 か月後に実行すると、そのブートストラップの実行時点での最新の Visual Studio リリースがインストールされます。
>
> しかし、*レイアウト*を作成し、そのレイアウトからインストールする場合、レイアウト内に存在する特定のバージョンの Visual Studio がインストールされます。 新しいバージョンがオンラインに存在するとしても、レイアウトに存在するバージョンの Visual Studio が取得されます。

::: moniker-end

旧バージョンの Visual Studio のレイアウトを作成する必要がある場合は、[https://my.visualstudio.com](https://my.visualstudio.com) に進み、Visual Studio ブートストラップの "固定" バージョンをダウンロードできます。

### <a name="how-to-get-support-for-your-offline-installer"></a>オフライン インストーラーのサポートを受ける方法

オフライン インストールに問題が発生した場合は、マイクロソフトにお知らせください。 問題報告の最善の方法として、[[問題を報告する]](../ide/how-to-report-a-problem-with-visual-studio.md) ツールを使用できます。 このツールでは、テレメトリとログを送信できます。これを、マイクロソフトは問題の診断と解決に役立てます。

インストール関連の問題については、[**ライブ チャット**](https://visualstudio.microsoft.com/vs/support/#talktous) (英語のみ) のサポート オプションも用意されています。

他にも利用可能なサポート オプションがあります。 一覧については、[フィードバック](../ide/feedback-options.md)に関するページをご覧ください。

## <a name="see-also"></a>関連項目

- [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
- [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
- [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
- [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)
- [サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)
- [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
- [Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)
