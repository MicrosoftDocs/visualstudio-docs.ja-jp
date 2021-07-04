---
title: IDE 定数 | Microsoft Docs
description: VSConstants クラスは、これまでヘッダー ファイルでのみ定義されていた IDE に固有の定数をサポートします。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- IDE, errors
- logical views
- errors [Visual Studio], IDE
- UI context constants
- constants, Visual Studio IDE
- IDE, constants
- physical views
ms.assetid: 5030e70a-241d-474a-ba8c-e3b1cf947ff0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 802de0fd29d909320040667f972de422595bdd4f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904969"
---
# <a name="ide-constants"></a>IDE 定数

<xref:Microsoft.VisualStudio.VSConstants> クラスは、これまでヘッダー ファイルでのみ定義されていた統合開発環境 (IDE) に固有の定数をサポートします。

## <a name="logical-and-physical-views"></a>論理ビューと物理ビュー

|値|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` ハンドラーで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドにこの値を渡すと、 **[プログラムから開く]** ダイアログ ボックス (この場合、選択可能なコード ビュー) が取得されます。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` ハンドラーで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドにこの値を渡すと、 **[プログラムから開く]** ダイアログ ボックス (この場合、<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid> と同じビューにマップされる選択可能な <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid> デバッグ ビューが表示される) が取得されます。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Designer_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` ハンドラーで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドにこの値を渡すと、 **[プログラムから開く]** ダイアログ ボックス (この場合、 **[フォームの表示]** デザイナー ビュー) が取得されます。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Primary_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` ハンドラーで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドにこの値を渡すと、 **[プログラムから開く]** ダイアログ ボックス (この場合、エディター ファクトリのデフォルト ビューとプライマリ ビュー) が取得されます。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.TextView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` ハンドラーで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドにこの値を渡すと、 **[プログラムから開く]** ダイアログ ボックス (この場合、ドキュメントまたはデータ テキスト エディター ビュー用) が取得されます。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.UserChooseView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` ハンドラーで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドにこの値を渡すと、使用するユーザー定義ビューを選択するようにユーザーにダイアログが表示されます。|

## <a name="editor-factory-flags"></a>エディター ファクトリ フラグ

|値|説明|
|-----------|-----------------|
|[CEF.CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> メソッドの最初のパラメーターとしてビットごとに結合される古いフラグ。|
|[CEF.OpenAsNew](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenAsNew>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> メソッドの最初のパラメーターとしてビットごとに結合され、エディター ファクトリが必要な修正を実行する必要のあることを示します。|
|[CEF.OpenFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenFile>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> メソッドの最初のパラメーターとしてビットごとに結合されます。このフラグは、[CEF.CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>) とは同時に指定できません。|
|[CEF.Silent](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_Silent>)|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> メソッドの最初のパラメーターとしてビットごとに結合され、エディター ファクトリがユーザー インターフェイス (UI) を表示せずにエディターを作成する必要があることを示します。|

## <a name="visual-studio-errors"></a>Visual Studio のエラー

|値|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|対象のオブジェクトが既にビジー状態である場合に、インターフェイスによって非同期動作に返される定数|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|"互換性のないドキュメント データ" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|"パッケージが読み込まれていません" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|"プロジェクトは既に存在します" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|"プロジェクトの構成に失敗しました" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|"プロジェクトが読み込まれていません" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|"ソリューションは既に開いています" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|"ソリューションが開いていません" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput> インターフェイスから配列を指定するためのパラメーターを持つビルド インターフェイスによって返されますが、実装によって、すべての出力にメソッドを適用することしかできません。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|ドキュメントの形式がエディターで開けない場合、<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> メソッドでこの値が返されます。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|ユーザーが Visual Studio ウィザードの [戻る] ボタンを押したことを示す HRESULT 値。|

## <a name="visual-studio-constants"></a>Visual Studio の定数

|値|説明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|"プロジェクトが転送されました" を示す Visual Studio に固有のエラー HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|"ツールボックス マーカー" を示す Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|モダリティの開始を示す <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> メソッドを介して通知メッセージをブロードキャストする Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|モダリティの終了を示す <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> メソッドを介して通知メッセージをブロードキャストする Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|コマンド バーのメトリックが変更されたを示す <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> メソッドを介して通知メッセージをブロードキャストする Visual Studio に固有の定数。|
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|Cookie が設定されていないことを示す Visual Studio に固有の定数。|
|[VSITEMID.Nil](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|プロジェクト項目が存在しないことを表す Visual Studio 項目識別子。 この値は、現在選択されているものがない場合に使用されます。|
|[VSITEMID.Root](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|プロジェクト階層のルートを表す Visual Studio 項目識別子。単一の項目ではなく、階層全体を識別するために使用されます。|
|[VSITEMID.Selection](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|現在選択されている項目 (階層のルートを含むことができる) を表す Visual Studio の項目識別子。|

## <a name="ivsselectionevents"></a>IVsSelectionEvents
 たとえば、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> の呼び出しなどで、IDE のどのコンポーネントが選択されたかを表します。

|定数|値|
|--------------|-----------|
|[SelectionElement.DocumentFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[SelectionElement.PropertyBrowserSID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[SelectionElement.StartupProject](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[SelectionElement.UndoManager](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[SelectionElement.UserContext](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0x5|
|[SelectionElement.WindowFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1|

## <a name="vsselelemid"></a>VSSELELEMID
 新しい選択状態を示すために使用される定数。

|定数|値|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|2|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|7|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|4|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|6|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|3|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|0|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|5|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|1|

## <a name="component-selector-dialog-constants"></a>コンポーネント セレクター ダイアログ定数

|定数|値|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELCHANGED>|WM_USER + 1280|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELDBLCLICK>|WM_USER + 1281|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_CLEARSELECTION>|WM_USER + 1290|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_GETSELECTION>|WM_USER + 1287|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZELIST>|WM_USER + 1285|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZETAB>|WM_USER + 1288|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_QUERYCANSELECT>|WM_USER + 1286|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_SETMULTISELECT>|WM_USER + 1289|

## <a name="see-also"></a>こちらもご覧ください

- [プロジェクト システムを拡張するための IDE 定義コマンド](../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
