---
title: Visual Studio を更新する
titleSuffix: ''
description: Visual Studio を最新のリリースに更新する詳細な手順を説明します。
ms.date: 04/06/2021
ms.custom: vs-acquisition
ms.topic: how-to
ms.prod: visual-studio-windows
ms.technology: vs-installation
helpviewer_keywords:
- update [Visual Studio]
- change [Visual Studio]
f1_keywords:
- VS.ToolsOptionsPages.Environment.ProductUpdates
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8414d745b63eb0e9145208dca97ce9f117c5cf2c
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387958"
---
# <a name="update-visual-studio-to-the-most-recent-release"></a>Visual Studio を最新リリースに更新する

::: moniker range="vs-2017"

常に最新の機能、修正、改善を利用できるように、Visual Studio 2017 の[最新リリース](/visualstudio/releasenotes/vs2017-relnotes/)に更新することをお勧めします。

また、最新バージョンを試す場合は、代わりに [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) のダウンロードとインストールを検討してください。

> [!IMPORTANT]
> Visual Studio をインストール、更新、または変更するには、管理アクセス許可を持つアカウントでログオンする必要があります。 詳細については、「[ユーザー アクセス許可と Visual Studio](../ide/user-permissions-and-visual-studio.md)」を参照してください。
>
> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[Visual Studio for Mac を更新する](/visualstudio/mac/update)」を参照してください。

## <a name="update-visual-studio-2017-version-156-or-later"></a>Visual Studio 2017 バージョン 15.6 以降を更新する

IDE 内から直接使用しやすくするために、インストールと更新プログラムのエクスペリエンスが整理されました。 ここでは、バージョン 15.6 以降から新しいバージョンの Visual Studio に更新する方法について説明します。

### <a name="using-the-notifications-hub"></a>通知ハブの使用

更新プログラムがある場合、Visual Studio には対応する通知フラグが表示されます。

1. 作業内容を保存します。

1. 通知フラグを選択して **通知** ハブを開き、インストールする更新プログラムを選択します。

   ![通知ハブを使用して Visual Studio 2017 を更新する](media/vs-install-notifications-hub-15dot6.png "Visual Studio 2017 の通知ハブ")

      > [!TIP]
      > Visual Studio 2017 のエディションに対する更新プログラムは累積になっているため、常に最新のバージョン番号のものをインストールしてください。

1. **[更新]** ダイアログ ボックスが開いたら、 **[今すぐ更新]** を選択します。

    ![通知ハブの [更新] ダイアログボックスを使用して Visual Studio 2017 を更新する](media/vs-update-now-from-notifications-hub.png "Visual Studio の通知ハブの [更新] ダイアログ ボックス")

     [ユーザー アクセス制御] ダイアログ ボックスが開いたら、 **[はい]** を選択します。 [お待ちください] ダイアログが表示されることがあります。処理が完了すると、Visual Studio インストーラーが開き、更新が開始されます。

     ![バージョン 15.6 の新しい Visual Studio インストーラー エクスペリエンス](media/visual-studio-15dot6-installer.png "バージョン 15.6 の新しい Visual Studio インストーラー エクスペリエンス")

     更新が続行されます。 処理が完了すると、Visual Studio が再起動されます。

     > [!NOTE]
     > Visual Studio を管理者モードで実行する場合は、更新後に Visual Studio を手動で再起動する必要があります。

### <a name="using-the-ide"></a>IDE の使用

更新プログラムを確認し、Visual Studio のメニュー バーから更新プログラムをインストールすることができます。

1. 作業内容を保存します。

1. **[ヘルプ]** > **[更新プログラムの確認]** を選択します。

     ![Visual Studio バージョン 15.6 の新しい [ヘルプ] メニュー](media/vs-help-menu-check-for-updates.png "Visual Studio バージョン 15.6 の新しい [ヘルプ] メニュー")

1. **[更新]** ダイアログ ボックスが開いたら、 **[今すぐ更新]** を選択します。

   前のセクションと同様に更新が実行され、更新が正常に完了すると Visual Studio が再起動されます。

   > [!NOTE]
   > Visual Studio を管理者モードで実行する場合は、更新後に Visual Studio を手動で再起動する必要があります。

