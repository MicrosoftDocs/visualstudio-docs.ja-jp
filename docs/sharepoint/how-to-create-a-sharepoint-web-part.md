---
title: '方法: SharePoint Web パーツを作成する | Microsoft Docs'
description: Web パーツを作成したりカスタマイズしたりするには、デザイナーを使用するか、SharePoint プロジェクトに Web パーツ項目を追加して Web パーツのコード ファイルを編集します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f15cd788d19540bdea416b36ab0f8e8d8aa95e3a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925601"
---
# <a name="how-to-create-a-sharepoint-web-part"></a>方法: SharePoint Web パーツを作成する
  Web パーツを作成したりカスタマイズしたりするには、SharePoint プロジェクトに **Web パーツ** 項目を追加して Web パーツのコード ファイルを編集する方法と、デザイナーを使用する方法があります。 詳細については、「[方法: デザイナーを使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)」を参照してください。

### <a name="to-create-a-sharepoint-web-part"></a>SharePoint Web パーツを作成するには

1. SharePoint プロジェクトを作成するか開きます。

     詳細については、「[SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. **ソリューション エクスプローラー** で SharePoint プロジェクト ノードを選択し、 **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

4. SharePoint テンプレートの一覧で、 **[Web パーツ]** を選択します。

5. **[名前]** ボックスに Web パーツの名前を入力し、 **[追加]** ボタンを選択します。

     **ソリューション エクスプローラー** に Web パーツが表示されます。 Web パーツに含まれるファイルの詳細については、「[SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)」を参照してください。

6. **ソリューション エクスプローラー** で、作成した Web パーツのコード ファイルを開きます。

     たとえば、Web パーツの名前が *WebPart1* の場合、*WebPart1.vb* (Visual Basic の場合) または *WebPart1.cs* (C# の場合) を開きます。

7. コード ファイルで、<xref:System.Web.UI.Control.CreateChildControls%2A> メソッドにコントロールを追加します。

     例については、「[チュートリアル: SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [方法: デザイナーを使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
- [チュートリアル: SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [チュートリアル: デザイナーを使用した SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
