---
title: プロジェクト モデルのコア コンポーネント | Microsoft Docs
description: この記事では、プロジェクト モデル コアで識別されるインターフェイスおよびサービスと、オブジェクトに関連付けられたインターフェイスおよびサービスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project models, objects and interfaces
- project models, services
ms.assetid: b2f572d3-b26d-4846-92d1-84055fac141a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ae01d149611afe5bf75a6952f19baff7d70f6210
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062812"
---
# <a name="project-model-core-components"></a>プロジェクト モデルのコア コンポーネント
次の表は、プロジェクト モデルについて詳しく記しています。 この表では、モデルで識別されるインターフェイスおよびサービスと、特定のオブジェクトに関連付けられているインターフェイスおよびサービスについて簡単に説明します。 また、表には、特定のプロジェクト タイプの要件に応じて、プロジェクトの作成とメンテナンスでオプションとなる他のインターフェイスの詳細も示されます。

 詳細については、「[シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)」を参照してください。

### <a name="package-object"></a>パッケージ オブジェクト

|インターフェイス|コメント|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|IDE で VSPackage を初期化し、そのサービスを IDE で使用できるようにします。|

### <a name="project-factory-object"></a>プロジェクト ファクトリ オブジェクト

|インターフェイス|コメント|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|新しいプロジェクトの作成と、既存のプロジェクトの開始を管理します。|

### <a name="project-objects"></a>プロジェクト オブジェクト

|インターフェイス|コメント|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|プロジェクト項目の追加と削除を管理し、エディターを開き、各ドキュメント モニカーと `VSITEMID` の間のマッピングを維持します。 `IVsProject` と `IVsProject2` から継承されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|ナビゲーションと表示のプロパティを管理し、イベントを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|ソリューション エクスプローラーにフォーカスがある場合にのみ適用される切り取りや名前の変更などのコマンドに対して、`IOleCommandTarget` のものに似たコマンドの実行を有効にします。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|プロジェクト階層の主要なコマンド ターゲット インターフェイスとして機能します。 これは、コマンドのステータスまたは状態のオブジェクトのクエリを実行し、コマンドを実行するための標準インターフェイスです。 プロジェクト ウィンドウでフォーカスされていない場合に使用できます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|プロジェクトの状態の永続性を調整します。 通常、プロジェクトの状態はプロジェクト ファイルとして保存されますが、ファイルベースではないストレージ システムに適応させることができます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|ディスク上のファイルまたは他のストレージ システムのオブジェクトのどちらかとして、プロジェクト項目の永続化のすべての側面をプロジェクトで管理できるようにします。 `IVsPersistHierarchyItem2` インターフェイスは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> インターフェイスを実装しない項目に使用されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|ソース コード管理との相互作用を調整します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|プロジェクトで構成情報を管理できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|デバッグ/リリース構成など、プロジェクト構成オブジェクトを管理します。 ビルド、デプロイ、デバッグの各操作は、プロジェクト構成オブジェクトを使用して調整されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|階層項目の削除 (破壊) オプションまたは除去 (非破壊的) オプションを制御するために、階層によって実装されます。 `IVsHierarchy` インターフェイスから `IVsHierarchyDeleteHandler` インターフェイスでのクエリ インターフェイスを呼び出し ます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|`IVsHierarchy` インターフェイスを実装するプロジェクト オブジェクトとは異なる COM ID で `IVsCfgProvider2` インターフェイスをサポートするオブジェクトを持つというオプションを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|他の開発者がプロジェクトを拡張できるようにするために実装された省略可能なインターフェイス。 `IVsProjectStartupServices` インターフェイスを使用すると、プロジェクトが読み込まれるたびに、サードパーティのサービス GUID をプロジェクト ファイルに読み込んで、その GUID に対して `QueryService` を呼び出せるように、サードパーティの VSPackage で、プロジェクト ファイルに保存する GUID を登録できます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|切り取り、コピー、貼り付けなどのクリップボード操作を調整するために、`UIHierarchy` ウィンドウでソース階層によって実装されます。 クリップボード イベントを登録するには、`AdviseClipboardHelperEvents` インターフェイスを使用します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|UI 階層ウィンドウでのドラッグ アンド ドロップ操作中に、データ ソースに対して相対的な、ドラッグされた項目に関する情報を提供します。 `IVsHierarchy` インターフェイスから呼び出されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|UI 階層ウィンドウでのドラッグ アンド ドロップ操作中に、ドロップ ターゲットに対して相対的な、ドラッグされた項目に関する情報を提供します。 `IVsHierarchy` インターフェイスから呼び出されます。|

