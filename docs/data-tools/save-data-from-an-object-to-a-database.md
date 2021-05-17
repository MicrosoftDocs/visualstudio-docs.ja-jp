---
title: オブジェクトからデータベースにデータを保存する
description: Visual Studio の DataSet ツールを使用して、オブジェクトのデータをデータベースに保存します。 新しいレコードを保存する、既存のレコードを更新する、および既存のレコードを削除する方法を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 50debf24fa691ba74d082543b1c0bb1a27b5786e
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215787"
---
# <a name="save-data-from-an-object-to-a-database"></a>オブジェクトからデータベースにデータを保存する

オブジェクト内のデータをデータベースに保存するには、オブジェクトから TableAdapter のいずれかの DBDirect メソッド (`TableAdapter.Insert` など) に値を渡します。 詳細については、[TableAdapter](../data-tools/create-and-configure-tableadapters.md) に関するページを参照してください。

オブジェクトのコレクションのデータを保存するには、オブジェクトのコレクションをループ処理し (for-next ループなど)、TableAdapter のいずれかの `DBDirect` メソッドを使用して、各オブジェクトの値をデータベースに送信します。

既定で `DBDirect` メソッドは、データベースに対して直接実行できる TableAdapter に作成されます。 これらのメソッドは直接呼び出すことができ、更新をデータベースに送信するために、変更を調整する <xref:System.Data.DataSet> または <xref:System.Data.DataTable> オブジェクトを必要としません。

> [!NOTE]
> TableAdapter を構成する場合、メイン クエリでは、`DBDirect` メソッドを作成するための十分な情報を提供する必要があります。 たとえば、主キー列が定義されていないテーブルのデータをクエリするように TableAdapter が構成されている場合、`DBDirect` メソッドは生成されません。

|TableAdapter DBDirect メソッド|説明|
| - |-----------------|
|`TableAdapter.Insert`|データベースに新しいレコードを追加し、個々の列の値をメソッド パラメーターとして渡せるようにします。|
|`TableAdapter.Update`|データベースの既存のレコードを更新します。 `Update` メソッドは、元の列と新しい列の値をメソッドのパラメーターとして受け取ります。 元の値は元のレコードを検索するために使用され、新しい値はそのレコードを更新するために使用されます。<br /><br /> `TableAdapter.Update` メソッドは、<xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow>、または <xref:System.Data.DataRow> の配列をメソッド パラメーターとして受け取り、データベースに戻されるデータセット内の変更を調整するためにも使用されます。|
|`TableAdapter.Delete`|メソッド パラメーターとして渡された元の列の値に基づいて、データベースから既存のレコードを削除します。|

## <a name="to-save-new-records-from-an-object-to-a-database"></a>オブジェクトの新しいレコードをデータベースに保存するには

- 値を `TableAdapter.Insert` メソッドに渡して、レコードを作成します。

     次の例では、`currentCustomer` オブジェクトの値を `TableAdapter.Insert` メソッドに渡すことによって、`Customers` テーブルに新しい顧客レコードを作成し ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet23":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet23":::

## <a name="to-update-existing-records-from-an-object-to-a-database"></a>オブジェクトの既存のレコードをデータベースに更新するには

- `TableAdapter.Update` メソッドを呼び出し、レコードを更新するための新しい値を渡し、レコードを検索するための元の値を渡して、レコードを変更します。

    > [!NOTE]
    > オブジェクトでは、`Update` メソッドに渡すために元の値を保持する必要があります。 この例では、`orig` プレフィックスを持つプロパティを使用して、元の値を格納しています。

     次の例では、`Customer` オブジェクトの新しい値と元の値を `TableAdapter.Update` メソッドに渡すことによって、`Customers` テーブル内の既存のレコードを更新しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet24":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet24":::

## <a name="to-delete-existing-records-from-a-database"></a>データベースから既存のレコードを削除するには

- レコードを削除するには、`TableAdapter.Delete` メソッドを呼び出し、レコードを検索するための元の値を渡します。

    > [!NOTE]
    > オブジェクトでは、`Delete` メソッドに渡すために元の値を保持する必要があります。 この例では、`orig` プレフィックスを持つプロパティを使用して、元の値を格納しています。

     次の例では、`Customer` オブジェクトの元の値を `TableAdapter.Delete` メソッドに渡すことによって、`Customers` テーブルからレコードを削除しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet25":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet25":::

## <a name="net-security"></a>.NET セキュリティ

データベースのテーブルに対して、選択した `INSERT`、`UPDATE`、または `DELETE` を実行するアクセス許可が必要です。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