### <a name="using-the-visual-studio-installer"></a>Visual Studio インストーラーの使用

Visual Studio の以前のバージョンと同様に、Visual Studio インストーラーを使用して更新プログラムをインストールすることもできます。

1. 作業内容を保存します。

1. インストーラーを開きます。 必要に応じて、Visual Studio インストーラーを更新してから続行します。

   > [!NOTE]
   > Windows 10 を実行しているコンピューターの場合、**V** という文字の下に **Visual Studio インストーラー** と表示されるか、**M** という文字の下に **Microsoft Visual Studio インストーラー** と表示されます。

1. インストーラーの **[製品]** ページで、前にインストールした Visual Studio のエディションを探します。

1. 更新プログラムが使用可能な場合は、 **[更新]** ボタンが表示されます (使用可能な更新プログラムがあるかどうかをインストーラーが判断するために数秒かかる場合があります)。

   **[更新]** ボタンを選択して更新プログラムをインストールします。

     ![Visual Studio インストーラーを使用して Visual Studio 2017 を更新する](media/update-visual-studio.png "Visual Studio インストーラーを使用して Visual Studio 2017 を更新する")

## <a name="update-visual-studio-2017-version-155-or-earlier"></a>Visual Studio 2017 バージョン 15.5 以前のバージョンを更新する

以前のバージョンを使用している場合、Visual Studio 2017 バージョン 15.0 からバージョン 15.5 の更新プログラムを適用するには、次の手順を実行します。

### <a name="update-by-using-the-notifications-hub"></a>通知ハブを使用して更新する

1. 更新プログラムがある場合、Visual Studio には対応する通知フラグが表示されます。

   ![Visual Studio 2017 の通知フラグを更新する](media/notification-flag.png "Visual Studio の更新の通知フラグ")

   通知フラグを選択して、**通知** ハブを開きます。

   ![通知ハブの Visual Studio 2017 更新プログラム](media/notifications-hub.png "通知ハブの Visual Studio 2017 更新プログラム")

      > [!TIP]
      > Visual Studio 2017 のエディションに対する更新プログラムは累積になっているため、常に最新のバージョン番号のものをインストールしてください。

1. **["Visual Studio 更新プログラム" が使用可能です]** を選択すると、 **[拡張機能と更新プログラム]** ダイアログ ボックスが開きます。

   ![Visual Studio の更新プログラムを選択する](media/notifications-hub-select.png "Visual Studio の更新プログラムを選択する")

1. **[拡張機能と更新プログラム]** ダイアログ ボックスで、 **[更新]** ボタンを選択します。

   ![[拡張機能と更新プログラム] ダイアログで [更新] を選択する](media/notifications-extensions-and-updates.png "Visual Studio の [拡張機能と更新プログラム] ダイアログ")

#### <a name="more-about-visual-studio-notifications"></a>Visual Studio の通知の詳細

Visual Studio は、Visual Studio 自体またはいずれかのコンポーネントの更新プログラムが入手可能な場合に通知します。また、Visual Studio 環境で特定のイベントが発生した場合も通知します。

* 通知フラグが黄色の場合は、インストールできる Visual Studio 製品の更新プログラムが存在します。
* 通知フラグが赤の場合は、ライセンスに問題があります。
* 通知フラグが黒の場合は、確認のためのオプション メッセージまたは情報メッセージが存在します。

通知フラグを選択して **通知** ハブを開いてから、操作する通知を選択します。 または、通知を無視するか破棄するかを選択します。

 ![通知ハブでオプション メッセージまたは情報メッセージを表示する](media/notification-flag-optional.png "Visual Studio のオプション メッセージまたは情報メッセージの通知フラグ")

通知を無視することを選択した場合は、Visual Studio で表示されなくなります。 無視される通知のリストをリセットする場合は、通知ハブの **[設定]** ボタンを選択します。

   ![通知ハブの設定ボタンを選択して通知オプションを表示する](media/vs-notifications-hub-settings-button.png "通知ハブの [設定] ボタンを選択して通知オプションを表示する")

### <a name="update-by-using-the-visual-studio-installer"></a>Visual Studio インストーラーを使用して更新する

