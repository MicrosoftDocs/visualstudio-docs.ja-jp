---
title: 設定を同期する
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: a3d2ea29-be5d-4012-9820-44b06adbb7dd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ff663a7d2a22f152b3a0b9081623766535f9a53
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "57869045"
---
# <a name="synchronize-visual-studio-settings-across-multiple-computers"></a>複数のコンピューター間で Visual Studio 設定を同期する

複数のコンピューターで同じ個人アカウントを使用して Visual Studio にサインインした場合、コンピューター間で設定が同期されます。

## <a name="synchronized-settings"></a>同期された設定

既定では、次の設定が同期されます。

- 開発設定。 Visual Studio を初めて実行するときに一連の設定を選択しますが、選択内容はいつでも変更できます。 詳細については、[環境設定](../ide/environment-settings.md)に関するページを参照してください。

- ユーザー定義のコマンド エイリアス。 コマンド エイリアスを定義する方法について詳しくは、「[Visual Studio コマンドの定義済みのエイリアス](../ide/reference/visual-studio-command-aliases.md)」をご覧ください。

- **[ウィンドウ]** > **[ウィンドウ レイアウトの管理]** ページのユーザー定義のウィンドウ レイアウト。

- **[ツール]** > **[オプション]** ページの次のオプション。

   - **[環境]** > **[全般]** オプション ページの [テーマ] とメニュー バー枠の設定。

   - **[環境]** > **[フォントおよび色]** オプション ページのすべての設定。

   - **[環境]** > **[キーボード]** オプション ページのすべてのキーボード ショートカット。

   - **[環境]** > **[タブとウィンドウ]** オプション ページのすべての設定。

   - **[環境]** > **[スタートアップ]** オプション ページのすべての設定。

   - **テキスト エディター**のオプション ページでのすべての設定。[コード スタイルのユーザー設定](code-styles-and-quick-actions.md)など。

   - **[XAML デザイナー]** オプション ページのすべての設定。

## <a name="turn-off-synchronized-settings-on-a-particular-computer"></a>特定のコンピューター上の同期された設定の無効化

Visual Studio の同期された設定は、既定でオンになっています。 あるコンピューター上の同期された設定をオフにするには、**[ツール]** > **[オプション]** > **[環境]** > **[アカウント]** ページに移動して、**[Visual Studio にサインインしたときにデバイス間の設定を同期する]** チェック ボックスをオフにします。

たとえば、コンピューター "A" 上の Visual Studio の設定を同期しないようにすると、コンピューター "A" で行った設定変更がコンピューター "B" やコンピューター "C" に表示されなくなります。 コンピューター "B" と "C" は、引き続き相互に同期しますが、コンピューター "A" とは同期しなくなります。

> [!NOTE]
> **[ツール]** > **[オプション]** > **[環境]** > **[アカウント]** ページのオプションをオフにすることによって設定を同期しないことを選択した場合、同じコンピューター上にある Visual Studio の他のバージョンまたはエディションには影響ありません。 Visual Studio のこれらのサイド バイ サイド インストールでは、(そこにあるオプションもオフにしない限り) 引き続きそれらの設定が同期されます。

## <a name="synchronize-settings-across-visual-studio-family-products-and-editions"></a>Visual Studio ファミリ製品およびエディション間での設定の同期

設定は、"*サイド バイ サイド*" でインストールされている Visual Studio のバージョンおよびエディション間で同期されます。 設定は、Blend for Visual Studio を含む Visual Studio ファミリ製品の間でも同期されます。 ただし、個々のファミリ製品には Visual Studio で共有されない独自の設定が含まれる場合があります。 たとえば、コンピューター "A" 上の Blend for Visual Studio に固有の設定は、コンピューター "A" または "B" 上の Visual Studio とは共有されません。

## <a name="side-by-side-synchronized-settings"></a>サイド バイ サイドで同期された設定

::: moniker range="vs-2017"

Visual Studio の異なるサイド バイ サイド インストールの間では、ツール ウィンドウ レイアウトなどの一部の設定は共有されません。 *%userprofile%\Documents\Visual Studio 2017\Settings* の *CurrentSettings.vssettings* ファイルはインストール固有フォルダーに置かれています。このフォルダーは、*%localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx\Settings* のようなフォルダーになります。

> [!NOTE]
> 新しいインストール固有設定を使用するには、新しくインストールを行います。 既存の Visual Studio インストールをアップグレードすると、既存の共有の場所が使用されます。

現在、Visual Studio がサイド バイ サイド インストールされているとき、新しいインストール固有設定ファイル用フォルダーを使用する場合、次の手順に従ってください。

1. Visual Studio 2017 バージョン 15.3 以降にアップグレードします。

2. **設定のインポート/エクスポート** ウィザードを利用し、すべての既存設定を *%localappdata%\Microsoft\VisualStudio\15.0_xxxxxxxx* フォルダーから別の場所にエクスポートします。

3. **[開発者コマンド プロンプト for VS 2017]** を開き、`devenv /resetuserdata` を実行します。

1. Visual Studio を開き、エクスポートした設定ファイルから保存済みの設定をインポートします。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio の異なるサイド バイ サイド インストールの間では、ツール ウィンドウ レイアウトなどの一部の設定は共有されません。 *%userprofile%\Documents\Visual Studio 2019\Settings* の *CurrentSettings.vssettings* ファイルはインストール固有フォルダーに置かれています。このフォルダーは、*%localappdata%\Microsoft\VisualStudio\16.0_xxxxxxxx\Settings* のようなフォルダーになります。

::: moniker-end

## <a name="see-also"></a>関連項目

- [IDE をカスタマイズする](../ide/personalizing-the-visual-studio-ide.md)
- [環境設定](../ide/environment-settings.md)
- [[環境] - [アカウント] ([オプション] ダイアログ ボックス)](reference/accounts-environment-options-dialog-box.md)
