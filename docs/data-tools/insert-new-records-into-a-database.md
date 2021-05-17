---
title: データベースに新しいレコードを挿入する
description: TableAdapter.Update メソッド、TableAdapter の DBDirect メソッドの 1 つ、またはコマンド オブジェクトを使用して、データベースに新しいレコードを挿入します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, inserting new records into
- data [Visual Studio], saving
- databases, inserting new records into
- records, inserting
- saving data
ms.assetid: ea118fff-69b1-4675-b79a-e33374377f04
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 6e1046dfd114e4cad69445b8f4e1432c03aac0e5
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216463"
---
# <a name="insert-new-records-into-a-database"></a>データベースに新しいレコードを挿入する

新しいレコードをデータベースに挿入するには、`TableAdapter.Update` メソッド、または TableAdapter の DBDirect メソッドの 1 つ (具体的には `TableAdapter.Insert` メソッド) を使用します。 詳細については、[TableAdapter](../data-tools/create-and-configure-tableadapters.md) に関するページを参照してください。

アプリケーションで TableAdapter を使用しない場合は、コマンド オブジェクト (<xref:System.Data.SqlClient.SqlCommand> など) を使用してデータベースに新しいレコードを挿入できます。

アプリケーションでデータセットを使用してデータを格納する場合は、`TableAdapter.Update` メソッドを使用します。 `Update` メソッドでは、すべての変更 (更新、挿入、削除) をデータベースに送信します。

アプリケーションでオブジェクトを使用してデータを格納する場合、またはデータベースで新しいレコードの作成をより細かく制御する必要がある場合は、`TableAdapter.Insert` メソッドを使用します。

TableAdapter に `Insert` メソッドがない場合は、TableAdapter がストアド プロシージャを使用するように構成されているか、その `GenerateDBDirectMethods` プロパティが `false` に設定されていることを意味します。 **データセット デザイナー** 内から TableAdapter の `GenerateDBDirectMethods` プロパティを `true` に設定し、データセットを保存します。 これにより、TableAdapter が再生成されます。 TableAdapter に `Insert` メソッドがまだない場合、テーブルには、個別の行を区別するための十分なスキーマ情報がない可能性があります (たとえば、テーブルに主キーが設定されていない可能性があります)。

## <a name="insert-new-records-by-using-tableadapters"></a>TableAdapter を使用して新しいレコードを挿入する

TableAdapter には、アプリケーションの要件に応じて、データベースに新しいレコードを挿入するためのさまざまな方法が用意されています。

アプリケーションでデータセットを使用してデータを格納する場合は、単にデータセット内の目的の <xref:System.Data.DataTable> に新しいレコードを追加し、`TableAdapter.Update` メソッドを呼び出すことができます。 `TableAdapter.Update` メソッドでは、<xref:System.Data.DataTable> の変更をデータベースに送信します (変更されたレコードと削除されたレコードを含む)。

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>TableAdapter.Update メソッドを使用して新しいレコードをデータベースに挿入するには

1. 新しい <xref:System.Data.DataRow> を作成し、<xref:System.Data.DataTable.Rows%2A> コレクションに追加して、目的の <xref:System.Data.DataTable> に新しいレコードを追加します。

2. 新しい行を <xref:System.Data.DataTable> に追加した後、`TableAdapter.Update` メソッドを呼び出します。 更新するデータの量を制御するには、<xref:System.Data.DataSet> 全体、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> の配列、または単一の <xref:System.Data.DataRow> を渡します。

   次のコードでは、<xref:System.Data.DataTable> に新しいレコードを追加し、`TableAdapter.Update` メソッドを呼び出して新しい行をデータベースに保存する方法を示します (この例では、Northwind データベースの `Region` テーブルを使用します)。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb" id="Snippet14":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs" id="Snippet14":::

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>TableAdapter.Insert メソッドを使用して新しいレコードをデータベースに挿入するには

アプリケーションでオブジェクトを使用してデータを格納する場合は、`TableAdapter.Insert` メソッドを使用してデータベースに直接新しい行を作成できます。 `Insert` メソッドは、各列の個別の値をパラメーターとして受け取ります。 メソッドを呼び出すと、渡されたパラメーター値を使用して新しいレコードがデータベースに挿入されます。

- TableAdapter の `Insert` メソッドを呼び出し、各列の値をパラメーターとして渡します。

次の手順では、`TableAdapter.Insert` メソッドを使用して行を挿入する方法を示します。 この例では、Northwind データベースの `Region` テーブルにデータを挿入します。

> [!NOTE]
> 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

## <a name="insert-new-records-by-using-command-objects"></a>コマンド オブジェクトを使用して新しいレコードを挿入する

コマンド オブジェクトを使用して、新しいレコードをデータベースに直接挿入できます。

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>コマンド オブジェクトを使用して新しいレコードをデータベースに挿入するには

- 新しいコマンド オブジェクトを作成し、`Connection`、`CommandType`、`CommandText` の各プロパティを設定します。

次の例では、コマンド オブジェクトを使用してデータベースにレコードを挿入する方法を示します。 Northwind データベースの `Region` テーブルにデータを挿入します。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet16":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet16":::

## <a name="net-security"></a>.NET セキュリティ

接続しようとしているデータベースへのアクセス権と、目的のテーブルに挿入を実行する権限が必要です。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
