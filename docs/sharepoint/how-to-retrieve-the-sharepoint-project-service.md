---
title: '方法: SharePoint プロジェクト サービスを取得する | Microsoft Docs'
description: プロジェクト システムの拡張機能、サーバー エクスプローラーの拡張機能、またはその他の Visual Studio 拡張機能で、SharePoint プロジェクト サービスにアクセスする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: ef53a0328fe8427b356132fe878b52a3e504ea9a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214461"
---
# <a name="how-to-retrieve-the-sharepoint-project-service"></a>方法: SharePoint プロジェクト サービスを取得する
  SharePoint プロジェクト サービスには、次の種類のソリューションでアクセスできます。

- SharePoint プロジェクト システムの拡張機能 (プロジェクトの拡張機能、プロジェクト項目の拡張機能、プロジェクト項目の種類の定義など)。 これらの種類の拡張機能について詳しくは、「[SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)」をご覧ください。

- **サーバー エクスプローラー** の **[SharePoint 接続]** ノードの拡張機能。 これらの種類の拡張機能について詳しくは、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」をご覧ください。

- 別の種類の Visual Studio 拡張機能 (VSPackage など)。

## <a name="retrieve-the-service-in-project-system-extensions"></a>プロジェクト システムの拡張機能でサービスを取得する
 SharePoint プロジェクト システムの拡張機能では、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectService%2A> プロパティを使ってプロジェクト サービスにアクセスできます。

 また、次の手順を使用してプロジェクト サービスを取得することもできます。

#### <a name="to-retrieve-the-service-in-a-project-extension"></a>プロジェクトの拡張機能でサービスを取得するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> インターフェイスの実装で、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> メソッドを探します。

2. *projectService* パラメーターを使ってサービスにアクセスします。

     次のコード例は、シンプルなプロジェクト拡張機能でプロジェクト サービスを使って、 **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージを書き込む方法を示したものです。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet1":::

     プロジェクトの拡張機能の作成について詳しくは、「[方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)」をご覧ください。

#### <a name="to-retrieve-the-service-in-a-project-item-extension"></a>プロジェクト項目の拡張機能でサービスを取得するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> インターフェイスの実装で、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> メソッドを探します。

2. *projectItemType* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType.ProjectService%2A> プロパティを使ってサービスを取得します。

     次のコード例は、シンプルな拡張機能でプロジェクト サービスを使って、**List Definition** プロジェクト項目の **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージを書き込む方法を示したものです。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet2":::

     プロジェクト項目の拡張機能の作成について詳しくは、「[方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)」をご覧ください。

#### <a name="to-retrieve-the-service-in-a-project-item-type-definition"></a>プロジェクト項目の種類の定義でサービスを取得するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> インターフェイスの実装で、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> メソッドを探します。

2. *typeDefinition* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.ProjectService%2A> プロパティを使ってサービスを取得します。

     次のコード例は、シンプルなプロジェクト項目の種類の定義でプロジェクト サービスを使って、 **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージを書き込む方法を示したものです。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet3":::

     プロジェクト項目の種類の定義について詳しくは、「[方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)」をご覧ください。

## <a name="retrieve-the-service-in-server-explorer-extensions"></a>サーバー エクスプローラーの拡張機能でサービスを取得する
 **サーバー エクスプローラー** の **[SharePoint 接続]** ノードの拡張機能では、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> プロパティを使ってプロジェクト サービスにアクセスできます。

#### <a name="to-retrieve-the-service-in-a-server-explorer-extension"></a>サーバー エクスプローラーの拡張機能でサービスを取得するには

1. 拡張機能内の <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> プロパティから、<xref:System.IServiceProvider> オブジェクトを取得します。

2. <xref:System.IServiceProvider.GetService%2A> メソッドを使って <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> オブジェクトを要求します。

     次のコード例は、拡張機能によって **サーバー エクスプローラー** のリスト ノードに追加されるショートカット メニューから、プロジェクト サービスを使って、 **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージを書き込む方法を示したものです。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.cs" id="Snippet1":::

     **サーバー エクスプローラー** の **[SharePoint 接続]** ノードの拡張について詳しくは、「[方法: サーバー エクスプローラーの SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)」をご覧ください。

## <a name="retrieve-the-service-in-other-visual-studio-extensions"></a>他の Visual Studio 拡張機能でサービスを取得する
 VSPackage や、オートメーション オブジェクト モデルの <xref:EnvDTE80.DTE2> オブジェクトにアクセスできる任意の Visual Studio 拡張機能 (<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装するプロジェクト テンプレート ウィザードなど) で、プロジェクト サービスを取得できます。

 VSPackage では、次のいずれかの方法を使って <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> オブジェクトを要求できます。

- <xref:Microsoft.VisualStudio.Shell.Package> クラスから派生したマネージド VSPackage の <xref:System.IServiceProvider.GetService%2A> メソッド。 詳しくは、「[方法: サービスを取得する](../extensibility/how-to-get-a-service.md)」をご覧ください。

- 静的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> メソッド。 詳しくは、「[GetGlobalService を使用する](../extensibility/internals/service-essentials.md#how-to-use-getglobalservice)」をご覧ください。

  <xref:EnvDTE80.DTE2> オブジェクトへのアクセス権を持つ Visual Studio 拡張機能では、<xref:Microsoft.VisualStudio.Shell.ServiceProvider> オブジェクトの <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> メソッドを使って <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> オブジェクトを要求できます。 詳しくは、「[DTE オブジェクトからサービスを取得する](../extensibility/how-to-get-a-service.md#getting-a-service-from-the-dte-object)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)
- [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)
- [方法: プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)