1. インストーラーを開きます。 続行する前に、インストーラーの更新が必要な場合があります。 更新が必要な場合は、更新するよう求められます。

   > [!NOTE]
   > Windows 10 を実行しているコンピューターの場合、**V** という文字の下に **Visual Studio インストーラー** と表示されるか、**M** という文字の下に **Microsoft Visual Studio インストーラー** と表示されます。

1. インストーラーの **[製品]** ページで、前にインストールした Visual Studio のエディションを探します。

1. 更新プログラムが使用可能な場合は、 **[更新]** ボタンが表示されます (使用可能な更新プログラムがあるかどうかをインストーラーが判断するために数秒かかる場合があります)。

   **[更新]** ボタンを選択して更新プログラムをインストールします。

     ![Visual Studio インストーラーを使用して Visual Studio 2017 を更新する](media/update-visual-studio.png "Visual Studio インストーラーを使用して Visual Studio を更新する")

::: moniker-end

::: moniker range="vs-2019"

常に最新の機能、修正、改善を利用できるように、Visual Studio の[最新リリース](/visualstudio/releases/2019/release-notes/)に更新することをお勧めします。

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。 現在、別のバージョンの Visual Studio を使用している場合は、[複数バージョンの Visual Studio をインストールする](../install/install-visual-studio-versions-side-by-side.md)か、[以前のバージョンの Visual Studio をアンインストール](../install/uninstall-visual-studio.md)してください。

> [!IMPORTANT]
> Visual Studio をインストール、更新、または変更するには、管理アクセス許可を持つアカウントでログオンする必要があります。 詳細については、「[ユーザー アクセス許可と Visual Studio](../ide/user-permissions-and-visual-studio.md)」を参照してください。
>
> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[Visual Studio for Mac を更新する](/visualstudio/mac/update)」を参照してください。

Visual&nbsp;Studio&nbsp;2019 を更新する方法を次に示します。

## <a name="use-the-visual-studio-installer"></a>Visual Studio インストーラーを使用する

1. コンピューター上の **Visual Studio インストーラー** を見つけます。

   Windows の [スタート] メニューで "installer" を検索できます。

   ![Visual Studio インストーラー](media/vs-2019/visual-studio-installer.png "Visual Studio インストーラーを検索する")

   続行する前に、インストーラーの更新が必要な場合があります。 その場合は、画面の指示に従います。

1. インストーラーで、インストールした Visual Studio のエディションを探します。

   たとえば、以前にインストールした Visual&nbsp;Studio Community&nbsp;2019 に対して更新プログラムが存在する場合は、"**利用可能な更新プログラムがあります**" というメッセージが表示されます。

     ![更新する Visual Studio 2019 のエディションを選択する](media/vs-2019/vs-installer-update-visual-studio-community.png "更新する Visual Studio 2019 のエディションを選択する")

1. **[更新]** を選択して更新プログラムをインストールします。

    ![[更新] ボタンを選択して更新プログラムをインストールする](media/vs-2019/vs-installer-choose-update-visual-studio-community.png "[更新] ボタンを選択して更新プログラムをインストールする")

1. 更新が完了したら、コンピューターの再起動を求められる場合があります。 その場合は、その操作を行い、通常どおり Visual Studio を起動します。

   コンピューターの再起動を求められなかった場合は、**[起動]** を選択してインストーラーから Visual Studio を起動します。

    ![[起動] ボタンを選択して Visual Studio を起動する](media/vs-2019/choose-launch-visual-studio-community.png "[起動] ボタンを選択して Visual Studio を起動する")

## <a name="use-the-ide"></a>IDE を使用する

更新プログラムを確認し、Visual Studio 2019 にあるメニュー バーまたは検索ボックスを使用してインストールできます。

### <a name="open-visual-studio"></a>Visual Studio を開きます

1. Windows の **[スタート]** メニューから、**[Visual Studio 2019]** を選択します。

    ![Visual Studio 2019 を開く](media/vs-2019/vs-installer-visual-studio-2019.png "Windows から Visual Studio 2019 を開く")

1. **[作業の開始]** で、任意のオプションを選択すると、IDE が開きます。

    ![Visual Studio インストーラーを開く](media/vs2019-choose-option-from-get-started.png "Visual Studio インストーラーを開く")

    Visual Studio が開きます。 IDE 内に、**Visual Studio 2019 の更新プログラム** に関するメッセージが表示されます。

    ![IDE 内の "Visual Studio 2019 の更新プログラム" に関するメッセージ](media/vs-2019/update-visual-studio-ide-message.png "IDE 内の &quot;Visual Studio 2019 の更新プログラム&quot; に関するメッセージ")

