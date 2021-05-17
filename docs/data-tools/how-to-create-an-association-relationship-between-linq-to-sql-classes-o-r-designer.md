---
title: LINQ to SQL クラス間のリレーションシップ
description: オブジェクト リレーショナル デザイナー (O/R デザイナー) の [関連付けエディター] ダイアログ ボックスを使用して LINQ to SQL エンティティ クラス間の関連付けを作成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 56133e65-81f3-44c3-bc28-ffdd0671a0d2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: a4a13de7c6d9f9627332852be26356f26109c92d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866841"
---
# <a name="how-to-create-an-association-between-linq-to-sql-classes-or-designer"></a>方法: LINQ to SQL クラス間の関連付けを作成する (O/R デザイナー)
[!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] のエンティティ クラス間の関連付けは、データベース内のテーブル間の関連付けに似ています。 **[関連付けエディター]** ダイアログ ボックスを使用することで、エンティティ クラス間の関連付けを作成できます。

**[関連付けエディター]** ダイアログ ボックスを使用して関連付けを作成するときは、親クラスと子クラスを選択する必要があります。 親クラスは、主キーを含むエンティティ クラスであり、子クラスは、外部キーを含むエンティティ クラスです。 たとえば、`Northwind Customers` テーブルと `Orders` テーブルにマップされるエンティティ クラスが作成された場合は、`Customer` クラスが親クラスであり、`Order` クラスが子クラスです。

> [!NOTE]
> **サーバー エクスプローラー** または **データベース エクスプローラー** から **オブジェクト リレーショナル デザイナー** (**O/R デザイナー**) にテーブルをドラッグすると、データベース内の既存の外部キー リレーションシップに基づいて関連付けが自動的に作成されます。

## <a name="association-properties"></a>関連付けのプロパティ
関連付けの作成後、**O/R デザイナー** で関連付けを選択すると、**[プロパティ]** ウィンドウにいくつかの構成可能なプロパティが表示されます。 (関連付けは、関連クラス間の線で表されます。) 次の表は、関連付けのプロパティの説明を示しています。

|プロパティ|説明|
|--------------|-----------------|
|**カーディナリティ**|関連付けが 1 対多と 1 対 1 のどちらであるかを制御します。|
|**子プロパティ**|コレクションのプロパティを親に作成するか、子レコードへの参照を関連付けの外部キー側に作成するかを指定します。 たとえば、`Customer` と `Order` 間の関連付けでは、**子プロパティ** が **True** に設定され、`Orders` という名前のプロパティが親クラスに作成されます。|
|**Parent プロパティ**|関連付けられている親クラスを参照する子クラスのプロパティです。 たとえば、`Customer` と `Order` の間の関連付けでは、注文に関連付けられている顧客を参照する `Customer` という名前のプロパティが `Order` クラスに作成されます。|
|**関与のプロパティ**|関連付けのプロパティを表示し、**[関連付けエディター]** ダイアログ ボックスを再び開く **省略記号** ボタン (...) が用意されています。|
|**[一意]**|外部ターゲット列に一意性の制約があるかどうかを示します。|

## <a name="to-create-an-association-between-entity-classes"></a>エンティティ クラス間に関連付けを作成するには

1. 関連付けの親クラスを表すエンティティ クラスを右クリックし、**[追加]** をポイントして、**[関連付け]** をクリックします。

2. **[関連付けエディター]** ダイアログ ボックスで、正しい **親クラス** が選択されていることを確認します。

3. コンボ ボックスで **子クラス** を選択します。

4. クラスに関連する **[関連付けのプロパティ]** を選択します。 通常、これはデータベースで定義されている外部キー リレーションシップにマップされます。 たとえば、`Customers` と `Orders` の関連付けでは、 **[関連付けのプロパティ]** は各クラスの `CustomerID` になります。

5. **[OK]** をクリックして、関連付けを作成します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [方法: 主キーを表す](/dotnet/framework/data/adonet/sql/linq/how-to-represent-primary-keys)
