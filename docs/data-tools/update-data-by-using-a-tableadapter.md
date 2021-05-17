---
title: TableAdapter を使用してデータを更新する
description: データセット内のデータを更新します。 TableAdapter の Update メソッドを呼び出して、データをデータベースに戻します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: f3054c5c74c8844f780c3562327353fca164f1f4
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215644"
---
# <a name="update-data-by-using-a-tableadapter"></a>TableAdapter を使用してデータを更新する

データセット内のデータを変更および検証した後に、[TableAdapter](../data-tools/create-and-configure-tableadapters.md) の `Update` メソッドを呼び出すことによって、更新済みのデータをデータベースに戻すことができます。 `Update` メソッドでは、単一のデータ テーブルが更新され、正しいコマンド (INSERT、UPDATE、または DELETE) がテーブル内の各データ行の <xref:System.Data.DataRow.RowState%2A> に基づいて実行されます。 データセットに関連テーブルがある場合、Visual Studio によって、更新を実行するために使用する TableAdapterManager クラスが生成されます。 TableAdapterManager クラスにより、データベースに定義されている外部キー制約に基づいて、更新が確実に正しい順序で行われます。 データバインド コントロールを使用すると、データバインディング アーキテクチャによって tableAdapterManager という TableAdapterManager クラスのメンバー変数が作成されます。

> [!NOTE]
> データセットの内容でデータソースを更新しようとすると、エラーが発生することがあります。 エラーを回避するには、アダプターの `Update` メソッドを呼び出すコードを `try`/`catch` ブロック内に配置することが推奨されます。

データ ソースを更新するための正確な手順は、ビジネス ニーズによって異なる可能性がありますが、次の手順が含まれます。

1. `try`/`catch` ブロックでアダプターの `Update` メソッドを呼び出します。

2. 例外が検出された場合は、エラーを引き起こしたデータ行を探します。

3. データ行の問題を調整し (可能な場合はプログラムによって、またはユーザーに無効な行を提示して修正を求めることによって)、再度更新を試みます (<xref:System.Data.DataRow.HasErrors%2A>、<xref:System.Data.DataTable.GetErrors%2A>)。

## <a name="save-data-to-a-database"></a>データベースにデータを保存する

TableAdapter の `Update` メソッドを呼び出します。 データベースに書き込まれる値を含むデータ テーブルの名前を渡します。

### <a name="to-update-a-database-by-using-a-tableadapter"></a>TableAdapter を使用してデータベースを更新するには

- TableAdapter の `Update` メソッドを `try`/`catch` ブロックで囲みます。 次の例は、`NorthwindDataSet` 内の `Customers` テーブルの内容を、`try`/`catch` ブロック内から更新する方法を示しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet9":::

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