1. **Visual Studio 2019 の更新プログラム** に関するメッセージで、**[詳細の表示]** を選択します。

   ![Visual Studio 2019 の更新プログラムに関するメッセージで [詳細の表示] を選択する](media/vs-2019/update-visual-studio-ide-view-details.png "Visual Studio 2019 の更新プログラムに関するメッセージで [詳細の表示] ボタンを選択する")

1. **[更新プログラムがダウンロードされてインストールの準備完了]** ダイアログ ボックスで、**[更新]** を選択します。

     ![[更新プログラムがダウンロードされてインストールの準備完了] ダイアログ ボックスで [更新] ボタンを選択する](media/vs-2019/update-ready-install-visual-studio-community-from-ide.png "[更新プログラムがダウンロードされてインストールの準備完了] ダイアログ ボックスで [更新] ボタンを選択する")

   Visual Studio が更新され、閉じられた後に、再起動されます。

### <a name="in-visual-studio"></a>Visual Studio 内

1. メニュー バーから、**[ヘルプ]** を選択して、**[更新プログラムの確認]** を選択します。

     ![[ヘルプ] メニューから [更新プログラムの確認] を選択する](media/vs-2019/vs-ide-check-updates-help-menu.png "[ヘルプ] メニューから [更新プログラムの確認] を選択する")

    > [!NOTE]
    > 更新プログラムを確認するには、IDE にある検索ボックスを使用することもできます。 **Ctrl**+**Q** キーを押し、「更新プログラムの確認」と入力して、一致した検索結果を選択します。

1. **[利用可能な更新プログラムがあります]** ダイアログ ボックスで、**[更新]** を選択します。

     ![[利用可能な更新プログラムがあります] ダイアログ ボックスで [更新] ボタンを選択する](media/vs-2019/update-visual-studio-community-from-ide.png "[利用可能な更新プログラムがあります] ダイアログ ボックスで [更新] ボタンを選択する")

   Visual Studio が更新され、閉じられた後に、再起動されます。

## <a name="use-the-notifications-hub"></a>通知ハブを使用する

1. Visual Studio 内に、作業内容を保存します。

1. Visual Studio IDE の右下隅にある通知アイコンを選択して、**[通知]** ハブを開きます。

   ![Visual Studio IDE の通知アイコン](media/vs-2019/notification-bar.png "Visual Studio IDE の通知アイコン")

1. **[通知] ハブ** では、インストールする更新プログラムを選択して、**[詳細表示]** を選択します。

     ![Visual Studio 2019 の通知ハブ](media/vs-2019/notification-hub-update.png "Visual Studio 2019 の通知ハブ")

      > [!TIP]
      > Visual Studio 2019 のエディションに対する更新プログラムは累積になっているため、常に最新のバージョン番号のものをインストールしてください。

1. **[利用可能な更新プログラムがあります]** ダイアログ ボックスで、**[更新]** を選択します。

   Visual Studio が更新され、閉じられた後に、再起動されます。

## <a name="customize-update-settings"></a>更新設定のカスタマイズ

Visual Studio の更新設定は、いくつかの異なる方法でカスタマイズできます。たとえば、インストール モードの変更や、自動ダウンロードの選択などを行います。

2 つのインストール モードから選択することができます。

* **ダウンロード中にインストールする**
* **全部ダウンロードしてからインストールする**

また、**[Automatically download updates]\(更新プログラムを自動的にダウンロードする\)** 設定を選択することもできます。これを使うと、コンピューターがアイドル状態のときに更新プログラムがダウンロードされます。

その方法は次のとおりです。

1. メニュー バーで **[ツール]** > **[オプション]** の順に選択します。

2. **[環境]** を展開してから、**[製品の更新プログラム]** を選択します。

    ![Visual Studio での更新設定](media/vs-2019/update-settings-options.png)

3. Visual Studio の更新プログラム用に使用したいインストール モードと自動ダウンロード オプションを選択します。

::: moniker-end

::: moniker range=">=vs-2022"

