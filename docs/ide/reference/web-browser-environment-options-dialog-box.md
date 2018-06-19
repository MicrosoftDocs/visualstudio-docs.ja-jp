---
title: '[Web ブラウザー] ([オプション] ダイアログ ボックス - [環境])'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.Environment.Web Browser
- VS.ToolsOptionsPages.Environment.WebBrowser
- VS.ToolsOptionsPag.Environment.Web_Browser
- VS.ToolsOptionsPages.Environment.Web_Browser
helpviewer_keywords:
- browsers, customizing
- searching, search page for Web browser
- Visual Studio Start page, default URL
- Web browsers, customizing
- searches, default Web browser search page
- URLs, specifying VS home page
- home page
- Options dialog box, Web settings
- Internet Explorer, setting options
ms.assetid: 586db4eb-032d-4cb5-93a6-a7c14de1ae49
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c6f8dc8fb781e75116dbdcb6e316981225f32439
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31947119"
---
# <a name="web-browser-environment-options-dialog-box"></a>[Web ブラウザー] ([オプション] ダイアログ ボックス - [環境])
内部 Web ブラウザーと Internet Explorer のオプションを設定します。 このダイアログ ボックスにアクセスするには、**[ツール]** メニューの **[オプション]** をクリックし、**[環境]** フォルダーを展開して **[Web ブラウザー]** を選択します。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)」を参照してください。


> [!IMPORTANT]
> Web の特定のファイルまたはコンポーネントを開いて、コンピューター上のコードを実行できます。


## <a name="home-page"></a>ホーム ページ
 IDE Web ブラウザーを開いたときに表示されるページを設定します。

## <a name="search-page"></a>[検索] ページ
 内部 Web ブラウザーの [検索] ページを指定できます。 この場所には、統合開発環境 (IDE) 以外で開始された Internet Explorer のインスタンスが使用する検索ページとは別のページを指定できます。

## <a name="view-source-in"></a>ソース表示の選択
 内部 Web ブラウザーからページの **[ソースの表示]** を選択するときに Web ページを開くために使用するエディターを設定します。

-   **ソース エディター** 選択すると、[エディター](../../ide/writing-code-in-the-code-and-text-editor.md)にソースが表示されます。

-   **HTML エディター** 選択すると、[HTML デザイナー](http://msdn.microsoft.com/Library/640043cc-3657-4677-a091-bc315e636477)にソースが表示されます。 この場合、デザイン ビューまたは標準のテキストベースのソース ビューで Web ページを編集します。

-   **外部エディター** 選択すると、別のエディターにソースが表示されます。 選択するエディター (Notepad.exe など) のパスを指定します。

## <a name="internet-explorer-options"></a>Internet Explorer オプション
クリックして、**[インターネットのプロパティ]** ダイアログ ボックスで Internet Explorer のオプションを変更します。 このダイアログ ボックスの変更内容は、内部 Web ブラウザーと、Visual Studio IDE 以外 (たとえば、[スタート] メニュー) で開始された Internet Explorer のインスタンスの両方に影響があります。

> [!NOTE]
> **[ブラウザーの選択]** ダイアログ ボックスを使用して、Visual Studio の内部 Web ブラウザーを任意のブラウザーに置き換えます。 [ブラウザーの選択] ダイアログ ボックスにアクセスするには、プロジェクト内の HTML ファイルなどを右クリックして、コンテキスト メニューからアクセスできます。


## <a name="see-also"></a>関連項目

- [[環境] ([オプション] ダイアログ ボックス)](../../ide/reference/environment-options-dialog-box.md)
- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
- [HTML デザイナー](http://msdn.microsoft.com/Library/640043cc-3657-4677-a091-bc315e636477)