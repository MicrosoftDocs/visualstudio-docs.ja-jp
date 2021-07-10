---
title: 最小限のオフライン レイアウトを使用して Visual Studio を更新する
description: 最小限のオフライン レイアウトを使用して Visual Studio を更新する方法について説明します。
ms.date: 05/18/2021
ms.custom: seodec18
ms.topic: how-to
ms.assetid: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 1c3a6254c3205038be3d56c64de091e659d2bbd5
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306736"
---
# <a name="update-visual-studio-using-a-minimal-offline-layout"></a>最小限のオフライン レイアウトを使用して Visual Studio を更新する

インターネットに接続されていないコンピューターの場合、オフラインの Visual Studio インスタンスを更新する最も簡単かつ迅速な方法は、最小限のレイアウトを作成することです。

最小限のレイアウトのツールを使用すれば、チームのニーズに合わせて特別に調整されたレイアウトを生成できます。 エンタープライズ管理者は、このツールを使用することで、Visual Studio 2017 および 2019 のほとんどのバージョン用の更新レイアウトを作成できます。 完全な Visual Studio レイアウトとは異なり、最小限のレイアウトには更新されたパッケージのみが含まれるため、常により小さなサイズで、より高速に、生成と配置が行われます。 必要な言語、ワークロード、およびコンポーネントのみを指定すれば、更新レイアウトのサイズをさらに最小化することができます。

## <a name="how-to-generate-a-minimal-layout"></a>最小限のレイアウトを生成する方法

> [!IMPORTANT]
> これらの手順は、お客様が以前にレイアウトを作成して使用したことがあることを前提としています。 それを行う方法の詳細については、「[Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)」のページを参照してください。
>
> Visual Studio のライフサイクルの理解を深めるには、「[Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing)」のページを参照してください。
>

このツールでは、Visual Studio 2017 (15.9) 以降の更新レイアウトが作成されます。 このレイアウトをネットワークやオフラインのコンピューターに配置すれば、Visual Studio インスタンスを更新することができます。 [通常のレイアウトの作成](update-a-network-installation-of-visual-studio.md)時には、その特定のリリースのすべてのパッケージがダウンロードされます。 Visual Studio インスタンスの修復、アンインストール、その他の標準的な操作を行う場合は、通常のレイアウトの作成が必要になります。 最小限のレイアウトによってダウンロードされるのは更新されたパッケージのみであるため、オフライン コンピューターへのコピーはよりサイズが小さく、より簡単なものとなります。

