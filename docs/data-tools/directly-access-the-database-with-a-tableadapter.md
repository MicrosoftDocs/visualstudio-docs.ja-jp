---
title: TableAdapter で直接データベースにアクセスする
description: TableAdapter で直接データベースにアクセスし、Insert、Update、Delete などのメソッドを使用してデータベース内のデータを直接操作します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Visual Basic], accessing with a TableAdapter
- DBDirect methods
- datasets [Visual Basic], adding to projects
- data [Visual Studio], saving
- TableAdapter.Delete method
- GenerateDbDirectMethods property
- TableAdapter.Insert method
- TableAdapter.GenerateDBDirectMethods property
- TableAdapter.Update method
- saving data
- TableAdapters
ms.assetid: 012c5924-91f7-4790-b2a6-f51402b7014b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 30248632eacde07cfcc94213aeeb75ecac8dcf70
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215917"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>TableAdapter で直接データベースにアクセスする

`InsertCommand`、`UpdateCommand`、`DeleteCommand` に加えて、データベースに対して直接実行できるメソッドで、TableAdapter が作成されます。 これらのメソッド (`TableAdapter.Insert`、`TableAdapter.Update`、`TableAdapter.Delete`) を呼び出して、データベース内のデータを直接操作できます。

これらの直接メソッドを作成しない場合は、 **[プロパティ]** ウィンドウで、TableAdapter の `GenerateDbDirectMethods` プロパティを `false` に設定します。 TableAdapter のメイン クエリに加えて、TableAdapter にクエリが追加された場合、それらは、これらの `DbDirect` メソッドを生成しないスタンドアロン クエリです。

## <a name="send-commands-directly-to-a-database"></a>コマンドをデータベースに直接送信する

実行しようとしているタスクを実行する TableAdapter `DbDirect` メソッドを呼び出します。

### <a name="to-insert-new-records-directly-into-a-database"></a>新しいレコードをデータベースに直接挿入するには

- TableAdapter の `Insert` メソッドを呼び出し、各列の値をパラメーターとして渡します。 次の手順では、例として、Northwind データベースの `Region` テーブルを使用します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

### <a name="to-update-records-directly-in-a-database"></a>データベース内のレコードを直接更新するには

- TableAdapter の `Update` メソッドを呼び出し、各列の新しい値と元の値をパラメーターとして渡します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet18":::

### <a name="to-delete-records-directly-from-a-database"></a>データベースから直接レコードを削除するには

- TableAdapter の `Delete` メソッドを呼び出し、各列の値を `Delete` メソッドのパラメーターとして渡します。 次の手順では、例として、Northwind データベースの `Region` テーブルを使用します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet21":::

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
