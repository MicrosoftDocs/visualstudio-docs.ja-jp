---
title: '方法: モデルにエンティティを追加する | Microsoft Docs'
description: Visual Studio のツールボックスからビジネス データ接続 (BDC) デザイナーにエンティティ コントロールを追加することによって、モデルにエンティティを追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- EntityTool
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], entity
- Business Data Connectivity service [SharePoint development in Visual Studio], adding an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], entity
- BDC [SharePoint development in Visual Studio], adding an entity
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 94d34e6a623438cd0e2d63d74ee2321841a0582a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216775"
---
# <a name="how-to-add-an-entity-to-a-model"></a>方法: モデルにエンティティを追加する
  エンティティを作成するには、Visual Studio の **ツールボックス** からビジネス データ接続 (BDC) デザイナーにエンティティ コントロールを追加します。

### <a name="to-add-an-entity-to-the-model"></a>モデルにエンティティを追加するには

1. BDC プロジェクトを作成するか、または既存の BDC プロジェクトを開きます。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

2. **ツールボックス** で、**BusinessDataCatalog** グループから、**Entity** コントロールをデザイナーに追加します。

     新しいエンティティがデザイナーに表示されます。 Visual Studio では、プロジェクト内の BDC モデル ファイルの XML に `<Entity>` 要素を追加します。 Entity 要素の属性の詳細については、[Entity](/previous-versions/office/developer/sharepoint-2010/ee558325(v=office.14)) に関するページを参照してください。

3. デザイナーで、エンティティのショートカット メニューを開き、 **[追加]** を選択してから、 **[識別子]** を選択します。

     新しい識別子がエンティティに表示されます。

    > [!NOTE]
    > エンティティと識別子の名前は、 **[プロパティ]** ウィンドウで変更できます。

4. クラスでエンティティのフィールドを定義します。 プロジェクトに新しいクラスを追加するか、またはオブジェクト リレーショナル デザイナー (O/R デザイナー) などの他のツールを使用して作成された既存のクラスを使用できます。 次の例は、Contact という名前のエンティティ クラスを示しています。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_bdc_entity_data_class/bdcmodel1/contact.cs" id="Snippet1":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc_entity_data_class/bdcmodel1/contact.vb" id="Snippet1":::

## <a name="see-also"></a>関連項目
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Specific Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
