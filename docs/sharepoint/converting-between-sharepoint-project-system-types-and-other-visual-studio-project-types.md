---
title: SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類間の変換 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: aec5557b2837317bfd634035875628ef0e68220c
ms.sourcegitcommit: c0202a77d4dc562cdc55dc2e6223c062281d9749
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54863358"
---
# <a name="convert-between-sharepoint-project-system-types-and-other-visual-studio-project-types"></a>SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類間の変換します。
  場合によっては、SharePoint プロジェクト システムでオブジェクトがある可能性があり、Visual Studio オートメーション オブジェクト モデルまたは統合オブジェクト モデル内の対応するオブジェクトの機能を使用するか、その逆です。 このような場合は、使用することができます、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>オブジェクトを別のオブジェクト モデルに変換する SharePoint プロジェクト サービスのメソッド。

 たとえば、する必要があります、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>のみで使用できるメソッドを使用するには、オブジェクト、<xref:EnvDTE.Project>または<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>オブジェクト。 この場合、使用することができます、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>に変換するメソッド、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>を<xref:EnvDTE.Project>または<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>します。

 Visual Studio オートメーション オブジェクト モデルと、Visual Studio の統合オブジェクト モデルの詳細については、[ツールの拡張機能を SharePoint のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)を参照してください。

## <a name="types-of-conversions"></a>型の変換
 次の表では、このメソッドは、SharePoint プロジェクト システムと他の Visual Studio のオブジェクト モデルの間で変換できる型を示します。

|SharePoint プロジェクト システムの種類|Automation との統合オブジェクト モデルの対応する型|
|------------------------------------|-------------------------------------------------------------------------|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>|<xref:EnvDTE.Project><br /><br /> または<br /><br /> プロジェクトの基になる COM オブジェクトによって実装されている Visual Studio の統合オブジェクト モデル内の任意のインターフェイス これらのインターフェイスを含める<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> (または派生インターフェイス)、および<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>します。 プロジェクトで実装される主なインターフェイスの一覧は、[プロジェクト モデルのコア コンポーネント](../extensibility/internals/project-model-core-components.md)を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.IMappedFolder><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>|<xref:EnvDTE.ProjectItem><br /><br /> または<br /><br /> A<xref:System.UInt32> (、VSITEMID とも呼ばれます) でプロジェクトのメンバーを識別する値、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>含まれています。 この値に渡されることができます、 *itemid*いくつかのパラメーター<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>メソッド。|

## <a name="example"></a>例
 次のコード例は、使用する方法を示します、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>に変換するメソッド、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>オブジェクトを<xref:EnvDTE.Project>します。

 [!code-csharp[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/CSharp/spprojectserviceaddin/connect.cs#2)]
 [!code-vb[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/VisualBasic/spprojectserviceaddin/connect.vb#2)]

 この例で必要な要素は次のとおりです。

-   参照を含む SharePoint プロジェクト システムの拡張機能、 *EnvDTE.dll*アセンブリ。 詳細については、[SharePoint プロジェクト システムを拡張](../sharepoint/extending-the-sharepoint-project-system.md)を参照してください。

-   登録するコードを`projectService_ProjectAdded`を処理するメソッド、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded>のイベント、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService>オブジェクト。 例については、「[方法: SharePoint プロジェクト拡張機能作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)です。

## <a name="see-also"></a>関連項目

- [SharePoint プロジェクト サービスを使用します。](../sharepoint/using-the-sharepoint-project-service.md)
- [方法: SharePoint プロジェクト サービスを取得します。](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)
- [ツールの拡張機能を SharePoint のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
