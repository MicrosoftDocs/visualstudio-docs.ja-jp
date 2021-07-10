---
title: ネットワーク ベース インストールを作成する
description: 企業内に Visual Studio を展開するためのネットワーク インストール ポイントを作成する方法について説明します。
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 4CABFD20-962E-482C-8A76-E4012052F701
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 080c4450cfcdca28386811865229af75303beb6a
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307532"
---
# <a name="create-a-network-installation-of-visual-studio"></a>Visual Studio のネットワーク インストールを作成する

エンタープライズ管理者は、クライアントワーク ステーションに展開できる Visual Studio ファイルを含むネットワーク インストール ポイントの作成が必要になる場合があります。 これは、クライアント コンピューターのアクセス許可が制限されている場合や、インターネットへのアクセスが制限されている場合や、組織が特定のバージョンの開発者ツールセットを標準化する前に、内部チームが互換性テストを行う必要がある場合に役立ちます。 Visual Studio は、管理者が "_ネットワーク レイアウトを作成_" できるように設計されました。基本的に、初期インストールと今後のすべての製品の更新プログラムの両方について、すべての Visual Studio ファイルを含む内部静的ネットワーク共有上にファイル キャッシュが作成されます。

 > [!NOTE]
 >  - 複数のエディションの Visual Studio を企業内で利用している場合 (たとえば、Visual Studio 2019 と Visual Studio 2019 Enterprise の両方)、エディションごとに個別のネットワーク インストール共有を作成する必要があります。
 >  - 最初のクライアントをインストールする "_前に_"、クライアントがどのように製品の更新プログラムを受信するかを決定することをお勧めします。  これにより、構成オプションが簡単に正しく設定されるようになります。 クライアントが更新プログラムを入手する場所としては、ネットワーク レイアウトの場所、またはインターネットを選択することができます。 
 >  - 修復とアンインストールの機能が正しく動作するには、元の Visual Studio のインストール レイアウトとそれ以降のすべての製品の更新プログラムが同じネットワーク ディレクトリに配置されている必要があります。

## <a name="download-the-visual-studio-bootstrapper"></a>Visual Studio ブートストラップをダウンロードする

必要な Visual Studio のエディションのブートストラップ ファイルをダウンロードします。 必ず **[保存]** を選択し、 **[フォルダーを開く]** を選択します。

::: moniker range="vs-2017"

