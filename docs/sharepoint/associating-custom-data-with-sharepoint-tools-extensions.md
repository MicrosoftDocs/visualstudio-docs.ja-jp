---
title: カスタム データの SharePoint ツール拡張機能への関連付け | Microsoft Docs
description: カスタム データを SharePoint ツール拡張機能に関連付けます。 カスタム データを含めることができるオブジェクトの一覧を参照してください。 カスタム データを追加して取得します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], associating custom data
- project items [SharePoint development in Visual Studio], associating custom data
- SharePoint project items, associating custom data
- SharePoint projects, associating custom data
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5665fc28bacb76c6887cb7dcb1820ec9dc0d2b3a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215319"
---
# <a name="associate-custom-data-with-sharepoint-tools-extensions"></a>カスタム データを SharePoint ツール拡張機能に関連付ける
  SharePoint ツール拡張機能の特定のオブジェクトにカスタム データを追加できます。 これは、拡張機能の一部に、後でその拡張機能の他のコードからアクセスするデータがある場合に役立ちます。 データを格納したり、データにアクセスしたりするための独自の方法を実装する代わりに、データを拡張機能のオブジェクトに関連付け、後で同じオブジェクトからそのデータを取得できます。

 カスタム データのオブジェクトへの追加はまた、Visual Studio の特定の項目に関連するデータを保持したい場合にも役立ちます。 SharePoint ツール拡張機能は Visual Studio で 1 回だけ読み込まれるため、拡張機能ではいつでも、いくつかの異なる項目 (プロジェクト、プロジェクト項目、**サーバー エクスプローラー** ノードなど) を操作する可能性があります。 特定の項目にのみ関連するカスタム データがある場合は、その項目を表すオブジェクトにそのデータを追加できます。

 SharePoint ツール拡張機能のオブジェクトにカスタム データを追加する場合、そのデータは保持されません。 そのデータはオブジェクトの有効期間中にのみ使用できます。 オブジェクトがガーベジ コレクションによって回収されると、そのデータは失われます。

 SharePoint プロジェクト システムの拡張機能では、拡張機能がアンロードされた後も保持される文字列データを保存することもできます。 詳細については、[SharePoint プロジェクト システムの拡張機能へのデータの保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)に関するページを参照してください。

## <a name="objects-that-can-contain-custom-data"></a>カスタム データを含めることができるオブジェクト
 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> インターフェイスを実装する SharePoint ツール オブジェクト モデル内の任意のオブジェクトにカスタム データを追加できます。 このインターフェイスでは、カスタム データ オブジェクトのコレクションである 1 つのプロパティ <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> のみを定義します。 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> は、次の種類によって実装されます。

- <xref:Microsoft.VisualStudio.SharePoint.IMappedFolder>

- <xref:Microsoft.VisualStudio.SharePoint.IMenuItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectMember>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>

- <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentContext>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition>

## <a name="add-and-retrieve-custom-data"></a>カスタム データを追加して取得する
 SharePoint ツール拡張機能のオブジェクトにカスタム データを追加するには、データを追加するオブジェクトの <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティを取得してから、<xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A> メソッドを使用してオブジェクトにデータを追加します。

 SharePoint ツール拡張機能のオブジェクトからカスタム データを取得するには、そのオブジェクトの <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティを取得してから、次のいずれかのメソッドを使用します。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>. このメソッドは、データ オブジェクトが存在する場合は **true** を、存在しない場合は **false** を返します。 このメソッドを使用すると、値の型または参照型のインスタンスを取得できます。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>. このメソッドは、データ オブジェクトが存在する場合はそのデータ オブジェクトを、存在しない場合は **null** を返します。 このメソッドは、参照型のインスタンスを取得するためにのみ使用できます。

  次のコード例では、特定のデータ オブジェクトが既にプロジェクト項目に関連付けられているかどうかを判定します。 データ オブジェクトがまだプロジェクト項目に関連付けられていない場合、このコードでは、そのオブジェクトをプロジェクト項目の <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティに追加します。 この例をより大きな例のコンテキストで確認するには、「[方法: プロパティをカスタムの SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)」を参照してください。

  :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet13":::
  :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet13":::

## <a name="see-also"></a>関連項目
- [SharePoint ツール拡張機能におけるプログラミングに関する概念および特徴](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [チュートリアル: 項目テンプレートに基づくカスタム動作プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [方法: プロパティをカスタムの SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
