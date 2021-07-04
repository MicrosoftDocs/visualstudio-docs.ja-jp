---
title: 使用可能なサービスの一覧 | Microsoft Docs
description: 各サービスのインターフェイスを取得するためのサービス GUID を含む、Visual Studio と Visual Studio SDK でサポートされている使用可能なサービスの一覧を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- services, Visual Studio
- Visual Studio, services
ms.assetid: 724eb24b-b87c-4971-a2e7-adee7afc03b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f5ba7fdfd7d86ef9158554d30acdd2995c98e5ec
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899941"
---
# <a name="list-of-available-services"></a>使用可能なサービスの一覧

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] と Visual Studio SDK では、次のサービスがサポートされています。 パッケージの中には、ここには一覧表示されていない独自のサービスを提供している場合があります。たとえば、言語サービスには 1 つもサービス GUID がありません。 レジストリで言語サービスの GUID を検索するには、言語の名前を使用する必要があります。

ここに一覧表示されているサービス GUID か、他の何らかのソース (言語サービスなど) から取得したサービス GUID を使用して、プライマリ インターフェイスまたは各サービスで表示されるインターフェイスを取得します。

## <a name="the-services"></a>サービス

| サービス | インターフェイス | Visual Studio | Visual Studio 2005 | 説明 |
| - | - |---------------|--------------------| - |
| <xref:Microsoft.VisualStudio.OLE.Interop.SBindHost> | <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> | はい | はい | ActiveX コントロールから <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> インターフェイスを取得して、非同期データ転送を容易にするために VSPackage で使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDTE> | <xref:EnvDTE.DTE> | いいえ | はい | オートメーションに使用されるデザイン時拡張機能 (DTE) オブジェクトを取得します。<br /><br /> C/C++ ID: SID_SDTE |
| <xref:Microsoft.VisualStudio.Shell.Interop.SCodeNavigate> | <xref:Microsoft.VisualStudio.Shell.Interop.ICodeNavigate> | はい | はい | コントロールの既定のイベント ハンドラーを表示するためにフォーム デザイナーによって実装されます。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SContainerDispatch> | IDispatch | はい | はい | VSPackage から別の VSPackage またはコントロールのオートメーション インターフェイスにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SExtendedTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IExtendedTypeLib> | はい | はい | 拡張タイプ ライブラリの追加または作成を VSPackage で行えるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDirList> | <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> | いいえ | はい | リストのコンテナーの名前付き一覧にアクセスできるようにします。たとえば、 **[検索対象]** ドロップダウン リストの **[検索と置換]** ダイアログ ボックスに示されているような、検索するディレクトリの一覧です。 <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> オブジェクトから読み取ることも、そこに書き込むこともできます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SIVsPackageDynamicToolOwner> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwner> | はい | はい | VSPackage で独自のツール ウィンドウの表示と非表示を動的に切り替えられるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLicensedClassManager> | <xref:Microsoft.VisualStudio.Shell.Interop.ILicensedClassManager> | はい | はい | VSPackage で、ライセンス キーの一覧を指定して、必要とするクラスを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に示すことができるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> | はい | はい | ローカルの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] レジストリ ハイブに対して相対的なレジストリに VSPackage からアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleComponentManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager> | はい | はい | メッセージ ループ、キーボード ループ、イベント通知などのコンポーネント調整サービスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> | はい | はい | ヘルプ、ステータス バー、UI イベントなど、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のさまざまなユーザー インターフェイス (UI) 要素に、VSPackage からアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponent> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> | はい | はい | VSPackage でその UI を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の UI と統合できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponentSite> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentSite> | はい | はい | ツールに固有の UI の変更を VSPackage で制御できるようにします。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleUndoManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> | はい | はい | コンテナーのアンドゥ マネージャーに VSPackage からアクセスして、そのコンテナーの元に戻すスタックに参加するか、そのコンテナーの元に戻すスタックにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> | はい | はい | VSPackage で独自のサービスを提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferTypeLib> | はい | はい | フォーム デザイナーでタイプ ライブラリを参照に使用できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> | はい | はい | 選択コンテナー内の選択肢にアクセスできるようにします。 フォーム デザイナーで使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostCommandDispatcher> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> | はい | はい | VSPackage で、コマンド ハンドラー チェーンに参加し、統合開発環境 (IDE) またはそれ自体のためにコマンドを処理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostLocale> | <xref:Microsoft.VisualStudio.Shell.Interop.IUIHostLocale> | はい | はい | ホストの UI ロケール情報にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> | いいえ | はい | ログ記録を有効にしているときに、VSPackage で高レベルのメッセージを記録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg> | はい | はい | **[プロジェクト項目の追加]** ダイアログ ボックスにアクセスできるようにし、VSPackage による独自の **[項目の追加]** メニュー オプションの実装を許可します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg> | はい | はい | **[参照の追加]** ダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> | はい | はい | コマンドライン スイッチが devenv.exe に与えられたかどうかを VSPackage で判断できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCallBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCallBrowser> | いいえ | はい | デバッグ中に使用する新しい **呼び出しブラウザー** を VSPackage で作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsClassView> | はい | はい | VSPackage で **クラス ビュー** を特定のオブジェクトに同期できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCmdNameMapping> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCmdNameMapping> | はい | はい | コマンド名の GUID へのマップと、使用可能なすべてのコマンドと名前の特定をサポートします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeDefView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeDefView> | いいえ | はい | VSPackage で **コード定義ビュー** を操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeShareHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeShareHandler> | はい | はい | 内部サービス。 使用しないでください。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindow> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> | はい | はい | 1 つ以上のドキュメントを含められるコード ウィンドウにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindowManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> | はい | はい | ドロップダウン バーなどのコード ウィンドウに VSPackage で変更を加えられるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow2> | はい | はい | VSPackage で、**コマンド ウィンドウ** からコマンドを実行し、それ以外の場合は **コマンド ウィンドウ** と対話できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindowsCollection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindowsCollection> | いいえ | はい | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で保持される **コマンド** ウィンドウの一覧を VSPackage で操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComplusLibrary> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibraryReferenceManager> | はい | はい | VSPackage から **オブジェクト ブラウザー** にブラウザー情報を提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg> | いいえ | はい | VSPackage で **[参照の追加]** オプションをサポートできるようにします。これにより、ユーザーはプロジェクトに追加する外部コンポーネントを選択できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg2> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg2> | いいえ | はい | VSPackage で **[参照の追加]** オプションをサポートできるようにします。これにより、ユーザーはプロジェクトに追加する外部コンポーネントを選択できます。 このバージョンのダイアログ ボックスを使用すると、コンポーネントの一覧は表示される前に事前に入力されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsConfigurationManagerDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsConfigurationManagerDlg> | いいえ | はい | **[構成マネージャー]** ダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject> | いいえ | はい | VSPackage で他のプロジェクトのコレクションを含むプロジェクトを作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebuggableProtocol> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProtocol> | はい | はい | 特定のデバッグ エンジンを起動するために IDE で使用されるデバッグ可能なプロトコルの一覧を VSPackage で更新できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebugLaunch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugLaunch> | はい | はい | デバッガーの起動を VSPackage でサポートできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDiscoveryService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService> | はい | はい | Web サービスの検出に使用される検出セッションを VSPackage で作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsEnumHierarchyItemsFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> | はい | はい | 指定された階層 (プロジェクト) にわたって列挙に使用される <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> オブジェクトを作成するファクトリを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsErrorList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsErrorList> | いいえ | はい | **[ビルド エラー一覧]** タスク ウィンドウを操作するための追加のメソッドを提供します。 特に、 **[ビルド エラー一覧]** タスク ウィンドウを最前面に移動して、すべてのエラーを強制的に表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager> | はい | はい | 現在のソリューションの **[その他のファイル]** プロジェクト ノードにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChange> | | はい | はい | 互換性のために残されています。 代わりに `SVsFileChangeEx` サービスを使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> | はい | はい | IDE によってトリガーされるさまざまなファイル変更イベントに、VSPackage からアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> | はい | はい | **[項目の追加]** ダイアログ ボックスに表示する項目を VSPackage でフィルター処理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterKeys> | はい | はい | 高度なキーボード フィルター処理を VSPackage で実行できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorCacheManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> | いいえ | はい | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でのフォントと色に関するキャッシュのセットにアクセスして、特定のキャッシュまたはすべてのキャッシュを更新または消去できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorStorage> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities> | はい | はい | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で保持されるフォントおよび色の設定を、VSPackage で操作できるようにします。 さらに、このサービスは、フォントおよび色データを操作するためのユーティリティ メソッドのコレクションにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> | はい | はい | 一般的な **[出力ウィンドウ]** ペインにアクセスできるようにし、必要な場合は作成します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHelpService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHelpSystem> | はい | はい | ヘルプ システムにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHTMLConverter> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHTMLConverter> | はい | はい | 出力の書式を設定するように HTML を処理するために [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーで使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIME> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIME> | はい | はい | VSPackage 内から入力方式エディター (IME) API にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntegratedHelp> | <xref:Microsoft.VisualStudio.VSHelp.SVsHelp> | はい | はい | ヘルプ ファイルを通じてナビゲーション コントロールとともにキーワードや URL が得られるように、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ヘルプ システムにアクセスできるようにします。 このサービスは、ヘルプが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE に統合され、外部プログラムとして実行していない場合にのみ利用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntelliMouseHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntelliMouseHandler> | はい | はい | VSPackage からマウス ホイールの使用やスクロールの操作などの IntelliMouse 機能にアクセスし、マウス ホイールがクリックされたときにビットマップをパンできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseEngine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseEngine> | いいえ | はい | IntelliSense 操作のサポートの一環として、プロジェクト階層ノードで、ファイルをロードまたはアンロードできるようにします。 ロードおよびアンロードのプロセスによって、プロジェクトに関する IntelliSense ツールヒントに表示される内容に影響する可能性のあるイベントがトリガーされます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectHost> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectHost> | いいえ | はい | IntelliSense ツールヒントに表示できる (<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> インターフェイスを実装する) 入れ子になった IntelliSense プロジェクトに関する情報を、プロジェクト階層ノードで提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectManager> | いいえ | はい | IntelliSense ツールヒントに表示される内容に影響を与える可能性のある、参照や構成における変更などのイベントについて、プロジェクト階層ノードでリスナーに通知できるようにします。 含まれる言語で使用されるように設計されています。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsInvisibleEditorManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> | はい | はい | "不可視" エディター、つまり完全な編集機能を提供するが、ユーザーには表示されないエディターを VSPackage で登録できるようにします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLanguageFilter> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> | はい | はい | VSPackage で、データ ヒントや単語の範囲などの追加情報をテキスト ビューに表示できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPad> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> | はい | はい | VSPackage で、一時バッチ スクリプトを実行し、出力が出力ウィンドウに送信されるコマンドライン プログラムを実行し、エラー ウィンドウに送信される標準の警告およびエラー メッセージを解析できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPadFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPadFactory> | はい | はい | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> オブジェクトを作成するためのファクトリを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLinkedUndoTransactionManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> | はい | はい | リンクされたアンドゥ マネージャーにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMenuEditor> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditorFactory> | はい | はい | フォーム デザイナーから共有メニュー エディターにアクセスできるようにします。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditor> について IVsMenuEditorFactory に照会できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> | はい | はい | VSPackage で、"コンテキスト バッグ" を作成できるようにします。これは、特定のコンテキストに関するヘルプ キーワードを関連付けるために使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjBrowser> | はい | はい | VSPackage から **オブジェクト ブラウザー** 内の特定のオブジェクトに移動できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager> | はい | はい | VSPackage で、名前空間、クラス、列挙型などのオブジェクトを管理するために、ライブラリ マネージャーを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectSearch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectSearch> | はい | はい | VSPackage で特定のオブジェクトを検索できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOpenProjectOrSolutionDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOpenProjectOrSolutionDlg> | いいえ | はい | VSPackage で、標準の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ダイアログ ボックスを使用して、プロジェクトまたはソリューションを開くことができるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> | はい | はい | VSPackage で、一般的な [出力] ウィンドウに追加の出力ウィンドウを作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsParseCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsParseCommandLine> | はい | はい | コマンド行を解析するために、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスの実装を有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPathVariableResolver> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPathVariableResolver> | いいえ | はい | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に固有で、最終パスを生成するためにパスに埋め込まれている変数を解決する方法を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPreviewChangesService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPreviewChangesService> | いいえ | はい | コードのリファクタリングで使用される **[変更のプレビュー]** ダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfileDataManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfileDataManager> | いいえ | はい | 設定データをインポートおよびエクスポートし、現在のユーザーのプロファイル設定の UI を表示できるようにする [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のプロファイル マネージャーにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfilesManagerUI> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfilesManagerUI> | いいえ | はい | 現在のユーザーのプロファイル設定を示したダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPropertyPageFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPageFrame> | はい | はい | **[プロパティ]** ウィンドウに最初に表示されるプロパティ ページを VSPackage でオーバーライドできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | いいえ | はい | ファイルがメモリ内で変更される、または保存されるところであることをソース管理プロバイダーに通知するために VSPackage で使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterDebugTargetProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectDebugTargetProvider> | いいえ | はい | VSPackage プロジェクトで、起動するターゲットをデバッガー内でプログラムを使用してオーバーライドできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> | はい | はい | VSPackage で、エディター ファクトリを IDE に登録できるようにします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsRegisterFindScope> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsRegisterFindScope> | いいえ | はい | **[フォルダーを指定して検索]** ダイアログ ボックスの検索スコープを VSPackage で登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterPriorityCommandTarget> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> | はい | はい | VSPackage を優先度の高いコマンド ハンドラーとして登録できるようにします。これにより VSPackage ですべてのコマンドを表示できます。 使用するとしても控えめに使用してください。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes> | はい | はい | VSPackage で、プロジェクト タイプを IDE に登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceManager> | いいえ | はい | VSPackage で、サテライト DLL からマネージド リソースとアンマネージド リソースを読み込めるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceView> | はい | はい | 代わりに <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> サービスを使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> | はい | はい | 現在開いているすべてのドキュメントを追跡する IDE の実行中のドキュメント テーブル (RDT) にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | いいえ | はい | ソース管理に参加できるように、ソース管理プロバイダーに VSPackage を登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | はい | はい | VSPackage で、ソース管理プロバイダー オプションを取得して設定できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSettingsReader> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> | いいえ | はい | ユーザーのプロファイル設定に読み取りアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell> | はい | はい | VSPackage で他の VSPackage と直接やり取りし、操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger> | はい | はい | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> | はい | はい | VSPackage から現在の選択にアクセスし、コマンド UI コンテキストを管理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDCodeDomProvider> | IVSMDCodeDomProvider | いいえ | はい | ネイティブ コードで使用できるコード ドキュメント オブジェクト モデル (DOM) プロバイダーにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDDesignerService> | IVSMDCodeDomCreator<br /><br /> IVSMDDesignerService | いいえ | はい | マネージド フォーム デザイナーに対する IDE のサポートにアクセスできるようにします。 コード DOM プロバイダーの作成に `IVSMDCodeDomCreator` を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDPropertyBrowser> | IVSMDPropertyBrowser | いいえ | はい | デザイナープロパティ Windows サービスにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDTypeResolutionService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVSMDTypeResolutionService> | いいえ | はい | ネイティブ コードで使用できる <xref:System.ComponentModel.Design.ITypeResolutionService> オブジェクトを返すことのできるインターフェイスにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSmartOpenScope> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSmartOpenScope> | いいえ | はい | 必要に応じてロックを考慮しながら、アセンブリでスコープを開く方法を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | はい | はい | 現在のソリューションへの最上位レベルのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager> | はい | はい | VSPackage で、ソリューションのビルド プロセスを操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionObject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | はい | はい | 代わりに <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> サービスを使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionPersistence> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> | はい | はい | VSPackage で、現在のソリューションの .sln ファイルから情報を取得し格納できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSQLCLRReferences> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSQLCLRReferences> | いいえ | はい | マネージド コード アセンブリで参照を追加および更新する機能を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStartPageDownload> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStartPageDownload> | いいえ | はい | バックグラウンド スレッドでダウンロード サービスを起動および停止させるために、Visual Studio 2017 スタート ページのダウンロード サービスにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> | はい | はい | IDE のステータス バーにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStrongNameKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStrongNameKeys> | いいえ | はい | マネージド コード アセンブリの署名に使用されるパスワードを使用して厳密なキー名とキー ファイルを作成するためのメソッドにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStructuredFileIO> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStructuredFileIO> | はい | はい | 複数の形式によるデータの保存を、VSPackage でサポートできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> | はい | はい | IDE の [タスク一覧] ウィンドウにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextImageUtilities> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextImageUtilities> | いいえ | はい | テキスト ファイルを読み込み、保存するためのユーティリティを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> | はい | はい | IDE で使用できるすべてのテキスト バッファーおよび非表示のテキスト セッション (非表示領域用) にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTextOut> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTextOut> | はい | はい | デバイス コンテキスト (DC ハンドルが必要) にテキストを書き込むための Win32 `TextOut` 関数のバージョンを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextSpanSet> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextSpanSet> | はい | はい | テキスト イメージまたはバッファー内のテキスト範囲の一覧にアクセスできるようにします。 このサービスは、通常、ドキュメントのコンテナー上に実装され、現在のドキュメントを参照します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadedWaitDialog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadedWaitDialog> | いいえ | はい | 別のスレッド上で待機するダイアログ ボックス (バックグラウンド タスクの待機に使用) を VSPackage で表示できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadPool> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadPool> | いいえ | はい | その後 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって保持されるバックグラウンド タスクを VSPackage で開始できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> | はい | はい | IDE の **ツールボックス** にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxActiveXDataProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProvider> | はい | はい | VSPackage で **ツールボックス** の項目から情報を取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxDataProviderRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProviderRegistry> | いいえ | はい | VSPackage で、**ツールボックス** 全体を事前に読み込んでパフォーマンスを低下させずに、ツールボックス データ プロバイダーを登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolsOptions> | いいえ | はい | VSPackage で、 **[オプション]** ダイアログ ボックスが開いているかどうかを判断し、すべてのオプションのページの表示を更新できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | いいえ | はい | VSPackage で、プロジェクトのファイルでの変更を監視し、ソース管理プロバイダーに対するバッチ制御を提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> | はい | はい | VSPackage で、現在選択されているプロジェクト項目に影響する可能性のある選択に対する変更について、IDE に通知できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelper> | はい | はい | クリップボードの使用を階層 (プロジェクト VSPackage など) 間で調整できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> | はい | はい | ツール ウィンドウやドキュメント ウィンドウなどの IDE の UI 要素にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellDocumentWindowMgr> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellDocumentWindowMgr> | はい | はい | VSPackage で、データ ストリームの内容に基づいて、すべてのウィンドウの位置を復元したり、すべてのウィンドウの位置をストリームに保存したりできるようにします。 めったに使用されません。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> | はい | はい | VSPackage で、多数の方法でドキュメントを開き、誰がどのドキュメントを所有しているかを特定できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> | いいえ | はい | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> インターフェイスの実装でエラーおよび情報メッセージを報告するために使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebBrowsingService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebBrowsingService> | はい | はい | VSPackage で、Web ブラウジング セッションを作成し制御できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebFavorites> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebFavorites> | はい | はい | VSPackage でユーザーの **[お気に入り]** リストに追加できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebPreview> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebPreview> | はい | はい | VSPackage で、Web ページを通常は子ウィンドウでプレビューできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebURLMRU> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebURLMRU> | はい | はい | VSPackage で、最近使用した (MRU) URL の一覧に URL を追加し、MRU の一覧内のすべての URL の一覧を取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWindowFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> | はい | はい | VSPackage で、パッケージまたはパッケージの一部を配置できるウィンドウ フレームを取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsXMLMemberIndexService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsXMLMemberIndexService> | はい | はい | 特定のメタデータ ファイルに関連付けられた XML 形式のドキュメント ファイルにアクセスできるようにします。 |

## <a name="see-also"></a>関連項目

- [サービスの使用と提供](../../extensibility/using-and-providing-services.md)
