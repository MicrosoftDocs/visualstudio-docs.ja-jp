---
title: プロジェクト サブタイプによって拡張されるプロパティとメソッド | Microsoft Docs
description: プロジェクト サブタイプを拡張または変更して、Visual Studio のプロジェクト システムの動作をカスタマイズするための機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f32c489ba2907cabff47b916039f96754d403455
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064242"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>プロジェクト サブタイプによって拡張されるプロパティとメソッド
プロジェクト サブタイプは、ベース プロジェクトのアグリゲーターとして構築されるため、プロジェクトの動作に大きな影響力があります。 このセクションでは、プロジェクト サブタイプによって拡張または変更できる機能の一部についてまとめています。

## <a name="features-gained-by-aggregation"></a>アグリゲーションによって得られる機能
 プロジェクト サブタイプでは、アグリゲーションによって、次の表にまとめた多くのメソッドをベース プロジェクトでオーバーライドすることが可能になります。

|アグリゲーションによってオーバーライドされるメソッド|プロジェクト サブタイプ|
|---------------------------------------|---------------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> から:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|プロジェクト サブタイプを有効化する目的<br /><br /> -   プロジェクト ノードのキャプションとアイコンを変更する。<br />-   プロジェクトの `Browse` オブジェクトを完全にオーバーライドする。<br />-   プロジェクトの名前を変更できるかどうかを制御する。<br />-   並べ替え順序を制御する。<br />-   ダイナミック ヘルプのユーザー コンテキストを制御する。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> から:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|プロジェクト サブタイプで、デザイナーやエディターに提供されるコンテキスト サービスを制御できるようにします。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> から:<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|プロジェクト サブタイプを有効化する目的<br /><br /> -   プロジェクト コマンドのコマンド ルーティングに参加します。<br />-   プロジェクト アンビエント コマンドとソリューション エクスプローラー アクティブ コマンドの両方を追加、削除、または無効化します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|**[新しい項目の追加]** ダイアログ ボックスでユーザーへの表示をフィルター処理するために、プロジェクト サブタイプを有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|プロジェクト サブタイプを有効化する目的<br /><br /> -   ファイル拡張子を指定して既定のジェネレーターを決定します。<br />-   人間が判読できるジェネレーター名を COM オブジェクトにマップします。|

## <a name="properties-used-by-project-subtypes"></a>プロジェクト サブタイプで使用されるプロパティ
 次の表で詳しく説明する <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID> および <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> 列挙のプロパティを環境およびベース プロジェクト システムで使用すると、プロジェクト システムのさまざまな機能をプロジェクト サブタイプで制御できるようになります。

|VSHPROPID プロパティ|プロジェクト サブタイプ|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|プロジェクト サブタイプで、 **[項目の追加]** ダイアログ ボックスの内容を制御できるようにします。 プロジェクト サブタイプでは、テンプレート ディレクトリの新しい仕様の指定、新しい種類の項目の追加、既存の項目の削除、項目のサブセットの再編成を、ベース プロジェクトの **[項目の追加]** ダイアログ ボックスで実行できます。|
|`PropertyPagesCLSIDList`|プロジェクト サブタイプで、構成から独立したプロパティ ページを追加または削除できるようにします。|
|`CfgPropertyPagesCLSIDList`|プロジェクト サブタイプで、構成に依存したプロパティ ページを追加または削除できるようにします。|
|`ExtObjectCATID`|プロジェクト サブタイプで、エクステンダー CATID を知ることによってプロジェクトまたはプロジェクト項目オブジェクトに対してオートメーション エクステンダーを提供できるようにします。 たとえば、プロジェクト サブタイプはカスタムの `Project.Extender("<subtype>")` オブジェクトを提供できます。|
|`BrowseObjectCATID`|プロジェクト サブタイプで、エクステンダー CATID を知ることによって `Browse` オブジェクトに対してオートメーション エクステンダーを提供できるようにします。 たとえば、プロジェクト サブタイプは、追加のプロパティを <xref:EnvDTE.Project.Properties%2A> コレクションに追加できます。|
|`CfgBrowseObjectCATID`|プロジェクト サブタイプで、プロジェクト構成ブラウズ オブジェクトに対してオートメーション エクステンダーを提供できるようにします。 たとえば、プロジェクト サブタイプは、追加のプロパティを <xref:EnvDTE.Configuration.Properties%2A> コレクションに追加できます。|
|`CfgExtObjectCATID`|プロジェクト サブタイプで、構成オブジェクトに対してオートメーション エクステンダーを提供できるようにします。|
|`DefaultPlatformName`|プロジェクト サブタイプで、プロジェクトの構成オブジェクトに対してプラットフォーム名を決定できるようにします。|

 ベース プロジェクトは、上記のプロパティの既定の実装を提供します。 ベース プロジェクトは、最も外側のプロジェクト サブタイプで <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> の `QueryInterface` を呼び出してこれらを取得し、プロジェクト サブタイプでプロパティの実装をオーバーライドできるようにします。

## <a name="see-also"></a>関連項目
- [プロジェクト サブタイプのデザイン](../../extensibility/internals/project-subtypes-design.md)
