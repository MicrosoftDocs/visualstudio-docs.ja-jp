---
title: '方法: エンティティ間に関連付けを作成する | Microsoft Docs'
description: Visual Studio で関連付けを作成することによって、ビジネス データ接続 (BDC) モデルのエンティティ間のリレーションシップを定義します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- AssociationGroupTool
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associations between entities
- BDC [SharePoint development in Visual Studio], associations between entities
- Business Data Connectivity service [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associate external content types
- Business Data Connectivity service [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], associate external content types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e726e8b5702a656b340401c9a2db26e40be1a37d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925568"
---
# <a name="how-to-create-an-association-between-entities"></a>方法: エンティティ間に関連付けを作成する
  関連付けを作成することによって、ビジネス データ接続 (BDC) モデルのエンティティ間のリレーションシップを定義できます。 Visual Studio では、モデルのコンシューマーに各関連付けに関する情報を提供するメソッドが生成されます。 これらのメソッドは、SharePoint Web パーツ、リスト、またはカスタム アプリケーションで、ユーザー インターフェイス (UI) にデータ リレーションシップを表示するために使用できます。

 BDC デザイナーでは、2 種類の関連付けを作成できます。外部キー ベースの関連付けと、外部キーなしの関連付けです。 詳しくは、「[エンティティ間に関連付けを作成する](../sharepoint/creating-an-association-between-entities.md)」をご覧ください。

### <a name="to-create-an-association-between-entities"></a>エンティティ間に関連付けを作成するには

1. **ツールボックス** の **[BusinessDataConnectivity]** タブで、 **[関連付け]** 項目を選択します。

2. BDC デザイナーで、ソース エンティティ、ターゲット エンティティの順に選択します。

     **関連付けエディター** が表示されます。

3. 外部キー ベースの関連付けを作成する場合は、 **[外部キーの関連付けである]** チェック ボックスをオンにします。

    1. **[識別子のマッピング]** テーブルの **[ソース ID]** 列で、 **[フィールド]** 列に表示される型記述子のうち、一致するものごとに横にある識別子を選択します。

         たとえば、 **[ソース ID]** 列で、`ReadList.salesOrderList.SalesOrderList.SalesOrder.ContactID` 型記述子と `ReadItem.salesOrder.SalesOrder.ContactID` 型記述子の横にある `ContactID` を選択します。

4. 外部キーなしの関連付けを作成する場合は、 **[外部キーの関連付けである]** チェック ボックスをオフにします。

5. **[OK]** を選択します。

6. BDC デザイナーでは、関連付けを表す線が、ソース エンティティとターゲット エンティティの間に表示されます。

     Visual Studio では、ターゲット エンティティのサービス クラスとソース エンティティのサービス クラスに関連付けナビゲーター メソッドが追加されます。 関連付けナビゲーション メソッドの詳細については、[サポート対象の操作](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14))に関するページを参照してください。

7. ソース エンティティの関連付けナビゲーター メソッドで、ターゲット エンティティのコレクションを返すコードを追加します。

8. ターゲット エンティティの関連付けナビゲーター メソッドで、関連するソース エンティティを返すコードを追加します。

     関連付けナビゲーター メソッドの例については、「[エンティティ間に関連付けを作成する](../sharepoint/creating-an-association-between-entities.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [エンティティ間に関連付けを作成する](../sharepoint/creating-an-association-between-entities.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
- [方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [チュートリアル: ビジネス データを使用した SharePoint での外部リストの作成](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)