常に最新の機能、修正、改善を利用できるように、Visual Studio の[最新リリース](/visualstudio/releases/2022/release-notes/)に更新することをお勧めします。

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。 現在、別のバージョンの Visual Studio を使用している場合は、[複数バージョンの Visual Studio をインストールする](../install/install-visual-studio-versions-side-by-side.md)か、[以前のバージョンの Visual Studio をアンインストール](../install/uninstall-visual-studio.md)してください。

> [!IMPORTANT]
> Visual Studio をインストール、更新、または変更するには、管理アクセス許可を持つアカウントでログオンする必要があります。 詳細については、「[ユーザー アクセス許可と Visual Studio](../ide/user-permissions-and-visual-studio.md)」を参照してください。
>
> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[Visual Studio for Mac を更新する](/visualstudio/mac/update)」を参照してください。

Visual&nbsp;Studio&nbsp;2022 を更新する方法を次に示します。

## <a name="use-the-visual-studio-installer"></a>Visual Studio インストーラーを使用する

1. コンピューター上の **Visual Studio インストーラー** を見つけます。

   Windows の [スタート] メニューで "installer" を検索できます。

   ![Visual Studio インストーラー](media/vs-2019/visual-studio-installer.png "Visual Studio インストーラーを検索する")

   続行する前に、インストーラーの更新が必要な場合があります。 その場合は、画面の指示に従います。

1. インストーラーで、インストールした Visual Studio のエディションを探します。

   たとえば、以前にインストールした Visual&nbsp;Studio Community&nbsp;2022 に対して更新プログラムが存在する場合は、"**利用可能な更新プログラムがあります**" というメッセージが表示されます。

     ![更新する Visual Studio 2019 のエディションを選択する](media/vs-2019/vs-installer-update-visual-studio-community.png "更新する Visual Studio 2019 のエディションを選択する")

1. **[更新]** を選択して更新プログラムをインストールします。

    ![[更新] ボタンを選択して更新プログラムをインストールする](media/vs-2019/vs-installer-choose-update-visual-studio-community.png "[更新] ボタンを選択して更新プログラムをインストールする")

1. 更新が完了したら、コンピューターの再起動を求められる場合があります。 その場合は、その操作を行い、通常どおり Visual Studio を起動します。

   コンピューターの再起動を求められなかった場合は、**[起動]** を選択してインストーラーから Visual Studio を起動します。

    ![[起動] ボタンを選択して Visual Studio を起動する](media/vs-2019/choose-launch-visual-studio-community.png "[起動] ボタンを選択して Visual Studio を起動する")

## <a name="use-the-ide"></a>IDE を使用する

更新プログラムを確認し、Visual Studio 2022 にあるメニュー バーまたは検索ボックスを使用してインストールできます。

### <a name="open-visual-studio"></a>Visual Studio を開きます

1. Windows の **[スタート]** メニューから、 **[Visual Studio 2022]** を選択します。

    ![Visual Studio 2022 を開きます。](media/vs-2019/vs-installer-visual-studio-2019.png "Windows から Visual Studio 2019 を開く")

1. **[作業の開始]** で、任意のオプションを選択すると、IDE が開きます。

    ![Visual Studio インストーラーを開く](media/vs2019-choose-option-from-get-started.png "Visual Studio インストーラーを開く")

    Visual Studio が開きます。 IDE 内に、**Visual Studio 2022 の更新プログラム** に関するメッセージが表示されます。

    ![IDE 内の "Visual Studio 2019 の更新プログラム" に関するメッセージ](media/vs-2019/update-visual-studio-ide-message.png "IDE 内の &quot;Visual Studio 2019 の更新プログラム&quot; に関するメッセージ")

1. **Visual Studio 2022 の更新プログラム** に関するメッセージで、 **[詳細の表示]** を選択します。

   ![Visual Studio 2019 の更新プログラムに関するメッセージで [詳細の表示] を選択する](media/vs-2019/update-visual-studio-ide-view-details.png "Visual Studio 2019 の更新プログラムに関するメッセージで [詳細の表示] ボタンを選択する")

