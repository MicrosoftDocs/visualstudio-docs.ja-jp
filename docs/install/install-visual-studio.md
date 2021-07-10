---
title: Visual Studio のインストール
titleSuffix: ''
description: Visual Studio をインストールする方法について、ステップ バイ ステップで説明します。
ms.date: 12/13/2019
ms.custom: vs-acquisition
ms.topic: conceptual
helpviewer_keywords:
- install Visual Studio
- dev15
- set up Visual Studio
- Visual Studio setup
- Visual Studio installer
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 7bf44f9333a65ea821c0cd9936ee1f3fa051d4fe
ms.sourcegitcommit: d3658667e768d7516cbf4461ec47bf24c8fcb7e6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112925086"
---
# <a name="install-visual-studio"></a>Visual Studio のインストール

::: moniker range="vs-2019"

Visual Studio 2019 へようこそ このバージョンでは、必要な機能だけを簡単に選択してインストールできます。 占有領域が最小限まで小さくなっているため、インストールが速く、システムにほとんど影響しません。

::: moniker-end

::: moniker range=">=vs-2022"

Visual Studio 2022 へようこそ このバージョンでは、必要な機能だけを簡単に選択してインストールできます。 占有領域が最小限まで小さくなっているため、インストールが速く、システムにほとんど影響しません。

::: moniker-end

::: moniker range="vs-2017"

ここでは、Visual Studio の新しいインストール方法について説明します。 このバージョンでは、必要な機能だけを簡単に選んでインストールできるようになりました。 また、Visual Studio の最小フットプリントも減らしているため、以前よりもシステムへの影響が少なくなり、より迅速にインストールできます。

::: moniker-end

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac のインストール](/visualstudio/mac/installation/)に関するページを参照してください。

::: moniker range="vs-2019"

このバージョンの他の新機能については、 [リリース ノート](/visualstudio/releases/2019/release-notes/)を参照してください。

::: moniker-end

::: moniker range=">=vs-2022"

このバージョンの他の新機能については、 [リリース ノート](/visualstudio/releases/2022/release-notes/)を参照してください。

::: moniker-end

::: moniker range="vs-2017"

このバージョンの他の新機能については、 [リリース ノート](/visualstudio/releasenotes/vs2017-relnotes)を参照してください。

::: moniker-end

インストールの準備ができたら、 各ステップを順に実行していきます。

## <a name="step-1---make-sure-your-computer-is-ready-for-visual-studio"></a>手順 1 - コンピューターで Visual Studio の準備ができていることを確認する

Visual Studio のインストールを開始する前に

::: moniker range="vs-2017"

1. [システム要件](/visualstudio/productinfo/vs2017-system-requirements-vs)を確認します。 これらの要件により、ご利用のコンピューターが Visual Studio 2017 に対応しているかどうかを確認できます。

1. 最新の Windows 更新プログラムを適用します。 これらの更新プログラムにより、Visual Studio の最新のセキュリティ更新プログラムと必要なシステム コンポーネントの両方がコンピューターにインストールされます。

1. 再起動します。 この再起動により、Visual Studio のインストールの際に妨げとなる、保留中のインストールや更新プログラムがないようにします。

1. 記憶域を解放します。 ディスク クリーンアップ アプリを実行するなどして、%SystemDrive% から不要なファイルとアプリケーションを削除します。

::: moniker-end

::: moniker range="vs-2019"

1. [システム要件](/visualstudio/releases/2019/system-requirements)を確認します。 これらの要件により、ご利用のコンピューターが Visual Studio 2019 に対応しているかどうかを確認できます。

1. 最新の Windows 更新プログラムを適用します。 これらの更新プログラムにより、Visual Studio の最新のセキュリティ更新プログラムと必要なシステム コンポーネントの両方がコンピューターにインストールされます。

1. 再起動します。 この再起動により、Visual Studio のインストールの際に妨げとなる、保留中のインストールや更新プログラムがないようにします。

1. 記憶域を解放します。 ディスク クリーンアップ アプリを実行するなどして、%SystemDrive% から不要なファイルとアプリケーションを削除します。

::: moniker-end

::: moniker range=">=vs-2022"

1. [システム要件](/visualstudio/releases/2022/system-requirements)を確認します。 これらの要件により、ご利用のコンピューターが Visual Studio 2022 に対応しているかどうかを確認できます。

1. 最新の Windows 更新プログラムを適用します。 これらの更新プログラムにより、Visual Studio の最新のセキュリティ更新プログラムと必要なシステム コンポーネントの両方がコンピューターにインストールされます。

1. 再起動します。 この再起動により、Visual Studio のインストールの際に妨げとなる、保留中のインストールや更新プログラムがないようにします。

1. 記憶域を解放します。 ディスク クリーンアップ アプリを実行するなどして、%SystemDrive% から不要なファイルとアプリケーションを削除します。

::: moniker-end

::: moniker range="vs-2017"

