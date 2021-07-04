---
title: プロジェクト サブタイプの設計 | Microsoft Docs
description: プロジェクト サブタイプを使用し、Microsoft Build Engine (MSBuild) に基づいて VSPackage によってプロジェクトを拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c04c8e681646aed6816c645defe7ffd87ac7033c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899694"
---
# <a name="project-subtypes-design"></a>プロジェクト サブタイプのデザイン

プロジェクト サブタイプを使用すると、Microsoft Build Engine (MSBuild) に基づいて VSPackage によってプロジェクトを拡張することができます。 集計を使用すると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に実装されているコア マネージド プロジェクト システムの大部分を再利用しながら、特定のシナリオに合わせて動作をカスタマイズできます。

 以下のトピックでは、プロジェクト サブタイプの基本的な設計と実装について詳しく説明します。

- プロジェクト サブタイプの設計。

- 複数レベルの集計。

- サポート インターフェイス。

## <a name="project-subtype-design"></a>プロジェクト サブタイプの設計

プロジェクト サブタイプの初期化は、メインの <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> の各オブジェクトを集計することで実現されます。 この集計を使用すると、プロジェクト サブタイプにより、ベース プロジェクトのほとんどの機能をオーバーライドしたり、拡張したりすることができます。 プロジェクト サブタイプにより、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> を使用するプロパティ、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> を使用するコマンド、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> を使用するプロジェクト項目管理を初めて処理できるようになります。 また、プロジェクト サブタイプを使用して、以下を拡張することもできます。

- プロジェクト構成オブジェクト。

- 構成に依存するオブジェクト。

- 構成に依存しない参照オブジェクト。

- プロジェクト オートメーション オブジェクト。

- プロジェクト オートメーションのプロパティ コレクション。

プロジェクト サブタイプによる拡張性の詳細については、「[プロジェクト サブタイプによって拡張されるプロパティとメソッド](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)」を参照してください。

### <a name="policy-files"></a>ポリシー ファイル

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境には、ポリシー ファイルの実装でプロジェクト サブタイプを使用してベース プロジェクト システムを拡張する例が用意されています。 ポリシー ファイルを使用すると、ソリューション エクスプローラー、 **[プロジェクトの追加]** ダイアログ ボックス、 **[新しい項目の追加]** ダイアログ ボックス、 **[プロパティ]** ダイアログ ボックスなどの機能を管理して、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境を整えることができます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>、`IOleCommandTarget`、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> の実装を通じて、ポリシー サブタイプにより、これらの機能はオーバーライドおよび拡張されます。

### <a name="aggregation-mechanism"></a>集計メカニズム

この環境のプロジェクト サブタイプ集計メカニズムは、複数レベルの集計をサポートしているため、フレーバー プロジェクトにさらにフレーバーを付けることで、高度なサブタイプを実装できます。 また、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> などのプロジェクト サブタイプのサポート オブジェクトは、複数レベルの階層化を許可するように設計されています。 COM と COM の集計規則の制約に従って、プロジェクト サブタイプとベース プロジェクトを協調的にプログラムして、内部サブタイプまたはベース プロジェクトがメソッド呼び出しの委任と参照カウントの管理に適切に参加できるようにする必要があります。 つまり、集計対象のプロジェクトは、集計をサポートするようにプログラムする必要があります。

次の図は、複数レベルのプロジェクト サブタイプ集計の概略図です。

![Visual Studio マルチレベル projectflavor グラフィック](../../extensibility/internals/media/vs_multilevelprojectflavor.gif)

複数レベルのプロジェクト サブタイプ集計は、3 つのレベルで構成されます。ベース プロジェクトは、プロジェクト サブタイプごとに集計され、さらに高度なプロジェクト サブタイプによって集計されます。 この図では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクト サブタイプ アーキテクチャの一部として用意されているサポート インターフェイスの一部に焦点を当てています。

### <a name="deployment-mechanisms"></a>展開メカニズム

プロジェクト サブタイプによって拡張される多くのベース プロジェクト システム機能の中に、展開メカニズムがあります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> に対して QueryInterface を呼び出すことで取得される構成インターフェイス (<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> や <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> など) を実装することにより、プロジェクト サブタイプは展開メカニズムに影響します。 プロジェクト サブタイプと高度なプロジェクト サブタイプの両方によって、異なる構成実装が追加されるシナリオの場合、ベース プロジェクトから、高度なプロジェクト サブタイプの `IUnknown` に対して `QueryInterface` が呼び出されます。 ベース プロジェクトから要求されている構成実装が内側のプロジェクト サブタイプに含まれている場合、高度なプロジェクト サブタイプから、内側のプロジェクト サブタイプに用意されている実装に委任されます。 異なる集計レベル間で状態を保持されるメカニズムとして、すべてのレベルのプロジェクト サブタイプに <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> を実装し、ビルドに関係ない XML データをプロジェクト ファイルに保持します。 詳細については、「[MSBuild プロジェクト ファイルでのデータの保持](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)」を参照してください。 <xref:EnvDTE80.IInternalExtenderProvider> は、プロジェクト サブタイプからオートメーション エクステンダーを取得するメカニズムとして実装されています。

