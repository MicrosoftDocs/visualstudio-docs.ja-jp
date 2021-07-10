---
title: '方法: デザイナーを使用して SharePoint Web パーツを作成する | Microsoft Docs'
titleSuffix: ''
description: 視覚的 Web パーツ項目を SharePoint プロジェクトに追加し、Visual Studio で Visual Web Developer を開く Web パーツを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cbbb290af0029329910a23a71f68024ee0e5e5f4
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112381"
---
# <a name="how-to-create-a-sharepoint-web-part-by-using-a-designer"></a>方法: デザイナーを使用して SharePoint Web パーツを作成する

  Web パーツを作成するには、SharePoint プロジェクトに **視覚的 Web パーツ項目** を追加します。 これを行うと、Visual Studio で Visual Web Developer デザイナーが開きます。このデザイナーでは、コントロールとコードを Web パーツに追加できます。 視覚的 Web パーツは Web パーツと同じように機能します。 唯一の違いは、視覚的 Web パーツのデザインは Visual Web Developer デザイナーで行うことです。

## <a name="to-create-a-project-for-visual-web-parts"></a>視覚的 Web パーツのプロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  > **[新規作成]**  >  **[プロジェクト]** を選択します。
::: moniker range="=vs-2017"

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** の **[Office/SharePoint]** ノードを展開し、 **[SharePoint ソリューション]** カテゴリを選択します。

3. プロジェクト テンプレートの一覧で **[SharePoint 2013 - 視覚的 Web パーツ]** を選択し、 **[OK]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が表示されます。
::: moniker-end
::: moniker range=">=vs-2019"
2. **[新しいプロジェクトの作成]** ダイアログで、インストールした SharePoint の特定のバージョンに対応する *SharePoint 視覚的 Web パーツ** を選択します。 たとえば、SharePoint 2019 がインストールされている場合は、 **[SharePoint 2019 - 視覚的 Web パーツ]** テンプレートを選択します。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 必要であればプロジェクトの名前を変更し、 **[作成]** ボタンを選択します。

::: moniker-end
4. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、ローカル コンピューター上の SharePoint サイトの URL を指定し、 **[完了]** をクリックします。

     **ソリューション エクスプローラー** に Web パーツが表示されます。 Visual Web Developer デザイナーで Web パーツをデザインしたら、指定したサイトでその Web パーツをテストします。

### <a name="to-add-a-visual-web-part-to-an-existing-sharepoint-project"></a>既存の SharePoint プロジェクトに視覚的 Web パーツを追加するには

1. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[Office/SharePoint]** ノードを選択します。

3. プロジェクト テンプレートの一覧で **[視覚的 Web パーツ]** を選択し、それに名前を付けて、 **[追加]** をクリックします。

     **ソリューション エクスプローラー** に Web パーツが表示されます。 Visual Web Developer デザイナーで Web パーツをデザインしたら、指定したサイトでその Web パーツをテストします。

## <a name="see-also"></a>関連項目

- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [方法: SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)
- [チュートリアル: SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [チュートリアル: デザイナーを使用した SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