### <a name="installing-the-minimal-layout-tool"></a>最小限のレイアウトのツールのインストール

 1. 最初に、[こちら](https://aka.ms/vs/installer/minimallayout)にある最小限のレイアウトのツールをダウンロードします。 メッセージが表示されたら必ず **[保存]** を選択し、次に **[実行]** を選択します。

     ![最小限のレイアウトのツールを保存する](media/save-minimal-layout.png)

 2. 次に、 **[はい]** をクリックして、ユーザー アカウント制御のプロンプトを受け入れます。

     ![ユーザー アカウント制御を受け入れる](media/accept-user-account-control.png)

 3. 最小限のレイアウトのツールは、`C:\Program Files (x86)\Microsoft Visual Studio\MinimalLayout` にインストールされます。

### <a name="how-to-use-the-minimal-layout-tool"></a>最小限のレイアウトのツールを使用する方法

`MinimalLayout.exe` では、次のコマンドとオプションを使用して、レイアウトが生成されます。 このツールを実行するには、少なくとも 1 つのコマンドが必要です。 ツールの実行方法は次のとおりです。

```MinimalLayout.exe [command] <options>...```

#### <a name="commands"></a>コマンド

* **プレビュー**: このコマンドを使用すると、ダウンロードされるパッケージの数と、このレイアウトの作成に使用される領域の合計をプレビューできます。
* **生成**: このコマンドを使用すると、Visual Studio を更新するための最小限のレイアウトを生成できます。
* **Regenerate**: このコマンドでは、既存の最小限のレイアウトの応答ファイルを使用してレイアウトを再生成できます。 すべての最小限のレイアウトで、`MinimalLayout.json` 応答ファイルが生成されます。これには、元々の最小限のレイアウトの入力パラメーターが含まれます。 **Regenerate** コマンドと `MinimalLayout.json` 応答ファイルを使用することで、最小限のレイアウトを再生成することができます。 これは、Visual Studio の新しい更新プログラムのための最小限のレイアウトを、以前の最小限のレイアウトの応答ファイルに基づいて作成する場合に便利です。

   このコマンドでは、既に生成されたレイアウトからの `MinimalLayout.json` ファイル パスが必要です。

   ```shell
   MinimalLayout.exe regenerate --filePath C:\MinimalLayout\MinimalLayout.json
   ```

* **Verify**: このコマンドを使用すると、レイアウト フォルダーが破損しているかどうかを確認できます。
* **解決策**:このコマンドを使用すると、レイアウト フォルダーで欠落しているパッケージを置き換えるなど、破損したレイアウト フォルダーを修正できます。

#### <a name="options"></a>オプション

::: moniker range=">=vs-2019"

| オプション                                             | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                 | 必須/省略可能               | 例                                                                                                                                                          |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --targetLocation &lt;dir&gt;                        | 最小限のオフライン レイアウトを作成するディレクトリを指定します。                                                                                                                                                                                                                                                                                                                                                                          | 必須                        | --targetLocation c:\VSLayout\                                                                                                                                    |
| --baseVersion &lt;version&gt;                       | このバージョン以降で、最小限のオフライン レイアウトが生成されます。                                                                                                                                                                                                                                                                                                                                                                    | 必須                        | --baseVersion 16.4.0                                                                                                                                             |
| --targetVersion &lt;version&gt;                     | このバージョンまで (このバージョンを含む)、最小限のオフラインレ イアウトが生成されます。                                                                                                                                                                                                                                                                                                                                                              | 必須                        | --targetVersion 16.4.4                                                                                                                                           |
| --languages                                         | 最小限のオフライン レイアウトに含める言語を指定します。 複数の値を指定するには、スペースで区切ります。                                                                                                                                                                                                                                                                                                                    | 必須                        | --languages en-US fr-FR                                                                                                                                          |
| --productIds &lt;1 つまたは複数の製品 ID&gt;        | 製品の ID。最小オフライン レイアウトはこれから生成されます。コンマで区切られます。 <br> <ul><li>Microsoft.VisualStudio.Product.Enterprise</li><li>Microsoft.VisualStudio.Product.Professional</li><li>Microsoft.VisualStudio.Product.BuildTools</li><li>Microsoft.VisualStudio.Product.TestAgent</li><li>Microsoft.VisualStudio.Product.TestController</li><li>Microsoft.VisualStudio.Product.TeamExplorer</li></ul> | 必須                        | --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional                                                               |
| --filePath                                          | 既に作成されているレイアウトからの MinimalLayout.json ファイルのファイル パス。 このオプションは、Regenerate コマンドでのみ使用されます。                                                                                                                                                                                                                                                                                                          | Regenerate コマンドで必須 | --filePath C:\VSLayout\minimalLayout.json <br><br> **Regenerate コマンドは、オプションとして --filePath のみを受け取ることに注意してください。**                                      |
| --add &lt;1 つまたは複数のワークロード ID またはコンポーネント ID&gt; | 追加する 1 つまたは複数のワークロード ID またはコンポーネント ID を指定します。 その他のコンポーネントをグローバルに追加するには、--includeRecommended または <br> –-includeOptional を使用します。 複数のワークロード ID またはコンポーネント ID を指定するには、スペースで区切ります。                                                                                                                                                                                                   | Optional                        | --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb Component.GitHub.VisualStudio                                        |
| --includeRecommended                                | インストールされているワークロードの推奨されるコンポーネントを含めますが、オプションのコンポーネントは含めません。                                                                                                                                                                                                                                                                                                                                  | Optional                        | 特定のワークロードの場合: <br> --add Microsoft.VisualStudio.Workload. ManagedDesktop;includeRecommended <br><br> すべてのワークロードに適用するには: --includeRecommended |
| --includeOptional                                   | インストールされているワークロードのオプションのコンポーネントを含めます (推奨されるコンポーネントを含む)。                                                                                                                                                                                                                                                                                                                                | Optional                        | 特定のワークロードの場合: <br>--add Microsoft.VisualStudio.Workload. ManagedDesktop;includeOptional <br><br> すべてのワークロードに適用するには: --includeOptional         |

::: moniker-end

::: moniker range="vs-2017"

| オプション                                             | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                 | 必須/省略可能               | 例                                                                                                                                                          |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --targetLocation &lt;dir&gt;                        | 最小限のオフライン レイアウトを作成するディレクトリを指定します。                                                                                                                                                                                                                                                                                                                                                                          | 必須                        | --targetLocation c:\VSLayout\                                                                                                                                    |
| --baseVersion &lt;version&gt;                       | このバージョン以降で、最小限のオフライン レイアウトが生成されます。                                                                                                                                                                                                                                                                                                                                                                    | 必須                        | --baseVersion 15.0.0                                                                                                                                             |
| --targetVersion &lt;version&gt;                     | このバージョンまで (このバージョンを含む)、最小限のオフラインレ イアウトが生成されます。                                                                                                                                                                                                                                                                                                                                                              | 必須                        | --targetVersion 15.9.31                                                                                                                                          |
| --languages                                         | 最小限のオフライン レイアウトに含める言語を指定します。 複数の値を指定するには、スペースで区切ります。                                                                                                                                                                                                                                                                                                                    | 必須                        | --languages en-US fr-FR                                                                                                                                          |
| --productIds &lt;1 つまたは複数の製品 ID&gt;        | 製品の ID。最小オフライン レイアウトはこれから生成されます。コンマで区切られます。 <br> <ul><li>Microsoft.VisualStudio.Product.Enterprise</li><li>Microsoft.VisualStudio.Product.Professional</li><li>Microsoft.VisualStudio.Product.BuildTools</li><li>Microsoft.VisualStudio.Product.TestAgent</li><li>Microsoft.VisualStudio.Product.TestController</li><li>Microsoft.VisualStudio.Product.TeamExplorer</li></ul> | 必須                        | --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional                                                               |
| --filePath                                          | 既に作成されているレイアウトからの MinimalLayout.json ファイルのファイル パス。 このオプションは、Regenerate コマンドでのみ使用されます。                                                                                                                                                                                                                                                                                                          | Regenerate コマンドで必須 | --filePath C:\VSLayout\minimalLayout.json <br><br> **Regenerate コマンドは、オプションとして --filePath のみを受け取ることに注意してください。**                                      |
| --add &lt;1 つまたは複数のワークロード ID またはコンポーネント ID&gt; | 追加する 1 つまたは複数のワークロード ID またはコンポーネント ID を指定します。 その他のコンポーネントをグローバルに追加するには、--includeRecommended または <br> –-includeOptional を使用します。 複数のワークロード ID またはコンポーネント ID を指定するには、スペースで区切ります。                                                                                                                                                                                                   | Optional                        | --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb Component.GitHub.VisualStudio                                        |
| --includeRecommended                                | インストールされているワークロードの推奨されるコンポーネントを含めますが、オプションのコンポーネントは含めません。                                                                                                                                                                                                                                                                                                                                  | Optional                        | 特定のワークロードの場合: <br> --add Microsoft.VisualStudio.Workload. ManagedDesktop;includeRecommended <br><br> すべてのワークロードに適用するには: --includeRecommended |
| --includeOptional                                   | インストールされているワークロードのオプションのコンポーネントを含めます (推奨されるコンポーネントを含む)。                                                                                                                                                                                                                                                                                                                                | Optional                        | 特定のワークロードの場合: <br>--add Microsoft.VisualStudio.Workload. ManagedDesktop;includeOptional <br><br> すべてのワークロードに適用するには: --includeOptional         |

::: moniker-end

### <a name="generating-a-minimal-layout"></a>最小限のレイアウトの生成

> [!IMPORTANT]
> これらの手順では、既にネットワーク インストール レイアウトを作成していることを前提としています。 手順の詳細については、「[Visual Studio のネットワーク インストールを作成する](create-a-network-installation-of-visual-studio.md)」ページを参照してください。

指定した範囲のバージョンに対して **generate** コマンドを使用して、最小限のレイアウトを作成します。 また、productId、言語、および必要な特定のワークロードについても理解しておく必要があります。 この最小限のレイアウトでは、基本バージョンからターゲット バージョンまで (ターゲット バージョンを含む) の Visual Studio インスタンスが更新されます。

レイアウトを作成する前に、**preview** コマンドを使用して、ダウンロードの合計サイズと、含まれるパッケージの数を確認できます。 このコマンドは、**generate** コマンドと同じオプションを受け取ります。詳細はコンソールに書き込まれます。

最小限のレイアウトをプレビュー、生成、および再生成する方法の例をいくつか見てみましょう。

::: moniker range=">=vs-2019"

* 最初に、英語のみの Visual Studio Enterprise バージョン 16.4.0 から 16.4.4 までについてレイアウトをプレビューする方法の例を次に示します。

  ```shell
  MinimalLayout.exe preview --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --languages en-US
  ```

* 1 つのワークロードで同じレイアウトを生成する方法を次に示します。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US
  ```

* 既存の応答ファイルを使用して最小限のオフライン レイアウトを再生成する方法を次に示します。

  ```shell
  MinimalLayout.exe regenerate -filepath c:\VSLayout\MinimalLayout.json
  ```

**generate** コマンドを使用するその他の例:

* その他のワークロード (推奨されるパッケージのみを含む) を追加する方法を次に示します。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Professional --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb;includeRecommended --languages en-US
  ```

* 複数の製品をサポートする最小オフライン レイアウトも生成できます。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional --baseVersion 16.4.0 --targetVersion 16.4.4 --languages en-US
  ```

* 最後に、最小限のレイアウトに複数の言語を含める方法を次に示します。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US fr-FR
  ```

::: moniker-end

::: moniker range="vs-2017"

* 最初に、英語のみの Visual Studio Enterprise バージョン 15.0.0 から 15.9.31 までについてレイアウトをプレビューする方法の例を次に示します。

  ```shell
  MinimalLayout.exe preview --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 15.0.0 --targetVersion 15.9.31 --languages en-US
  ```

* 1 つのワークロードで同じレイアウトを生成する方法を次に示します。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 15.0.0 --targetVersion 15.9.31 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US
  ```

* 既存の応答ファイルを使用して最小限のオフライン レイアウトを再生成する方法を次に示します。

  ```shell
  MinimalLayout.exe regenerate -filepath c:\VSLayout\MinimalLayout.json
  ```

**generate** コマンドを使用するその他の例:

* その他のワークロード (推奨されるパッケージのみを含む) を追加する方法を次に示します。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Professional --baseVersion 15.0.0 --targetVersion 15.9.31 --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb;includeRecommended --languages en-US
  ```

* 複数の製品をサポートする最小オフライン レイアウトも生成できます。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise,Microsoft.VisualStudio.Product.Professional --baseVersion 15.0.0 --targetVersion 15.9.31 --languages en-US
  ```

* 最後に、最小限のレイアウトに複数の言語を含める方法を次に示します。

  ```shell
  MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 15.0.0 --targetVersion 15.9.31 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US fr-FR
  ```

::: moniker-end

### <a name="how-to-maintain-a-minimal-layout"></a>最小限のレイアウトを維持する方法

**verify** および **fix** コマンドを使用すれば、最小限のレイアウトの作成後、それを維持することができます。 **verify** コマンドでは、最小限のレイアウト内に破損または欠落しているパッケージがあるかどうかが判断されます。 **verify** コマンドを実行してから問題が検出された場合は、**fix** コマンドを使用して、欠落または破損しているパッケージを修正します。

* レイアウトに破損または欠落しているパッケージがないかを確認する方法を次に示します。

  ```shell
  MinimalLayout.exe Verify --targetLocation c:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeRecommended --languages en-US
  ```

* そのレイアウトを修正する方法を次に示します。

  ```shell
  MinimalLayout.exe fix --targetLocation C:\VSLayout\ --productIds Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeRecommended --languages en-US
  ```

>[!NOTE]
> Visual Studio のインストールの修復に、このレイアウトを使用することはできません。 Visual Studio の既存のインスタンスを修復するには、「[Visual Studio を修復します](repair-visual-studio.md)」を参照してください。
>

### <a name="how-to-use-a-minimal-offline-layout-to-update-an-existing-installation-of-visual-studio"></a>最小限のオフライン レイアウトを使用して、Visual Studio の既存のインストールを更新する方法

最小限のレイアウトを生成したら、最小限のレイアウト フォルダー全体をクライアント コンピューターにコピーできます。 これが必要となるのは、元の場所にある最小限のレイアウト フォルダーへのアクセス権がコンピューターにない場合です。

フォルダーに移動し、ブートストラップ アプリケーション名を識別します。 ブート ストラップ アプリケーションの名前は、最小限のレイアウトの生成中に指定された ProductId 値によって異なります。 一般的な例については、次の表を参照してください。

| ProductId 値                             | アプリケーション名    |
|---------------------------------------------|---------------------|
| Microsoft.VisualStudio.Product.Enterprise   | vs_enterprise.exe   |
| Microsoft.VisualStudio.Product.Professional | vs_professional.exe |
| Microsoft.VisualStudio.Product.BuildTools   | vs_buildtools.exe   |

更新プログラムは、2 つのステップで Visual Studio インスタンスに適用されます。 まず Visual Studio インストーラーを更新し、次に Visual Studio を更新します。

::: moniker range="vs-2017"

1. **Visual Studio インストーラーを更新する**

    `vs_enterprise.exe` を必要に応じて正しいブート ストラップ アプリケーション名に置き換えて、次のコマンドを実行します。

    ```shell
    vs_enterprise.exe --quiet --update --offline C:\VSLayout\vs_installer.opc
    ```

2. **Visual Studio アプリケーションを更新する**

    Visual Studio を更新するには、更新する Visual Studio インスタンスの installPath を指定する必要があります。 Visual Studio の複数のインスタンスがインストールされている場合は、それぞれを個別に更新する必要があります。 最小限のレイアウトに含まれていないコンポーネントがインストールされるのを防ぐために、update コマンドに `–noWeb` オプションを指定することを強くお勧めします。 これにより、Visual Studio が使用できない状態になるのを防ぐことができます。

    installPath コマンドライン パラメーターを適宜、置き換えて、次のコマンドを実行します。 ブート ストラップ アプリケーション名も必ず正しいものを使用してください。

    ```shell
    vs_enterprise.exe update --noWeb --quiet --installpath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise"
    ```

::: moniker-end

::: moniker range="vs-2019"

1. **Visual Studio インストーラーを更新する**

    `vs_enterprise.exe` を必要に応じて正しいブート ストラップ アプリケーション名に置き換えて、次のコマンドを実行します。

    ```shell
    vs_enterprise.exe --quiet --update --offline C:\VSLayout\vs_installer.opc
    ```

2. **Visual Studio アプリケーションを更新する**

    Visual Studio を更新するには、更新する Visual Studio インスタンスの installPath を指定する必要があります。 Visual Studio の複数のインスタンスがインストールされている場合は、それぞれを個別に更新する必要があります。 最小限のレイアウトに含まれていないコンポーネントがインストールされるのを防ぐために、update コマンドに `–noWeb` オプションを指定することを強くお勧めします。 これにより、Visual Studio が使用できない状態になるのを防ぐことができます。

    installPath コマンドライン パラメーターを適宜、置き換えて、次のコマンドを実行します。 ブート ストラップ アプリケーション名も必ず正しいものを使用してください。

    ```shell
    vs_enterprise.exe update --noWeb --quiet --installpath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise"
    ```

::: moniker-end

::: moniker range=">=vs-2022"

1. **Visual Studio インストーラーを更新する**

    `vs_enterprise.exe` を必要に応じて正しいブート ストラップ アプリケーション名に置き換えて、次のコマンドを実行します。

    ```shell
    vs_enterprise.exe --quiet --update --offline C:\VSLayout\vs_installer.opc
    ```

2. **Visual Studio アプリケーションを更新する**

    Visual Studio を更新するには、更新する Visual Studio インスタンスの installPath を指定する必要があります。 Visual Studio の複数のインスタンスがインストールされている場合は、それぞれを個別に更新する必要があります。 最小限のレイアウトに含まれていないコンポーネントがインストールされるのを防ぐために、update コマンドに `–noWeb` オプションを指定することを強くお勧めします。 これにより、Visual Studio が使用できない状態になるのを防ぐことができます。

    installPath コマンドライン パラメーターを適宜、置き換えて、次のコマンドを実行します。 ブート ストラップ アプリケーション名も必ず正しいものを使用してください。

    ```shell
    vs_enterprise.exe update --noWeb --quiet --installpath "C:\Program Files\Microsoft Visual Studio\2022\Enterprise"
    ```

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
* [Visual Studio インスタンスの検出および管理用のツール](tools-for-managing-visual-studio-instances.md)
* [応答ファイルの設定を定義する方法](automated-installation-with-response-file.md)
* [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)