Visual Studio 2017 バージョン 15.9 の最新のブートストラップを入手するには、[Visual Studio の以前のバージョン](https://visualstudio.microsoft.com/vs/older-downloads/)のページに移動し、次のいずれかのブートストラップ ファイルをダウンロードします。

| エディション                                      | ファイル名            |
|----------------------------------------------|---------------------|
| Visual Studio 2017 Enterprise バージョン 15.9   | vs_enterprise.exe   |
| Visual Studio 2017 Professional バージョン 15.9 | vs_professional.exe |
| Visual Studio 2017 Build Tools バージョン 15.9  | vs_buildtools.exe   |

その他にサポートされているブートストラップとして、vs_feedbackclient.exe、vs_teamexplorer.exe、vs_testagent.exe、vs_testcontroller.exe、vs_testprofessional.exe があります。

::: moniker-end

::: moniker range="vs-2019"

まずは、Visual Studio 2019 のブートストラップを、[Visual Studio のダウンロード ページ](https://visualstudio.microsoft.com/downloads)または、「[Visual Studio 2019 リリース](/visualstudio/releases/2019/history#installing-an-earlier-release)」ページから自分で選択した Visual Studio のバージョンおよびエディション用にダウンロードします。  セットアップ実行可能ファイル、より具体的にはブートストラップ ファイルは、次のいずれかと一致するか、またはそれに似たものとなります。

| エディション                    | ダウンロード                                                                                                                                                                                                                           |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Studio Enterprise   | [vs_enterprise.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019)     |
| Visual Studio Professional | [vs_professional.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
| Visual Studio Build Tools  | [vs_buildtools.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)     |

その他にサポートされているブートストラップして、[vs_teamexplorer.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/4026077127d25d33789f3882998266946608d8ada378b6ed7c8fff8c07f3dde2/vs_TeamExplorer.exe)、[vs_testagent.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/1383bf8bcda3d0e986a2e42c14114aaea8a7b085d31aa0623c9f70b2bad130e4/vs_TestAgent.exe)、[vs_testcontroller.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/54dcf24b76e7cd9fb8be0ac518a9dfba6daf18fe9b2aa1543411b1cda8820918/vs_TestController.exe) があります。

::: moniker-end

::: moniker range=">=vs-2022"

>![!TIP]
> Visual Studio 2022 のリリース バージョンはまだ利用できません。下のブートストラッパーは Visual Studio 2022 のプレビュー リリースのものです。
まず、[Visual Studio ダウンロード ページ](https://aka.ms/vs2022preview)から Visual Studio 2022 ブートストラッパーをダウンロードします。

| エディション                    | ダウンロード                                                                             |
|----------------------------|--------------------------------------------------------------------------------------|
| Visual Studio Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/preview/bootstrapper/vs_enterprise.exe)     |
| Visual Studio Professional | [vs_professional.exe](https://aka.ms/vs/17/preview/bootstrapper/vs_professional.exe) |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対する Visual Studio のリリースを調べるには、「[Visual Studio のビルド番号とリリース日](visual-studio-build-numbers-and-release-dates.md)」を参照してください。

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対応する Visual Studio のリリースを調べるには、「[Visual Studio 2019 リリース](/visualstudio/releases/2019/history)」を参照してください。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対応する Visual Studio のリリースを調べるには、「[Visual Studio 2022 リリース](/visualstudio/releases/2022/history)」を参照してください。

::: moniker-end

## <a name="create-an-offline-installation-folder"></a>オフライン インストール フォルダーを作成する

このステップを実行するにはインターネット接続が必要です。

コマンド プロンプトを開き、ブートストラップをダウンロードしたディレクトリに移動し、「[コマンドライン パラメーターを使用して Visual Studio をインストールする](../install/use-command-line-parameters-to-install-visual-studio.md)」ページで定義されているようにブートストラップのパラメーターを使用して、ネットワーク インストール キャッシュを作成および維持します。 初期レイアウトの作成の一般的な例については、下記と「[Visual Studio のインストールに使用するコマンド ライン パラメーターの例](../install/command-line-parameter-examples.md)」を参照してください。  

   > [!IMPORTANT]
   > 1 つの言語ロケールの完全な初期レイアウトを使用するには、Visual Studio Community では約 35 GB のディスク領域、Visual Studio Enterprise では 42 GB が必要です。 その他の[言語ロケール](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)には、それぞれ約 0.5 GB が必要になります。 詳細については、「[ネットワーク レイアウトをカスタマイズする](#customize-the-network-layout)」セクションを参照してください。 後続のレイアウトの更新プログラムも同じネットワークの場所に保存する必要があるため、ネットワーク レイアウトの場所のディレクトリの内容が時間の経過と共に大きくなる可能性があることに注意してください。  

- すべての言語とすべての機能が含まれる、Visual Studio Enterprise の初期レイアウトを作成するには、次のように実行します。

  ```vs_enterprise.exe --layout c:\VSLayout```

- すべての言語とすべての機能が含まれる、Visual Studio Professional の初期レイアウトを作成するには、次のように実行します。

  ```vs_professional.exe --layout c:\VSLayout```

## <a name="modify-the-responsejson-file"></a>response.json file を変更する

`response.json` ファイルを変更し、セットアップの実行時に使用される既定値を設定できます。  たとえば、自動での選択が必要な、特定のワークロード セットが選択されるように `response.json` ファイルを構成できます。 また、`response.json` を構成して、クライアントがネットワーク レイアウトの場所から更新されたファイルのみを受信する必要があるかどうかを指定することもできます。 詳細については、[応答ファイルを使用した Visual Studio インストールの自動化](../install/automated-installation-with-response-file.md)に関する記事を参照してください。 

Visual Studio ブートストラップを `response.json` ファイルとペアリングしている場合にエラーがスローされる問題が発生した場合の詳細については、[Visual Studio をインストールまたは使用するときのネットワーク関連のエラーのトラブルシューティング](../install/troubleshooting-network-related-errors-in-visual-studio.md#error-failed-to-parse-id-from-parent-process)に関する記事を参照してください。

## <a name="copy-the-layout-to-a-network-share"></a>ネットワーク共有にレイアウトをコピーする

クライアント コンピューターから実行できるようにネットワーク共有でレイアウトをホストします。

次の例では [`xcopy`](/windows-server/administration/windows-commands/xcopy/) が使用されます。 必要であれば、[`robocopy`](/windows-server/administration/windows-commands/robocopy/) を使用することもできます。

::: moniker range="vs-2017"

例:

```shell
xcopy /e c:\VSLayout \\server\products\VS2017
```

::: moniker-end

::: moniker range="vs-2019"

```shell
xcopy /e c:\VSLayout \\server\products\VS2019
```

::: moniker-end

::: moniker range=">=vs-2022"

```shell
xcopy /e c:\VSLayout \\server\products\VS2022
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

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US
    ```

* 複数の言語に対して、すべてのワークロードとコンポーネントをダウンロードするには、以下を実行します。

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US de-DE ja-JP
    ```

* すべての言語に対して、1 つのワークロードをダウンロードするには、以下を実行します。

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --includeRecommended
    ```

* 3 つの言語に対して、2 つのワークロードと 1 つのオプション コンポーネントをダウンロードするには、以下を実行します。

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended --lang en-US de-DE ja-JP
    ```

* 2 つのワークロードとその推奨コンポーネントのすべてをダウンロードするには:

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended
    ```

* 2 つのワークロードとそのすべての推奨コンポーネントと任意コンポーネントをダウンロードするには、次を実行します。

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeOptional
    ```

### <a name="save-your-layout-options"></a>レイアウト オプションの保存

レイアウト コマンドを実行すると、(ワークロードや言語などの) 指定したオプションが保存されます。 後続のレイアウトコマンドには、それ以前のすべてのオプションが含まれます。  英語のみ対象の 1 つのワークロードを含むレイアウトの例を示します。

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
```

レイアウトを新しいバージョンに更新したい場合、追加のコマンド ライン パラメーターを指定する必要はありません。 このレイアウト フォルダーに保存されている以前の設定が、後続のすべてのレイアウト コマンドで使用されます。  次のコマンドは、既存の部分的レイアウトを更新します。

```shell
vs_enterprise.exe --layout c:\VSLayout
```

追加のワークロードを追加したい場合は、次のようなコマンドを使用します。 この場合、Azure のワークロードとローカライズされた言語を追加します。  これで、Managed Desktop と Azure の両方がこのレイアウトに含まれるようになります。  これらのすべてのワークロードに、英語とドイツ語の言語リソースが含まれています。 レイアウトは利用可能な最新バージョンに更新されます。

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
```

既存のレイアウトを完全なレイアウトに更新したい場合は、次の例に示すように all オプションを使用します。

```shell
vs_enterprise.exe --layout c:\VSLayout --all
```

## <a name="deploy-from-a-network-installation"></a>ネットワーク インストールから展開する

管理者はインストール スクリプトの一部として Visual Studio をクライアント ワークステーションに展開することができます。 あるいは、管理者権限を持つユーザーは共有から直接セットアップを実行し、自分のコンピューターに Visual Studio をインストールできます。

* ユーザーは次のコマンドを実行してインストールできます。 <br>

    ```shell
    \\server\products\VS\vs_enterprise.exe
    ```

* 管理者は次のコマンドを実行することで、無人モードでインストールできます。

    ```shell
    \\server\products\VS\vs_enterprise.exe --quiet --wait --norestart
    ```

> [!IMPORTANT]
> エラーを防ぐには、レイアウト パス全体が 80 文字未満であることを確認してください。

> [!TIP]
> バッチ ファイルの一部として実行するとき、`--wait` オプションを利用すると、`vs_enterprise.exe` プロセスはインストールの完了を待ち、それから終了コードを返します。
>
> これは、企業の管理者が完了したインストールに追加のアクション (たとえば、[成功したインストールにプロダクト キーを適用する](automatically-apply-product-keys-when-deploying-visual-studio.md)など) を実行したい場合に便利ですが、そのインストールからのリターン コードを処理するにはインストールが終了するまで待つ必要があります。
>
> `--wait` を使用しない場合、インストールが完了する前に `vs_enterprise.exe` プロセスが終了し、インストール操作の状態を表していない不正確な終了コードが返されます。
>

::: moniker range=">=vs-2019"
> [!IMPORTANT]
> オフライン インストールで、"次のパラメーターと一致する製品が見つかりません" というエラー メッセージが表示される場合は、バージョン 16.3.5 以降で `--noweb` スイッチを使用していることを確認します。
>
::: moniker-end

レイアウトからインストールする場合、インストールされる内容はレイアウトから取得されます。 ただし、レイアウトに含まれないコンポーネントを選択した場合は、インターネットから取得されます。  Visual Studio のセットアップでレイアウトにない内容がダウンロードされないようにするには、`--noWeb` オプションを使用します。 `--noWeb` が使用されていて、インストール対象として選択されている内容がレイアウトにない場合、セットアップは失敗します。

> [!TIP]
> インターネットに接続されていないコンピューターのオフライン ソースからインストールする場合は、`--noWeb` と `--noUpdateInstaller` の両方のオプションを指定します。 前者では、更新されたワークロードやコンポーネントなどがダウンロードできなくなります。 後者では、インストーラーが Web から自己更新できなくなります。

> [!IMPORTANT]
> `--noWeb` オプションを使っても、インターネットに接続されたコンピューターにセットアップされた Visual Studio で更新プログラムのチェックが行われなくなることはありません。 詳細については、「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」ページをご覧ください。

### <a name="error-codes"></a>エラー コード

`--wait` パラメーターを使用した場合、操作の結果に応じて、`%ERRORLEVEL%` 環境変数は次のいずれかの値に設定されます。

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

## <a name="update-a-network-install-layout"></a>ネットワーク インストール レイアウトを更新する

製品の更新プログラムが利用できるようになったら、[ネットワーク インストール レイアウトを更新し](update-a-network-installation-of-visual-studio.md)、更新されたパッケージを組み込むことが推奨されます。

## <a name="how-to-create-a-layout-for-a-previous-visual-studio-release"></a>以前の Visual Studio リリースのレイアウトを作成する方法

まず、2 種類の Visual Studio ブートストラップがあることを理解しておく必要があります。"latest"、"current"、"evergreen"、および "tip" という文字が付けられたものと、本質的に "固定バージョン" を意味するものです。 どちらの種類のブートストラップ ファイルもまったく同じ名前で、種類を区別する最善の方法は、どこから入手したかに注目することです。 [Visual Studio のダウンロード ページ](https://visualstudio.microsoft.com/downloads)で入手できる Visual Studio ブートストラップは evergreen の Visual Studio ブートストラップと見なされ、ブートストラップの実行時にチャネルで利用可能な最新のリリースが常にインストール (または更新) されます。 「[Visual Studio 2019 リリース](/visualstudio/releases/2019/history)」、「[Visual Studio 2022 リリース](/visualstudio/releases/2022/history)」ページで使用可能な、または Microsoft Update カタログの管理者向け更新プログラムに埋め込まれている Visual Studio ブートストラップでは、特定の固定バージョンの製品がインストールされます。

そのため、Visual Studio の evergreen のブートストラップを今日ダウンロードし、今日から 6 か月後に実行すると、そのブートストラップの実行時点で最新の Visual Studio リリースがインストールされます。 常に最新のビットがインストールされ、最新になるように設計されています。

固定リンクのブートストラップをダウンロードした場合、または Microsoft カタログからダウンロードした管理者向け更新プログラムを実行した場合は、いつ実行されたかに関係なく、常に特定のバージョンの製品がインストールされます。

最後に、これらのブートストラップのいずれかを使用してネットワーク レイアウトを作成できます。また、レイアウトで作成されるバージョンは、使用しているブートストラップによって異なります。たとえば、固定バージョンまたは最新のいずれかになります。 それから、それ以降のブートストラップを使用してネットワーク レイアウトを更新したり、Microsoft Update カタログから管理者向け更新プログラムのパッケージを使用したりもできます。 レイアウトの更新方法に関係なく、結果として得られる更新後のレイアウトは、特定のバージョンの製品を含むパッケージ キャッシュになり、固定リンクのブートストラップのように動作します。 そのため、クライアントがレイアウトからインストールされるたびに、クライアントは (新しいバージョンがオンラインに存在する場合でも) レイアウトに存在する特定のバージョンの Visual Studio をインストールします。

### <a name="how-to-get-support-for-your-offline-installer"></a>オフライン インストーラーのサポートを受ける方法

オフライン インストールに問題が発生した場合は、マイクロソフトにお知らせください。 問題報告の最善の方法として、[[問題を報告する]](../ide/how-to-report-a-problem-with-visual-studio.md) ツールを使用できます。 このツールでは、テレメトリとログを送信できます。これを、マイクロソフトは問題の診断と解決に役立てます。

インストール関連の問題については、[**インストール チャット**](https://visualstudio.microsoft.com/vs/support/#talktous) (英語のみ) のサポート オプションも用意されています。

他にも利用可能なサポート オプションがあります。 一覧については、[フィードバック](../ide/feedback-options.md)に関するページをご覧ください。

## <a name="see-also"></a>関連項目

- [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
- [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
- [Visual Studio をインストールまたは使用するときのネットワーク関連のエラーのトラブルシューティング](troubleshooting-network-related-errors-in-visual-studio.md)
- [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
- [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)
- [サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)
- [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
- [Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)
- [Visual Studio オフライン インストールに必要な証明書をインストールする](install-certificates-for-visual-studio-offline.md)
