---
title: Visual Studio メニューの GUID および ID | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) に含まれている Visual Studio メニュー バー上にあるメニューとグループの GUID と ID の値の一覧について紹介します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio menus
- visual studio groups
- id
- existing menus
- guid
- menus
ms.assetid: 84639d86-dd21-4b35-9988-6bb654162488
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d9f5066c5ae5c9fa57517406b8eca388747979c4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082089"
---
# <a name="guids-and-ids-of-visual-studio-menus"></a>Visual Studio メニューの GUID および ID
この記事では、Visual Studio メニュー バーのメニューとグループの GUID と ID の値の一覧を紹介します。 これらの値は、Visual Studio SDK の一部としてインストールされる *.vsct* ファイルで定義されています。 詳細については、「[IDE 定義コマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

 *.vsct* ファイルに定義されている統合開発環境 (IDE) オブジェクトを使用する方法の詳細については、「[メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 Visual Studio メニュー バー上のメニューとグループには、GUID `guidSHLMainMenu` が使用されています。 メニュー バー自体の ID は `IDM_VS_TOOL_MAINMENU` です。

## <a name="groups-on-the-visual-studio-menu-bar"></a>Visual Studio メニュー バー上のグループ
 メニュー バーにメニューを追加するには、これらのグループのいずれかを親として設定します。

|グループ|ID|
|-----------|--------|
|ファイル、編集、表示|IDG_VS_MM_FILEEDITVIEW|
|リファクタリング|IDG_VS_MM_REFACTORING:|
|Project|IDG_VS_MM_PROJECT|
|ビルド|IDG_VS_MM_BUILDDEBUGRUN|
|書式設定、ツール|IDG_VS_MM_TOOLSADDINS|
|ウィンドウ、ヘルプ、コミュニティ|IDG_VS_MM_WINDOWHELP|
|Addins|IDG_VS_MM_MACROS|
|FullScreenBar|IDG_VS_MM_FULLSCREENBAR|

## <a name="menus-on-the-visual-studio-menu-bar"></a>Visual Studio メニュー バー上のメニュー
 既存の Visual Studio メニューにグループを追加するには、次のメニューのいずれかを親として設定します。 サブメニューはこの一覧に含まれていません。

|メニュー|id|
|----------|--------|
|ファイル|IDM_VS_MENU_FILE|
|編集|IDM_VS_MENU_EDIT|
|View|IDM_VS_MENU_VIEW|
|リファクター|IDM_VS_MENU_REFACTORING|
|Project|IDM_VS_MENU_PROJECT|
|ビルド|IDM_VS_MENU_BUILD|
|フォーマット|IDM_VS_MENU_FORMAT|
|ツール|IDM_VS_MENU_TOOLS|
|の拡張|IDM_VS_MENU_EXTENSIONS|
|ウィンドウ|IDM_VS_MENU_WINDOW|
|Addins|IDM_VS_MENU_ADDINS|
|コミュニティ|IDM_VS_MENU_COMMUNITY|
|ヘルプ|IDM_VS_MENU_HELP|

## <a name="groups-on-visual-studio-menus"></a>Visual Studio メニュー上のグループ
 次の一覧は、Visual Studio メニュー バー上のメニューから直接派生したグループです。 Visual Studio メニューにコマンドを追加する最も簡単な方法は、これらのグループのいずれかを親として設定することです。 サブメニューから派生したグループは、このセクションには表示されません。

### <a name="file-menu-groups"></a>[ファイル] メニュー グループ

|グループ|ID|
|-----------|--------|
|新規、開く|IDG_VS_FILE_FILE|
|追加|IDG_VS_FILE_ADD|
|ソリューション|IDG_VS_FILE_SOLUTION|
|その他|IDG_VS_FILE_MISC|
|保存|IDG_VS_FILE_SAVE|
|名前の変更|IDG_VS_FILE_RENAME|
|Browser|IDG_VS_FILE_BROWSER|
|印刷|IDG_VS_FILE_PRINT|
|[直前に使用]|IDG_VS_FILE_MRU|
|詳細ビュー|IDG_VS_FILE_MOVE|
|終了|IDG_VS_FILE_EXIT|

### <a name="edit-menu-groups"></a>[編集] メニュー グループ

|グループ|ID|
|-----------|--------|
|元に戻す/やり直し|IDG_VS_EDIT_UNDOREDO|
|切り取り、コピー、貼り付け|IDG_VS_EDIT_CUTCOPY|
|選択|IDG_VS_EDIT_SELECT|
|GoTo|IDG_VS_EDIT_GOTO|
|Find|IDG_VS_EDIT_FIND|
|オブジェクト|IDG_VS_EDIT_OBJECTS|
|OLE 動詞|IDG_VS_EDIT_OLEVERBS|
|コマンド ウェル|IDG_VS_EDIT_COMMANDWELL|

### <a name="refactor-menu-groups"></a>[リファクター] メニュー グループ

|グループ|ID|
|-----------|--------|
|共通|IDG_REFACTORING_COMMON|
|詳細設定|IDG_REFACTORING_ADVANCED|

### <a name="view-menu-groups"></a>[表示] メニュー グループ

|グループ|ID|
|-----------|--------|
|フォーム コード|IDG_VS_VIEW_FORMCODE|
|Browser|IDG_VS_VIEW_BROWSER|
|ビューの定義|IDG_VS_VIEW_DEFINEVIEWS|
|Windows|IDG_VS_VIEW_WINDOWS|
|設計ウィンドウ|IDG_VS_VIEW_ARCH_WINDOWS|
|組織ウィンドウ|IDG_VS_VIEW_ORG_WINDOWS|
|コード ブラウザー|IDG_VS_VIEW_CODEBROWSENAV_WINDOWS|
|開発ウィンドウ|IDG_VS_VIEW_DEV_WINDOWS|
|ツールバー|IDG_VS_VIEW_TOOLBARS|
|記号|IDG_VS_VIEW_SYMBOLNAVIGATE|
|Navigate|IDG_VS_VIEW_NAVIGATE|
|小さいナビゲート|IDG_VS_VIEW_SMALLNAVIGATE|
|オブジェクト ブラウザー|IDG_VS_VIEW_OBJBRWSR|
|コマンド ウェル|IDG_VS_VIEW_COMMANDWELL|
|[プロパティ ページ]|IDG_VS_VIEW_PROPPAGES|
|更新|IDG_VS_VIEW_REFRESH|

### <a name="project-menu-groups"></a>[プロジェクト] メニュー グループ

|グループ|ID|
|-----------|--------|
|その他の追加|IDG_VS_PROJ_MISCADD|
|追加|IDG_VS_PROJ_ADD|
|Folder|IDG_VS_PROJ_FOLDER|
|アンロード、再読み込み|IDG_VS_PROJ_UNLOADRELOAD|
|リファレンス|IDG_VS_PROJ_REFERENCE|
|オプション|IDG_VS_PROJ_OPTIONS|
|Settings|IDG_VS_PROJ_SETTINGS|

### <a name="build-menu-groups"></a>[ビルド] メニュー グループ

|グループ|ID|
|-----------|--------|
|ソリューション|IDG_VS_BUILD_SOLUTION|
|選択|IDG_VS_BUILD_SELECTION|
|ガイド付き最適化のプロファイル|IDG_VS_PGO_SELECTION|
|その他|IDG_VS_BUILD_MISC|
|キャンセル|IDG_VS_BUILD_CANCEL|

### <a name="tools-menu-groups"></a>[ツール] メニュー グループ

|グループ|ID|
|-----------|--------|
|コマンド ライン|IDG_VS_TOOLS_CMDLINE|
|スニペット|IDG_VS_TOOLS_SNIPPETS|
|オブジェクト サブセット|IDG_VS_TOOLS_OBJSUBSET|
|オプション|IDG_VS_TOOLS_OPTIONS|
|その他 2|IDG_VS_TOOLS_OTHER2|
|[外部ツール]|IDG_VS_TOOLS_EXT_TOOLS|
|外部のカスタマイズ|IDG_VS_TOOLS_EXT_CUST|

### <a name="window-menu-groups"></a>[ウィンドウ] メニュー グループ

|グループ|ID|
|-----------|--------|
|新規|IDG_VS_WINDOW_NEW|
|ドック、閉じる|IDG_VS_DOCKCLOSE|
|Dock/Hide|IDG_VS_DOCKHIDE|
|整列|IDG_VS_WINDOW_ARRANGE|
|ナビゲーション|IDG_VS_WINDOW_NAVIGATION|
|List|IDG_VS_WINDOW_LIST|

### <a name="help-menu-groups"></a>[ヘルプ] メニュー グループ

|グループ|ID|
|-----------|--------|
|サンプル|IDG_VS_HELP_SAMPLES|
|サポート|IDG_VS_HELP_SUPPORT|
|詳細|IDG_VS_HELP_ABOUT|

## <a name="submenus-of-visual-studio-menus"></a>Visual Studio メニューのサブメニュー
 次の階層は、Visual Studio メニュー バーのメニューに関連付けられているサブメニューを示しています。 メニューを親として持つことができるのはグループのみであるため、すべてのサブメニューは、メニューから直接ではなく、メニュー上のグループから派生する必要があります。 メニュー、グループ、サブメニューの関係の詳細については、「[メニューにサブメニューを追加する](../../extensibility/adding-a-submenu-to-a-menu.md)」を参照してください。

> [!NOTE]
> Visual Studio メニュー バー上のメニューの名前は、*IDG_VS_\<Menu Name\>_\<Group Name\>* のように IDE のグループの名前付け規則から推測できるため、この階層には個別に表示されません。

|[親グループ]|サブメニュー|子グループ|
|------------------|-------------|------------------|
|IDG_VS_FILE_FILE|IDM_VS_CSCD_NEW|IDG_VS_FILE_NEW_CASCADE|
||IDM_VS_CSCD_OPEN|IDG_VS_FILE_OPENP_CASCADE|
|||IDG_VS_FILE_OPENF_CASCADE|
|IDG_VS_FILE_ADD|IDM_VS_CSCD_ADD|IDG_VS_FILE_ADD_PROJECT_NEW|
|||IDG_VS_FILE_ADD_PROJECT_EXI|
|IDG_VS_FILE_MRU|IDM_VS_CSCD_FILEMRU|IDG_VS_FILE_FMRU_CASCADE|
||IDM_VS_CSCD_PROJMRU|IDG_VS_FILE_PMRU_CASCADE|
|IDG_VS_FILE_MOVE|IDM_VS_CSCD_MOVETOPRJ|IDG_VS_FILE_MOVE_CASCADE|
|||IDG_VS_FILE_MOVE_PICKER|
|IDG_VS_VIEW_DEV_WINDOWS|IDM_VS_CSCD_FINDRESULTS|IDG_VS_WNDO_FINDRESULTS|
||IDM_VS_CSCD_WINDOWS|IDG_VS_VIEW_CALLBROWSER|
|||IDG_VS_WNDO_OTRWNDWS1...6|
|||IDG_VS_WNDO_WINDOWS2|
|IDG_VS_VIEW_TOOLBARS|IDM_VS_CSCD_COMMANDBARS||
|IDG_VS_EDIT_GOTO|IDM_VS_EDITOR_FIND_MENU||
|IDG_VS_EDIT_OBJECTS|IDM_VS_CSCD_MNUDES|IDG_VS_MNUDES_INSERT|
|||IDG_VS_MNUDES_EDITNAMES|
||IDM_VS_CSCD_OLEVERBS|IDG_VS_EDIT_OLEVERBS|
|IDG_VS_BUILD_SELECTION|IDM_VS_CSCD_BUILD|IDG_VS_BUILD_CASCADE|
|||IDG_VS_BUILD_PROJPICKER|
||IDM_VS_CSCD_REBUILD|IDG_VS_REBUILD_CASCADE|
|||IDG_VS_REBUILD_PROJPICKER|
||IDM_VS_CSCD_PROJONLY|IDG_VS_PROJONLY_CASCADE|
||IDM_VS_CSCD_CLEAN|IDG_VS_CLEAN_CASCADE|
|||IDG_VS_CLEAN_PROJPICKER|
||IDM_VS_CSCD_DEPLOY|IDG_VS_DEPLOY_CASCADE|
|||IDG_VS_DEPLOY_PROJPICKER|
|IDG_VS_PGO_SELECTION|IDM_VS_CSCD_PGO_BUILD|IDG_VS_PGO_BUILD_CASCADE_BUILD|
|||IDG_VS_PGO_BUILD_CASCADE_RUN|

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio ツール バーの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)
- [Visual Studio コマンドの GUID および ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
