---
title: '変換: SharePoint プロジェクト システムの種類とその他の種類との間'
titleSuffix: ''
description: SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類の間で変換します。 変換できる種類について詳細に説明している一覧を参照してください。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 973c3d4b3c4fa2dc602e45736dc3a2d2f23c7616
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215293"
---
# <a name="convert-between-sharepoint-project-system-types-and-other-visual-studio-project-types"></a>SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類の間で変換する
  場合によっては、SharePoint プロジェクト システム内にオブジェクトがあるが、Visual Studio オートメーション オブジェクト モデルまたは統合オブジェクト モデル内の対応するオブジェクトの機能を使用したいか、またはその逆を行いたいことがあります。 これらの場合は、SharePoint プロジェクト サービスの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> メソッドを使用して、そのオブジェクトを別のオブジェクト モデルに変換できます。

 たとえば、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトがあるが、<xref:EnvDTE.Project> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> オブジェクトでのみ使用可能なメソッドを使用したいことがあります。 この場合は、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> メソッドを使用して、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> を <xref:EnvDTE.Project> または <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> に変換できます。

 Visual Studio オートメーション オブジェクト モデルと Visual Studio 統合オブジェクト モデルの詳細については、「[SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)」を参照してください。

## <a name="types-of-conversions"></a>変換の種類
 次の表は、このメソッドで SharePoint プロジェクト システムとその他の Visual Studio オブジェクト モデルの間で変換できる種類の一覧を示しています。

|SharePoint プロジェクト システムの種類|オートメーションおよび統合オブジェクト モデル内の対応する種類|
|------------------------------------|-------------------------------------------------------------------------|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>|<xref:EnvDTE.Project><br /><br /> or<br /><br /> プロジェクトの基になる COM オブジェクトによって実装される、Visual Studio 統合オブジェクト モデル内の任意のインターフェイス。 これらのインターフェイスには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> (または派生インターフェイス)、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> が含まれます。 プロジェクトによって実装される主要なインターフェイスの一覧については、「[プロジェクト モデルのコア コンポーネント](../extensibility/internals/project-model-core-components.md)」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.IMappedFolder><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>|<xref:EnvDTE.ProjectItem><br /><br /> or<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> に含まれているプロジェクト メンバーを識別する <xref:System.UInt32> 値 (VSITEMID とも呼ばれます)。 この値は、一部の <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> メソッドの *itemid* パラメーターに渡すことができます。|

## <a name="example"></a>例
 次のコード例は、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> メソッドを使用して <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトを <xref:EnvDTE.Project> に変換する方法を示しています。

:::code language="csharp" source="../sharepoint/codesnippet/CSharp/spprojectserviceaddin/connect.cs" id="Snippet2":::
:::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spprojectserviceaddin/connect.vb" id="Snippet2":::

 この例で必要な要素は次のとおりです。

- *EnvDTE.dll* アセンブリへの参照を含む SharePoint プロジェクト システムの拡張機能。 詳細については、「[SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> イベントを処理する `projectService_ProjectAdded` メソッドを登録するコード。 例については、「[方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)
- [方法: SharePoint プロジェクト サービスを取得する](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)
- [SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