### <a name="configuration-object"></a>構成オブジェクト

|インターフェイス|コメント|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|構成に関する情報を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|プロジェクトで構成情報を管理できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|デバッガーの制御下でプロジェクトを実行できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|他のプロジェクトのデプロイ操作を実行するデプロイ プロジェクトによって実装されます。|

### <a name="configuration-builder-object"></a>構成ビルダー オブジェクト

|インターフェイス|コメント|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|プロジェクト構成のビルド操作を管理します。|

### <a name="additional-project-objects"></a>追加のプロジェクト オブジェクト

|インターフェイス|コメント|
|----------------|--------------|
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|**[プロパティ]** ウィンドウに項目のプロパティを表示します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|デプロイの出力を表示します。|

 次の表に、プロジェクトモデルで識別されるサービスの簡単な説明を示します。

### <a name="services"></a>サービス

|サービス|コメント|
|-------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|プロジェクト タイプを実装して、存在するプロジェクト ファクトリを IDE に登録する VSPackage で使用されます。 VSPackage では、このサービスに対して `QueryService` を呼び出し、`IVsPackage::SetSite` メソッドが呼び出されたときにプロジェクト ファクトリを登録する必要があります。 `SetSite` メソッドが呼び出されない場合、プロジェクトのインスタンスは作成されません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|プロジェクトの列挙、新しいプロジェクトの作成、プロジェクトの変更への注目など、現在のソリューションに関する IDE 内部に組み込まれている概念にアクセスできるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|ソース管理に参加させるプロジェクトで呼び出されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|開いているドキュメントのテーブルを保持し、1 つ以上のプロジェクト項目が既に開かれているかどうかを判断します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|標準エディターまたは特定のエディターを使用して、プロジェクト項目を実際に開くために呼び出されるインターフェイスとメソッドが含まれます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|項目を追加、削除、または名前変更するときに、すべてのプロジェクトで呼び出される必要があります。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|ファイルまたはディレクトリへの変更を管理し、選択したファイルがディスク上で変更されたときにクライアントに通知します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|項目をダーティにしたり保存したりする前に、すべてのプロジェクトとエディターで呼び出される必要があります。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|プロジェクト構成のビルドおよびデプロイ操作の順序を管理します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|ほとんどのデバッグ コントロールに使用される低レベルのデバッガー サービスへのアクセスを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|現在の選択に関する情報に VSpackage でアクセスできるようにし、 **[プロパティ]** ウィンドウと通信できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|ツール ウィンドウまたはドキュメント ウィンドウを作成および列挙する機能やユーザーにエラーを報告する機能など、UI に関連する基本的な IDE 機能を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|IDE のステータス バーへのアクセスを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|オートメーション モデルを実装するために使用されます。 プロジェクト モデルでは、そのオブジェクトのインスタンスを作成できるようにするプロパティ オブジェクトを返します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|階層内のプロジェクト オブジェクトにクリップボード イベントを実装するために使用されます。 `SVsUIHierWinClipboardHelper` を使用すると、切り取り、コピー、貼り付けの各操作を正しく処理できます。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [ビルド内にありません: HierUtil7 プロジェクト クラスを使用したプロジェクトの種類の実装 (C++)](/previous-versions/bb166212(v=vs.100))
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)