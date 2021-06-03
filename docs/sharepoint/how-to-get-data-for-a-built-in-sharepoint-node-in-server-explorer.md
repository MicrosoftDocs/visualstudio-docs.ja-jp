---
title: サーバー エクスプローラーの組み込みの SharePoint ノードのデータを取得する
titleSuffix: ''
description: Visual Studio の [サーバー エクスプローラー] ウィンドウで、組み込みの SharePoint ノードの基になる SharePoint コンポーネントのデータを取得します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c58de345400c7b724a755839cb8baa1afc3cfce2
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217191"
---
# <a name="how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer"></a>方法: サーバー エクスプローラーの組み込みの SharePoint ノードのデータを取得する
  **サーバー エクスプローラー** の組み込みの SharePoint ノードごとに、そのノードが表す基になる SharePoint コンポーネントのデータを取得できます。 詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

## <a name="example"></a>例
 次のコード例は、**サーバー エクスプローラー** でリスト ノードが表す基になる SharePoint リストのデータを取得する方法を示しています。 既定では、リスト ノードには、クリックするとリストを Web ブラウザーで開くことができる **[ブラウザーで表示]** コンテキスト メニュー項目が含まれています。 この例では、リストを Visual Studio で直接開く **[Visual Studio で表示]** コンテキスト メニュー項目を追加することによってリスト ノードを拡張します。 このコードでは、Visual Studio で開くリストの URL を取得するために、そのノードのリスト データにアクセスします。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb" id="Snippet10":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs" id="Snippet10":::

 この例では、SharePoint プロジェクト サービスを使用して、リストを Visual Studio で開くために使用される <xref:EnvDTE.DTE> オブジェクトを取得します。 SharePoint プロジェクト サービスの詳細については、「[SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

 SharePoint ノードの拡張機能を作成するための基本タスクの詳細については、「[方法: サーバー エクスプローラーの SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照が必要です。

- EnvDTE

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.SharePoint.Explorer.Extensions

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 **サーバー エクスプローラー** の拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [方法: サーバー エクスプローラーの SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)
- [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
