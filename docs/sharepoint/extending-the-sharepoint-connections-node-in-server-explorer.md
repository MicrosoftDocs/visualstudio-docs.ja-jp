---
title: サーバー エクスプローラーの [SharePoint 接続] ノードの拡張 | Microsoft Docs
titleSuffix: ''
description: Visual Studio で [サーバー エクスプローラー] ウィンドウの [SharePoint 接続] ノードを拡張します。 ノードにカスタム プロパティを追加します。 組み込みノードのデータを取得します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1f77e0044b8ae3c7456a31bb9c9153ba9e9f4c99
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218036"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する
  Visual Studio では、**サーバー エクスプローラー** ウィンドウの **[SharePoint 接続]** ノードを使用して、開発用コンピューター上のローカル SharePoint サイトに接続できます。 このノードには、ローカル SharePoint サイトの多数のコンポーネントが階層ツリー ビューで表示されます。 たとえば、ローカル サイト上のリスト、ドキュメント ライブラリ、コンテンツ タイプを表示できます。 **サーバー エクスプローラー** を使用してローカル SharePoint サイトに接続する方法の詳細については、「[サーバー エクスプローラーを使用して SharePoint 接続を参照する](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)」を参照してください。

 既存のノードの拡張機能を作成するか、またはカスタムのノードの種類を作成し、それをノードの階層に追加することによって、 **[SharePoint 接続]** ノードを拡張できます。

## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>[SharePoint 接続] ノードを拡張するためのタスク
 既存のノードを拡張するには、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> インターフェイスを実装する Visual Studio 拡張機能を作成します。 ノードを拡張すると、そのノードに、独自のショートカット メニュー項目やカスタム プロパティなどの機能を追加できます。 詳細については、「[方法: サーバー エクスプローラーの SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)」を参照してください。

 カスタムのノードの種類を作成するには、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> インターフェイスを実装する Visual Studio 拡張機能を作成します。 カスタム ノードは、既定では **サーバー エクスプローラー** に表示されない SharePoint サイトのコンポーネントを表示したい場合に作成します。 たとえば、既定では **サーバー エクスプローラー** に SharePoint サイトの Web パーツ ギャラリーは表示されませんが、これを表示するカスタム ノードを追加できます。 詳細については、「[方法: サーバー エクスプローラーにカスタム SharePoint ノードを追加する](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)」および「[チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

## <a name="add-custom-properties-to-nodes"></a>ノードにカスタム プロパティを追加する
 ノードを拡張するか、またはカスタムのノードの種類を作成する場合は、そのノードにカスタム プロパティを追加できます。 これらのプロパティは、そのノードが選択されたときに **[プロパティ]** ウィンドウに表示されます。

 ノードに追加できるカスタム プロパティの種類には、次の 2 つがあります。

- SharePoint サイトからの一連の読み取り専用データを表示するプロパティ。 これらのデータには、そのノードが表す SharePoint コンポーネントが記述されています。 これを行う方法を示すチュートリアルについては、「[チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

- カスタムの読み取り/書き込みデータを表示するプロパティ。 これを行う方法を示すコード例については、「[方法: サーバー エクスプローラーの SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)」を参照してください。

## <a name="get-data-for-built-in-nodes"></a>組み込みノードのデータを取得する
 Visual Studio によって提供されるすべての組み込みノードには、それらのノードが表す SharePoint コンポーネントに関するいくつかのデータが含まれています。 たとえば、SharePoint サイト上のリストを表すノードは、そのリストに関するいくつかのデータ (そのリストの既定のビューのタイトルと URL など) を提供します。

 これらのデータにアクセスするには、目的のノードを表す <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティからデータ オブジェクトを取得します。 データ オブジェクトの種類は、そのノードの種類によって異なります。

 次のコード例は、リスト ノードのデータ オブジェクトを取得する方法を示しています。 この例をより大きな例のコンテキストで確認するには、「[方法: サーバー エクスプローラーの組み込みの SharePoint ノードのデータを取得する](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)」を参照してください。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb" id="Snippet11":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs" id="Snippet11":::

 次の表は、組み込みのノードの種類ごとのデータ オブジェクトの種類の一覧を示しています。

|ノード型|データ オブジェクトの種類|
|---------------|----------------------|
|SharePoint サイト ノード|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|
|Content type|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|
|機能|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|
|フィールド|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|
|List|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|
|リスト テンプレート|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|
|リスト ビュー (Microsoft.SharePoint.SPView)|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|
|ワークフローの関連付け|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|
|ワークフロー テンプレート|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|

 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティの使用の詳細については、「[カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [方法: サーバー エクスプローラーの SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [方法: サーバー エクスプローラーにカスタム SharePoint ノードを追加する](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [方法: サーバー エクスプローラーの組み込みの SharePoint ノードのデータを取得する](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)
- [カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [サーバー エクスプローラーを使用して SharePoint 接続を参照する](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
