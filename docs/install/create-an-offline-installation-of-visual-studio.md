---
title: オフライン インストールを作成する
description: インターネット接続の信頼性が低い場合や帯域幅が低い場合にオフラインで Visual Studio をインストールする方法について説明します。
ms.date: 4/16/2021
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- offline installation [Visual Studio]
- offline install [Visual Studio]
- layout [Visual Studio]
ms.assetid: f8625d5e-f6ea-4db0-83c0-619b77fab3cf
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: b10fc1adbb0b4a6e053549749ea90acf3919d0c6
ms.sourcegitcommit: 674d3fafa7c9e0cb0d1338027ef419a49c028c36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2021
ms.locfileid: "112602193"
---
# <a name="create-an-offline-installation-of-visual-studio"></a>Visual Studio のオフライン インストールを作成する

::: moniker range="vs-2017"

Visual Studio 2017 はさまざまなネットワークとコンピューターの構成で問題なく動作するように設計されています。 [Visual Studio Web インストーラー](https://visualstudio.microsoft.com/vs/older-downloads)を試すことを推奨していますが (これは最新の修正プログラムおよび機能が使用されるようにする小さなファイルです)、これが不可能な場合もあります。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio 2019 以降はさまざまなネットワーク構成およびコンピューター構成で問題なく動作するように設計されています。 [Visual Studio Web インストーラー](https://visualstudio.microsoft.com/downloads)を試すことを推奨していますが (これは最新の修正プログラムおよび機能が使用されるようにする小さなファイルです)、これが不可能な場合もあります。

::: moniker-end

たとえば、インターネット接続の信頼性が低い場合や帯域幅が低い場合があるでしょう。 その場合、いくつかの選択肢があります。新しい "全部ダウンロードしてからインストールする" 機能を使用してインストール前にファイルをダウンロードするか、コマンド ラインを使用してファイルのローカル キャッシュを作成することができます。

> [!NOTE]
> 企業の IT 管理者が、インターネットからファイアウォールで隔てられたクライアント ワークステーションのネットワークに Visual Studio を展開する場合は、[Visual Studio のネットワーク インストールの作成](../install/create-a-network-installation-of-visual-studio.md)に関するページと「[Visual Studio オフライン インストールに必要な証明書をインストールする](../install/install-certificates-for-visual-studio-offline.md)」をご覧ください。

## <a name="use-the-download-all-then-install-feature"></a>"全部ダウンロードしてからインストールする" 機能を使用する

::: moniker range="vs-2017"

[**15.8 の新機能**](/visualstudio/releasenotes/vs2017-relnotes-v15.8#install): Web インストーラーをダウンロードした後、Visual Studio インストーラーの新しい **[全部ダウンロードしてからインストールする]** オプションを選択します。 次に、インストールを続行します。

   !["全部ダウンロードしてからインストールする" オプション](media/download-all-then-install.png)

::: moniker-end

::: moniker range=">=vs-2019"

Web インストーラーをダウンロードした後、Visual Studio インストーラーから **[Download all, then install]\(全部ダウンロードしてからインストールする\)** オプションを選択します。 次に、インストールを続行します。

   !["全部ダウンロードしてからインストールする" オプション](media/vs-2019/download-all-then-install-from-installer.png)

::: moniker-end

"全部ダウンロードしてからインストールする" 機能は、ダウンロードしたのと同じコンピューターを対象とする 1 つのインストールとして Visual Studio をダウンロードできるように設計されています。 これにより、Visual Studio をインストールする前に安全に Web から切断できます。

> [!IMPORTANT]
> 別のコンピューターに転送する目的のオフライン キャッシュを作成するために "全部ダウンロードしてからインストールする" 機能を使わないでください。 これは、そのように動作するようには設計されていません。 <br><br>ローカル コンピューターにオフライン キャッシュを作成して、それを使用して Visual Studio をインストールする場合は、以下の「[コマンド ラインを使用してローカル キャッシュを作成する](#use-the-command-line-to-create-a-local-cache)」セクションを参照してください。  または、「[Visual Studio のネットワーク インストールを作成する](../install/create-a-network-installation-of-visual-studio.md)」ページに、ネットワーク上にキャッシュを作成する方法の情報があります。

## <a name="use-the-command-line-to-create-a-local-cache"></a>コマンドラインを使用してローカル キャッシュを作成する
::: moniker range="vs-2017"

小規模のブートストラップをダウンロードした後、コマンド ラインを使用してローカル キャッシュを作成します。 次に、ローカル キャッシュを使用して Visual Studio をインストールします。 (この手順は、以前のバージョンで利用できた ISO ファイルに代わるものです。) 

::: moniker-end

::: moniker range=">=vs-2019"

小規模のブートストラップ ファイルをダウンロードした後、コマンド ラインを使用してローカル キャッシュを作成します。 次に、ローカル キャッシュを使用して Visual Studio をインストールします。

::: moniker-end

### <a name="step-1---download-the-visual-studio-bootstrapper"></a>ステップ 1 - Visual Studio ブートストラップをダウンロードする

この手順を完了するには、インターネット接続が必要です。

::: moniker range="vs-2017"

Visual Studio 2017 バージョン 15.9 の最新のブートストラップを入手するには、[Visual Studio の以前のバージョン](https://visualstudio.microsoft.com/vs/older-downloads/)のページに移動し、次のいずれかのブートストラップ ファイルをダウンロードします。

| エディション                                      | ファイル名            |
|----------------------------------------------|---------------------|
| Visual Studio Professional 2017 バージョン 15.9 | vs_professional.exe |
| Visual Studio Enterprise 2017 バージョン 15.9   | vs_enterprise.exe   |
| Visual Studio Build Tools 2017 バージョン 15.9  | vs_buildtools.exe   |

::: moniker-end

::: moniker range="vs-2019"

まずは、Visual Studio 2019 のブートストラップを、[Visual Studio のダウンロード ページ](https://visualstudio.microsoft.com/downloads)または、「[Visual Studio 2019 リリース](/visualstudio/releases/2019/history#installing-an-earlier-release)」のページからご自分で選択した Visual Studio のバージョンおよびエディション用にダウンロードします。 お使いのセットアップ ファイル &mdash; またはブートストラップ &mdash; は、次のいずれかになります (あるいは同様のファイル)。

| Edition                         | ファイル                                                                                                                                                                                                                               |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Studio 2019 Community    | [vs_community.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)       |
| Visual Studio 2019 Professional | [vs_professional.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019) |
| Visual Studio 2019 Enterprise   | [vs_enterprise.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)     |
| Visual Studio 2019 Build Tools  | [vs_buildtools.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)     |

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
> Visual Studio 2022 のリリース バージョンはまだ利用できません。下のブートストラッパーは Visual Studio 2022 のプレビュー リリースのものです。
>まず、[Visual Studio ダウンロード ページ](https://aka.ms/vs2022preview)から Visual Studio 2022 ブートストラッパーをダウンロードします。

| エディション                         | ダウンロード                                                            |
|---------------------------------|---------------------------------------------------------------------|
| Visual Studio 2022 Professional | [vs_professional.exe](https://aka.ms/vs/17/pre/vs_professional.exe) |
| Visual Studio 2022 Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/pre/vs_enterprise.exe)     |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対応する Visual Studio のリリースを調べるには、「[Visual Studio のビルド番号とリリース日](/visual-studio-build-numbers-and-release-dates.md)」ページを参照してください。

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対応する Visual Studio のリリースを調べるには、「[Visual Studio 2019 リリース](/visualstudio/releases/2019/history)」のページを参照してください。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対応する Visual Studio のリリースを調べるには、「[Visual Studio 2022 リリース](/visualstudio/releases/2022/history)」のページを参照してください。

::: moniker-end

### <a name="step-2---create-a-local-install-cache"></a>ステップ 2 - ローカル インストール キャッシュを作成する

この手順を完了するには、インターネット接続が必要です。

コマンド プロンプトを開き、「[コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)」ページで定義されているブートストラップのパラメーターを使用して、ご自分のローカル インストール キャッシュを作成します。 Enterprise のブートストラップを使用する一般的な例については、[コマンド ライン パラメーターの例](command-line-parameter-examples.md)に関するページを参照してください。 英語以外の言語をインストールするには、`en-US` を「[言語ロケールの一覧](#list-of-language-locales)」のロケールに変更します。また、[コンポーネントとワークロードのリスト](workload-and-component-ids.md) を使用して、お使いのキャッシュをさらにカスタマイズできます。

> [!TIP]
> エラーを防ぐために、インストール パス全体が 80 文字未満であることを確認してください。

- .NET Web と .NET デスクトップ開発の場合、次を実行します。

   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
    ```

- .NET デスクトップと Office 開発の場合、次を実行します。

   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.Office --includeOptional --lang en-US
    ```

- C++ デスクトップ開発の場合、次を実行します。

   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --lang en-US
    ```

- すべての機能を備えた完全なローカル レイアウトを作成するには (英語のみ)、次を実行します ("_多くの_" 機能があるため、これには時間がかかります)。

   ```shell
    vs_enterprise.exe --layout c:\vslayout --lang en-US
    ```

::: moniker range="vs-2017"

   > [!NOTE]
   > Visual Studio の完全なレイアウトでは、少なくとも 35 GB のディスク領域が必要です。 詳細については、[システム要件](/visualstudio/productinfo/vs2017-system-requirements-vs/)に関するページを参照してください。 

::: moniker-end

::: moniker range=">=vs-2019"

   > [!NOTE]
   > Visual Studio の完全なレイアウトでは、少なくとも 41 GB のディスク領域が必要です。 詳細については、[システム要件](/visualstudio/releases/2019/system-requirements/)に関するページを参照してください。

::: moniker-end


### <a name="step-3---install-visual-studio-from-the-local-cache"></a>ステップ 3 - ローカル キャッシュから Visual Studio をインストールする
Visual Studio をローカル インストール キャッシュからインストールすると、Visual Studio インストーラーでは、そのファイルのローカルにキャッシュされたバージョンを使用します。 ただし、インストール時にキャッシュにないコンポーネントを選択すると、Visual Studio インストーラーではそれをインターネットからダウンロードしようとします。 以前にダウンロードしたファイルのみをインストールするには、レイアウト キャッシュの作成に利用したのと同じ[コマンド ライン オプション](use-command-line-parameters-to-install-visual-studio.md)を使用します。 

たとえば、次のコマンドでローカルのインストール キャッシュを作成した場合、

```shell
vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
```

次に、このコマンドを使用してインストールを実行します。

```shell
c:\vslayout\vs_enterprise.exe --noweb --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional
```

> [!IMPORTANT]
> Visual Studio Community を使用している場合は、インストール後 30 日以内に製品にログインし、ライセンス認証を行う必要があります。 ライセンス認証には、インターネット接続が必要です。

> [!NOTE]
> 署名が無効であるというエラーが発生する場合は、[更新された証明書をインストールする](install-certificates-for-visual-studio-offline.md)必要があります。 オフライン キャッシュ内の証明書フォルダーを開きます。 各証明書ファイルをダブルクリックした後、証明書マネージャー ウィザードの指示に従って操作します。 パスワードを求められたら、空のままにしてください。

::: moniker range=">=vs-2019"
> [!TIP]
> オフライン インストールで、"次のパラメーターと一致する製品が見つかりません" というエラー メッセージが表示される場合は、バージョン 16.3.5 以降で `--noweb` スイッチを使用していることを確認します。

::: moniker-end

### <a name="list-of-language-locales"></a>言語ロケールの一覧

| **言語ロケール** | **Language**          |
|---------------------|-----------------------|
| cs-CZ               | チェコ語                 |
| de-DE               | ドイツ語                |
| ja-JP               | 英語               |
| es-ES               | スペイン語               |
| fr-FR               | フランス語                |
| it-IT               | イタリア語               |
| ja-JP               | 日本語              |
| ko-KR               | 韓国語                |
| pl-PL               | ポーランド語                |
| pt-BR               | ポルトガル語 - ブラジル   |
| ru-RU               | ロシア語               |
| tr-TR               | トルコ語               |
| zh-CN               | 中国語 - 簡体字  |
| zh-TW               | 中国語 - 繁体字 |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

- [Visual Studio のネットワーク インストールを作成する](../install/create-a-network-installation-of-visual-studio.md)
- [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
- [Visual Studio オフライン インストールに必要な証明書をインストールする](../install/install-certificates-for-visual-studio-offline.md)
- [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
- [Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)