1. **[更新プログラムがダウンロードされてインストールの準備完了]** ダイアログ ボックスで、**[更新]** を選択します。

     ![[更新プログラムがダウンロードされてインストールの準備完了] ダイアログ ボックスで [更新] ボタンを選択する](media/vs-2019/update-ready-install-visual-studio-community-from-ide.png "[更新プログラムがダウンロードされてインストールの準備完了] ダイアログ ボックスで [更新] ボタンを選択する")

   Visual Studio が更新され、閉じられた後に、再起動されます。

### <a name="in-visual-studio"></a>Visual Studio 内

1. メニュー バーから、**[ヘルプ]** を選択して、**[更新プログラムの確認]** を選択します。

     ![[ヘルプ] メニューから [更新プログラムの確認] を選択する](media/vs-2019/vs-ide-check-updates-help-menu.png "[ヘルプ] メニューから [更新プログラムの確認] を選択する")

    > [!NOTE]
    > 更新プログラムを確認するには、IDE にある検索ボックスを使用することもできます。 **Ctrl**+**Q** キーを押し、「更新プログラムの確認」と入力して、一致した検索結果を選択します。

1. **[利用可能な更新プログラムがあります]** ダイアログ ボックスで、**[更新]** を選択します。

     ![[利用可能な更新プログラムがあります] ダイアログ ボックスで [更新] ボタンを選択する](media/vs-2019/update-visual-studio-community-from-ide.png "[利用可能な更新プログラムがあります] ダイアログ ボックスで [更新] ボタンを選択する")

   Visual Studio が更新され、閉じられた後に、再起動されます。

## <a name="use-the-notifications-hub"></a>通知ハブを使用する

1. Visual Studio 内に、作業内容を保存します。

1. Visual Studio IDE の右下隅にある通知アイコンを選択して、**[通知]** ハブを開きます。

   ![Visual Studio IDE の通知アイコン](media/vs-2019/notification-bar.png "Visual Studio IDE の通知アイコン")

1. **[通知] ハブ** では、インストールする更新プログラムを選択して、**[詳細表示]** を選択します。

     ![Visual Studio 2019 の通知ハブ](media/vs-2019/notification-hub-update.png "Visual Studio 2019 の通知ハブ")

      > [!TIP]
      > Visual Studio 2022 のエディションに対する更新プログラムは累積になっているため、常に最新のバージョン番号のものをインストールしてください。

1. **[利用可能な更新プログラムがあります]** ダイアログ ボックスで、**[更新]** を選択します。

   Visual Studio が更新され、閉じられた後に、再起動されます。

## <a name="customize-update-settings"></a>更新設定のカスタマイズ

Visual Studio の更新設定は、いくつかの異なる方法でカスタマイズできます。たとえば、インストール モードの変更や、自動ダウンロードの選択などを行います。

2 つのインストール モードから選択することができます。

* **ダウンロード中にインストールする**
* **全部ダウンロードしてからインストールする**

また、**[Automatically download updates]\(更新プログラムを自動的にダウンロードする\)** 設定を選択することもできます。これを使うと、コンピューターがアイドル状態のときに更新プログラムがダウンロードされます。

その方法は次のとおりです。

1. メニュー バーで **[ツール]** > **[オプション]** の順に選択します。

2. **[環境]** を展開してから、**[製品の更新プログラム]** を選択します。

    ![Visual Studio での更新設定](media/vs-2019/update-settings-options.png)

3. Visual Studio の更新プログラム用に使用したいインストール モードと自動ダウンロード オプションを選択します。
::: moniker-end

## <a name="administrator-updates"></a>管理者の更新

ソフトウェア インストールの管理を一元化している組織に属している場合、お使いのコンピューターでの更新をエンタープライズ管理者が Visual Studio に指示できます。 お使いのコンピューターで受け取れる更新プログラムの種類を制御または構成する方法については、「[Configuration Manager を使用して Visual Studio 更新プログラムを展開する](../install/applying-administrator-updates.md#using-configuration-manager-to-deploy-visual-studio-updates)」を参照してください。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [複数バージョンの Visual Studio をインストールする](install-visual-studio-versions-side-by-side.md)
* [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
* [Visual Studio 企業向けガイド](visual-studio-enterprise-guide.md)
* [サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)
* [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio の変更](modify-visual-studio.md)
* [Visual Studio のアンインストール](uninstall-visual-studio.md)