次の図は、オートメーション エクステンダーの実装、その中でも特に、ベース プロジェクト システムを拡張するためにプロジェクト サブタイプによって使用されるプロジェクト構成参照オブジェクトに焦点を当てています。

![VS プロジェクト フレーバー オート エクステンダー グラフィック](../../extensibility/internals/media/vs_projectflavorautoextender.gif)

プロジェクト サブタイプを使用して、オートメーション オブジェクト モデルを拡張することにより、ベース プロジェクト システムをさらに拡張できます。 これらは DTE オートメーション オブジェクトの一部として定義され、Project オブジェクト、`ProjectItem` オブジェクト、`Configuration` オブジェクトを拡張するために使用されます。 詳細については、「[ベース プロジェクトのオブジェクト モデルの拡張](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)」を参照してください。

## <a name="multi-level-aggregation"></a>複数レベルの集計

下位レベルのプロジェクト サブタイプをラップするプロジェクト サブタイプの実装は、内部のプロジェクト サブタイプが適切に機能するように協調的にプログラムする必要があります。 プログラミングの役割の一覧は次のとおりです。

- 内側のサブタイプをラップしているプロジェクト サブタイプの <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> の実装は、<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> の両メソッドについて、内側のプロジェクト サブタイプの <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> の実装に委任する必要があります。

- ラッパー プロジェクト サブタイプの <xref:EnvDTE80.IInternalExtenderProvider> の実装は、その内側のプロジェクト サブタイプの実装に委任する必要があります。 特に、<xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A> の実装の場合、内側のプロジェクト サブタイプから名前の文字列を取得してから、エクステンダーとして追加する文字列を連結する必要があります。

- ラッパー プロジェクト サブタイプの <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> の実装の場合、内側のプロジェクト サブタイプの <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> オブジェクトのインスタンスを作成し、プライベート デリゲートとして保持する必要があります。これは、ラッパー プロジェクト サブタイプの構成オブジェクトの存在を直接認識しているのは、ベース プロジェクトのプロジェクト構成オブジェクトのみだからです。 外側のプロジェクト サブタイプにより、まず直接処理する構成インターフェイスが選択され、残りは内側のプロジェクト サブタイプの <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A> の実装に委任されます。

## <a name="supporting-interfaces"></a>サポート インターフェイス

ベース プロジェクトにより、プロジェクト サブタイプから追加されたサポート インターフェイスへの呼び出しが委任され、その実装のさまざまな側面が拡張されます。 これには、プロジェクト構成オブジェクトとさまざまなプロパティ ブラウザー オブジェクトの拡張が含まれます。 これらのインターフェイスを取得するには、最も外側にあるプロジェクト サブタイプ アグリゲーターの `punkOuter` (`IUnknown` へのポインター) に対して `QueryInterface` を呼び出します。

|インターフェイス|プロジェクト サブタイプ|
|---------------|---------------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|プロジェクト サブタイプを使用すると、次のことができるようになります。<br /><br /> - <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> の実装を用意します。<br />- プロジェクト サブタイプにより、独自の <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> の実装を用意できるようにすることで、デバッガーの起動を制御します。<br />- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A> の実装で `DBGLAUNCH_DesignTimeExprEval` のケースを適切に処理することにより、デザイン時の式の評価を無効にします。|
|<xref:EnvDTE80.IInternalExtenderProvider>|プロジェクト サブタイプを使用すると、次のことができるようになります。<br /><br /> - プロジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject> を拡張して、プロジェクトの構成に依存しないプロパティを追加または削除できるようにします。<br />- プロジェクトのプロジェクトオートメーション オブジェクト (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtObject>) を拡張します。<br /><br /> 上記のプロパティ値は、<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> の列挙から取得されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|プロジェクト構成参照オブジェクトを指定して、プロジェクト サブタイプを <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> オブジェクトにマップし直すことができます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|プロジェクト構成参照オブジェクトを指定して、プロジェクト サブタイプを <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> または `VSITEMID` オブジェクトにマップし直すことができます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|プロジェクト サブタイプを使用して、任意の XML 構造化データをプロジェクト ファイル (.vbproj または .csproj) に保持できるようにします。 このデータは MSBuild には表示されません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|プロジェクト サブタイプを使用すると、次のことができるようになります。<br /><br /> - 保持する新しい MSBuild プロパティを追加します。<br />- MSBuild から不要なプロパティを削除します。<br />- MSBuild プロパティの現在の値のクエリを実行します。<br />- MSBuild プロパティの現在の値を変更します。|

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>
