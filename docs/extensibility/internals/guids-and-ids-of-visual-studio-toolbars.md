---
title: Visual Studio ツール バーの GUID および ID | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) に含まれているツール バーおよびそれらに含まれるグループの、GUID と ID の値の一覧を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- visual studio groups
- toolbars
- visual studio toolbar
- id
- toolgar group
- tool window toolbar
- guid
ms.assetid: c9cacd57-9225-450f-a9ac-cbf3168ea844
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d2ba6c92a2913ec63a59751a4181454aa67fa67
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898111"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>Visual Studio ツール バーの GUID および ID
このトピックでは、Visual Studio 統合開発環境 (IDE) に含まれているツール バーおよびそれらに含まれるグループの、GUID と ID の値について説明します。 これらの値は、Visual Studio SDK の一部としてインストールされる *.vsct* ファイルで定義されています。 詳細については、「[IDE 定義コマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

> [!NOTE]
> Visual Studio で使用できるツール バーの多くは、Visual Studio では定義されていません。また、それらの GUID と ID の値はパブリックではありません。 このトピックでは、Visual Studio SDK の *.vsct* ファイルで定義されているツール バーのみを示します。

 *.vsct* ファイルで定義されている IDE オブジェクトを操作する方法の詳細については、「[メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 Visual Studio IDE で提供されている既定のツール バーでは、`GUID:ID` 構文で特に指定されている場合を除き、GUID `guidSHLMainMenu` が使用されます。

## <a name="ide-toolbars"></a>IDE ツール バー
 Visual Studio IDE では、次のツール バーが提供されています。 ツール バーを表示するには、 **[ツール]** メニューの **[ツール バー]** サブメニューで選択します。 ツール ウィンドウのツール バーは、このセクションには含まれていません。

 ツール バーの直接の子になることができるのはグループだけです。 グループを追加するには、その親としてツール バーの GUID と ID を設定します。 ツール バーにボタンを追加するには、その親としてツール バー上のグループを設定します。

|ツール バー|id|
|-------------|--------|
|Standard|IDM_VS_TOOL_STANDARD|
|ビルド|IDM_VS_TOOL_BUILD|
|テキスト エディター|IDM_VS_TOOL_TEXTEDITOR|
|デバッグ|guidVSDebugGroup:IDM_DEBUG_TOOLBAR|
|デバッグの場所|guidVSDebugGroup:IDM_DEBUG_CONTEXT_TOOLBAR|

### <a name="special-toolbars"></a>特殊なツール バー
 これらのツール バーは、Visual Studio IDE で定義されていますが、特化された機能を提供します。また、コマンド グループをホストしません。

|ツール バー|id|
|-------------|--------|
|Add コマンド|IDM_VS_TOOL_ADDCOMMAND|
|未定義。|IDM_VS_TOOL_UNDEFINED|
|XML スキーマ|IDM_VS_TOOL_SCHEMA|
|XML データ|IDM_VS_TOOL_DATA|

## <a name="groups-on-the-ide-toolbars"></a>IDE ツール バーのグループ
 標準ツール バーにボタンを追加するには、その親として次のいずれかのグループを設定します。 グループは、親ツール バーによって並べ替えられます。

### <a name="standard-toolbar-groups"></a>標準ツール バーのグループ

|名前|id|
|----------|--------|
|保存/開く|IDG_VS_TOOLSB_SAVEOPEN|
|切り取り/コピー|IDG_VS_TOOLSB_CUTCOPY|
|元に戻す/やり直し|IDG_VS_TOOLSB_UNDOREDO|
|実行/ビルド|IDG_VS_TOOLSB_RUNBUILD|
|検索|IDG_VS_TOOLSB_SEARCH|
|Windows|IDG_VS_TOOLSB_WINDOWS|
|新しいウィンドウ|IDG_VS_TOOLSB_NEWWINDOWS|
|読み込み/保存|IDG_VS_WINDOWUI_LOADSAVE|
|ゲージ|IDG_VS_TOOLSB_GAUGE|

### <a name="build-toolbar-groups"></a>[ビルド] ツール バーのグループ

|名前|id|
|----------|--------|
|ビルド バー|IDG_VS_BUILDBAR|
|キャンセル|IDG_VS_BUILD_CANCEL|

### <a name="text-editor-toolbar-groups"></a>[テキスト エディター] ツール バーのグループ

|名前|id|
|----------|--------|
|Completion|IDM_VS_TOOL_TEXTEDITOR|
|インデントする|IDG_VS_EDITTOOLBAR_INDENT|
|コメント|IDG_VS_EDITTOOLBAR_COMMENT|
|ブックマーク|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|

### <a name="debug-toolbar-groups"></a>[デバッグ] ツール バーのグループ

|名前|id|
|----------|--------|
|実行|IDM_DEBUG_TOOLBAR|
|ステップ実行|IDG_DEBUG_TOOLBAR_STEPPING|
|Watch|IDG_DEBUG_TOOLBAR_WATCH|
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|

### <a name="debug-location-toolbar-groups"></a>[デバッグの場所] ツール バーのグループ

|名前|id|
|----------|--------|
|デバッグの場所|IDG_DEBUG_CONTEXT_TOOLBAR|

## <a name="tool-window-toolbars"></a>ツール ウィンドウのツール バー
 ツール バーは、IDE に直接表示されるか、**ソリューション エクスプローラー** のようなツール ウィンドウに表示されます。 ツール ウィンドウは *.vsct* ファイルでは定義されていないため、ツール ウィンドウのツール バーには定義された親がありません。 代わりに、コード内に記述されます。 IDE のツール ウィンドウに表示されるツール バーと、それらに含まれるコマンド グループを次の表に示します。

> [!NOTE]
> ツール バーとグループでは、GUID:ID 構文で特に指定されている場合を除き、GUID `guidSHLMainMenu` が使用されます。 ツール バーに対して GUID が指定されている場合は、そのツール バーの子であるグループにも適用されます。

|ツール ウィンドウ|ツール バー|グループ|
|-----------------|-------------|------------|
|ソリューション エクスプローラー|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1..5|
|[サーバー エクスプローラー]|guid_SE_MenuGroup:IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|
|プロパティ|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|
|クラス ビュー|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|
|クラス ビュー|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|
|オブジェクト ブラウザー|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|
|オブジェクト ブラウザー|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|
|出力|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|
|検索と置換|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|
|検索結果 1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|
|検索結果 2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|
|スニペット|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|
|ブックマーク|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|
|タスク一覧|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|
|ユーザー タスク|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|
|エラー一覧|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|
|呼び出しブラウザー|IDM_VS_TOOL_CALLBROWSER1..16|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|
|ブレークポイント|guidVSDebugGroup:IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|
|逆アセンブリ|guidVSDebugGroup:IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|
|メモリ 1-4|guidVSDebugGroup:IDM_MEMORY_WINDOW_TOOLBAR1...4|IDG_MEMORY_EXPRESSION1..4<br /><br /> IDG_MEMORY_COLUMNS1..4|
|処理|guidVSDebugGroup:IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRL IDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|

## <a name="see-also"></a>関連項目
- [ツール バーにメニュー コントローラーを追加する](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)
- [ツール ウィンドウにツール バーを追加する](../../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [Visual Studio メニューの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)