Visual Studio 2017 と以前のバージョンの Visual Studio を共存させて実行することについて疑問点があれば、[Visual Studio の互換性の詳細](/visualstudio/productinfo/vs2017-compatibility-vs#compatibility-with-previous-releases)に関する記事をご覧ください。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio 2019 と以前のバージョンの Visual Studio を共存させて実行することについて疑問点がある場合は、「[Visual Studio 2019 の対象プラットフォームと互換性](/visualstudio/releases/2019/compatibility/)」ページをご覧ください。

::: moniker-end

::: moniker range=">=vs-2022"

Visual Studio 2022 と以前のバージョンの Visual Studio を共存させて実行することについて疑問点がある場合は、[Visual Studio 2022 の対象プラットフォームと互換性](/visualstudio/releases/2019/compatibility/)に関するページをご覧ください。

::: moniker-end

## <a name="step-2---download-visual-studio"></a>手順 2 - Visual Studio をダウンロードする

次に、Visual Studio ブートストラップ ファイルをダウンロードします。

::: moniker range="vs-2017"

Visual Studio 2017 のブートストラップを取得するには、その方法の詳細について、[以前のバージョンの Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) のダウンロード ページを参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

これを行うには、以下のボタンを選択し、必要な Visual Studio のエディションを選択して、 **[保存]** 、 **[フォルダーを開く]** の順に選択します。

 > [!div class="button"]
 > [Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads)

::: moniker-end

## <a name="step-3---install-the-visual-studio-installer"></a>手順 3 - Visual Studio インストーラーをインストールする

ブートストラップ ファイルを実行して、Visual Studio インストーラーをインストールします。 この新しい軽量インストーラーには、Visual Studio のインストールとカスタマイズの両方に必要なすべてのものが含まれています。

1. **[ダウンロード]** フォルダーで、次のいずれかのファイルと一致する、または似ているブートストラップをダブルクリックします。

   * Visual Studio Community の場合は **vs_community.exe**
   * Visual Studio Professional の場合は **vs_professional.exe**
   * Visual Studio Enterprise の場合は **vs_enterprise.exe**

   ユーザー アカウント制御の通知を受信する場合、 **[はい]** を選択します。

2. Microsoft の[ライセンス条項](https://visualstudio.microsoft.com/license-terms/)と[プライバシーに関する声明](https://privacy.microsoft.com/privacystatement)の確認を求められます。 **[続行]** を選択します。

   ![ライセンス条項とプライバシーに関する声明](media/privacy-and-license-terms.png "Microsoft ライセンス条項とプライバシーに関する声明")

## <a name="step-4---choose-workloads"></a>手順 4 - ワークロードを選択する

インストーラーがインストールされたら、それを使用して、必要な機能セット (またはワークロード) を選択し、インストールをカスタマイズすることができます。 以下にその方法を示します。

 ::: moniker range="vs-2017"

1. **Visual Studio インストーラー** で必要なワークロードを見つけます。

   ![Visual Studio 2017: ワークロードをインストールする](../install/media/vs-installer-installing-workloads.png)

     たとえば、".NET デスクトップ開発" ワークロードを選択します。 これには既定のコア エディターが用意されており、20 を超える言語の基本的なコード編集サポートが含まれ、プロジェクトなしで任意のフォルダーからコードを開いて編集することができます。また、統合ソース コード管理を利用できます。

1. 必要なワークロード (複数可) を選択した後、**[インストール]** を選択します。

    そうすると、ステータス画面が表示され、Visual Studio のインストールの進行状況が示されます。

 ::: moniker-end

::: moniker range=">=vs-2019"

1. **Visual Studio インストーラー** で必要なワークロードを見つけます。

   ![Visual Studio 2019:ワークロードをインストールする](../install/media/vs-2019/vs-installer-workloads.png)

     たとえば、"ASP.NET と Web 開発" ワークロードを選択します。 これには既定のコア エディターが用意されており、20 を超える言語の基本的なコード編集サポートが含まれ、プロジェクトなしで任意のフォルダーからコードを開いて編集することができます。また、統合ソース コード管理を利用できます。

1. 必要なワークロード (複数可) を選択した後、**[インストール]** を選択します。

    そうすると、ステータス画面が表示され、Visual Studio のインストールの進行状況が示されます。

 ::: moniker-end

> [!TIP]
> インストール後いつでも、最初にインストールしなかったワークロードまたはコンポーネントをインストールできます。 Visual Studio を開いている場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動すると、Visual Studio インストーラーが開きます。 または、スタート メニューから **Visual Studio インストーラー** を開きます。 そこから、インストールするワークロードまたはコンポーネントを選択できます。 次に、 **[変更]** を選択します。

## <a name="step-5---choose-individual-components-optional"></a>手順 5 - 個々のコンポーネントを選択する (省略可能)

ワークロード機能を使用して Visual Studio のインストールをカスタマイズしない場合、またはワークロードのインストール以外のコンポーネントを追加する場合は、 **[個別のコンポーネント]** タブから個々のコンポーネントをインストールまたは追加することによって行うことができます。必要なものを選択した後、画面の指示に従います。

::: moniker range="vs-2017"

  ![Visual Studio 2017 - 個々のコンポーネントのインストール](media/vs-installer-installing-components.png "Visual Studio の個々のコンポーネントをインストールする")

::: moniker-end

::: moniker range=">=vs-2019"

  ![Visual Studio 2019 - 個々のコンポーネントのインストール](media/vs-2019/vs-installer-individual-components.png "Visual Studio の個々のコンポーネントをインストールする")

::: moniker-end

## <a name="step-6---install-language-packs-optional"></a>手順 6 - 言語パックをインストールする (省略可能)

既定では、インストーラー プログラムが、最初の実行時にオペレーティング システムの言語の照合を試みます。 選択した言語で Visual Studio をインストールするには、Visual Studio インストーラーで **[言語パック]** タブをクリックした後、画面の指示に従います。

::: moniker range="vs-2017"

  ![Visual Studio 2017 - 言語パックのインストール](media/vs-installer-installing-language-packs.png "Visual Studio の言語パックをインストールする")

::: moniker-end

::: moniker range=">=vs-2019"

  ![Visual Studio 2019 - 言語パックのインストール](media/vs-2019/vs-installer-language-packs.png "Visual Studio の言語パックをインストールする")

::: moniker-end

### <a name="change-the-installer-language-from-the-command-line"></a>コマンド ラインかインストーラーの言語を変更する

コマンド ラインからインストーラーを実行して、既定の言語を変更することもできます。 たとえば、`vs_installer.exe --locale en-US` コマンドを実行して、インストーラーを英語で実行するように指定することができます。 この設定は、次回インストーラーを実行したときにも保持されています。 インストーラーでは次の言語トークンがサポートされます。zh-cn、zh-tw、cs-cz、en-us、es-es、fr-fr、de-de、it-it、ja-jp、ko-kr、pl-pl、pt-br、ru-ru、tr-tr。

## <a name="step-7---select-the-installation-location-optional"></a>手順 7 - インストールの場所を選択する (省略可能)

::: moniker range="vs-2017"

**15.7 の新機能**: システム ドライブ上の Visual Studio のインストール フットプリントを小さくできるようになりました。 ダウンロード キャッシュ、共有コンポーネント、SDK、およびツールを別のドライブに移動して、Visual Studio を最速で実行できるドライブで維持できます。

  ![Visual Studio 2017 - インストール場所を変更する](media/installation-options-by-location.png "インストールの場所を変更する")

::: moniker-end

::: moniker range=">=vs-2019"

システム ドライブ上の Visual Studio のインストール占有領域を小さくすることができます。 ダウンロード キャッシュ、共有コンポーネント、SDK、およびツールを別のドライブに移動して、Visual Studio を最速で実行できるドライブで維持できます。

  ![Visual Studio 2019 - インストール場所を選択する](media/vs-2019/vs-installer-installation-locations.png "インストールの場所を選択する")

::: moniker-end

> [!IMPORTANT]
> Visual Studio を初めてインストールするときにのみ、別のドライブを選択できます。 既にインストールしてあるドライブを変更する場合は、Visual Studio をアンインストールした後、再インストールする必要があります。

詳しくは、「[インストールの場所を選択する](change-installation-locations.md)」ページをご覧ください。

## <a name="step-8---start-developing"></a>手順 8 - 開発を始める

::: moniker range="vs-2017"

1. Visual Studio のインストールが完了したら **[起動]** を選択して、Visual Studio を使用した開発を開始します。

2. **[ファイル]** を選択して、**[新しいプロジェクト]** を選択します。

3. プロジェクトの種類を選択します。

   たとえば、[C++ アプリをビルドする](/cpp/get-started/tutorial-console-cpp)には、**[インストール済み]** を選択し、**[Visual C++]** を展開して、ビルドする C++ プロジェクトの種類を選択します。

   [C# アプリをビルドする](../get-started/csharp/tutorial-console.md)には、**[インストール済み]** を選択し、**[Visual C#]** を展開して、ビルドする C# プロジェクトの種類を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio のインストールが完了したら **[起動]** を選択して、Visual Studio を使用した開発を開始します。

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

1. 検索ボックスに作成するアプリの種類を入力し、使用可能なテンプレートの一覧を表示します。 テンプレートの一覧は、インストール時に選択したワークロードに依存します。 別のテンプレートを表示するには、異なるワークロードを選択します。

   **[言語]** ドロップダウン リストを使用して、特定のプログラミング言語に検索をフィルター処理することもできます。 **[プラットフォーム]** の一覧や **[プロジェクトの種類]** の一覧を使用して、フィルター処理することもできます。

1. Visual Studio で新しいプロジェクトが開き、コーディングできる状態になります。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio の更新](update-visual-studio.md)
* [Visual Studio の変更](modify-visual-studio.md)
* [Visual Studio のアンインストール](uninstall-visual-studio.md)
* [Visual Studio のオフライン インストールを作成する](create-an-offline-installation-of-visual-studio.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
* [Visual Studio for Mac をインストールする](/visualstudio/mac/installation)
 
