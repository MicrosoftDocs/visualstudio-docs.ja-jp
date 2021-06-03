---
title: '方法: Finder メソッドにフィルター記述子を追加する | Microsoft Docs'
description: Visual Studio の [BDC メソッドの詳細] ウィンドウを使用して Finder メソッドにフィルター記述子を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], filter descriptors
- Business Data Connectivity service [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], filter descriptors
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 47fcc7e388f240d8b9636a733df4b6b8767f0df4
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218010"
---
# <a name="how-to-add-a-filter-descriptor-to-a-finder-method"></a>方法: Finder メソッドにフィルター記述子を追加する
  フィルター記述子を使用すると、モデルのコンシューマーは、実行前のメソッドに値を渡すことができます。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

 1 つの一般的なシナリオとして、SharePoint のユーザーが、何らかの条件に一致する外部コンテンツ タイプのインスタンスを取得しようとする場合があります。 このシナリオは、Finder メソッドにフィルター記述子を追加することによってサポートできます。

### <a name="to-add-a-filter-descriptor-to-a-finder-method"></a>Finder メソッドにフィルター記述子を追加するには

1. **[BDC メソッドの詳細]** ウィンドウで、Finder メソッドのノードを展開し、 **[パラメーター]** ノードを展開して、入力パラメーターを追加します。 詳細については、「[方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)」を参照してください。

2. **[メソッドの詳細]** ウィンドウで、パラメーターの型記述子を選択します。

3. メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択します。

4. **[プロパティ]** ウィンドウで、 **[型の名前]** プロパティをフィルターに適したデータ型に設定します。

     たとえば、あるフィルターでは、このメソッドによって返される販売注文の数を制限するために注文日を使用する可能性があります。 そのフィルターをサポートするには、型記述子の **[型の名前]** プロパティを **[System.DateTime]** に設定する必要があります。

5. **[メソッドの詳細]** ウィンドウで、 **[フィルター記述子]** ノードを展開します。

6. **[フィルター記述子の追加]** 一覧で、 **[フィルター記述子の作成]** を選択します。

     新しいフィルター記述子が **[フィルター記述子]** ノードの下に表示されます。

7. メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択します。

8. **[プロパティ]** ウィンドウで、 **[種類]** プロパティを選択します。

9. **[種類]** プロパティに対して表示される一覧で、必要なフィルター パターンを選択します。

     たとえば、Finder メソッドで返される販売注文の数を制限するために注文日を使用するフィルターを作成するには、 **[比較]** を選択します。 比較フィルターにより、Finder メソッドでは確実に、特定の条件を満たすインスタンスのみを返すようになります。 各フィルター パターンの詳細については、[BDC でサポートされているフィルターの種類](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14))に関するページを参照してください。

10. **[プロパティ]** ウィンドウで、 **[関連付けられた型記述子]** プロパティを選択します。

11. **[関連付けられた型記述子]** プロパティに対して表示される一覧で、この手順で前に作成した型記述子を選択します。 これにより、このフィルターが Finder メソッドの入力パラメーターに関連付けられます。

12. データを返す Finder メソッドにコードを追加します。 この入力パラメーターは、選択クエリでの条件として使用できます。

     次の例では、注文日が指定されている販売注文を返します。

    > [!NOTE]
    > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs" id="Snippet11":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb" id="Snippet11":::

## <a name="see-also"></a>関連項目
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Specific Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
