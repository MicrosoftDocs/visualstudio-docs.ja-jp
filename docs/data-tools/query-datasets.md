---
title: データセットのクエリ
description: クエリ データセットについて説明します。 データセットの大文字と小文字の区別について説明します。 データ テーブル内の特定の行を検索し、列の値で行を検索して、関連レコードにアクセスします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
ms.assetid: 7b1a91cf-8b5a-4fc0-ac36-0dc2d336fa1b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: c5f085cae185a48f3d41c6fa4bca5cad7afb46b3
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215800"
---
# <a name="query-datasets"></a>データセットのクエリ
データセット内の特定のレコードを検索するには、DataTable に対して `FindBy` メソッドを使用し、テーブルの Rows コレクションをループ処理する独自の foreach ステートメントを記述するか、[LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset) を使用します。

## <a name="dataset-case-sensitivity"></a>データセットの大文字と小文字の区別
データセット内では、テーブル名と列名は既定で大文字と小文字が区別されません。つまり、"Customers" というデータセット内のテーブルは "customers" として参照することもできます。 これは、SQL Server を含む多くのデータベースの名前付け規則に一致します。 SQL Server の既定の動作では、データ要素の名前を大文字と小文字のみで区別することはできません。

> [!NOTE]
> データセットとは異なり、XML ドキュメントでは大文字と小文字が区別されるため、スキーマに定義されているデータ要素の名前は大文字と小文字が区別されます。 たとえば、スキーマ プロトコルでは、"Customers" という名前のテーブルと "customers" という別のテーブルを定義できます。 これにより、大文字と小文字のみが異なる要素を含むスキーマを使用して、データセット クラスが生成される際に、名前の競合が発生する可能性があります。

ただし、大文字と小文字の区別は、データセット内でのデータの解釈方法の要因になることがあります。 たとえば、データセット テーブル内のデータをフィルター処理する場合、比較で大文字と小文字が区別されるかどうかによって、検索条件で異なる結果が返されることがあります。 フィルター処理、検索、および並べ替えの大文字と小文字の区別を制御するには、データセットの <xref:System.Data.DataSet.CaseSensitive%2A> プロパティを設定します。 データセット内のすべてのテーブルは、既定でこのプロパティの値を継承します。 (個々のテーブルごとにこのプロパティをオーバーライドするには、テーブルの <xref:System.Data.DataTable.CaseSensitive%2A> プロパティを設定します。)

## <a name="locate-a-specific-row-in-a-data-table"></a>データ テーブル内の特定の行を検索する

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>主キー値を使用して型指定されたデータセット内の行を検索するには

- 行を検索するには、テーブルの主キーを使用する厳密に型指定された `FindBy` メソッドを呼び出します。

     次の例では、`CustomerID` 列が `Customers` テーブルの主キーです。 これは、生成された `FindBy` メソッドが `FindByCustomerID` であることを意味します。 例では、生成された `FindBy` メソッドを使用して、特定の <xref:System.Data.DataRow> を変数に割り当てる方法を示します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet18":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet18":::

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>主キー値を含む型指定されていないデータセット内の行を検索するには

- <xref:System.Data.DataRowCollection> コレクションの <xref:System.Data.DataRowCollection.Find%2A> メソッドを呼び出し、主キーをパラメーターとして渡します。

     次の例は、`foundRow` という新しい行を宣言し、それに、<xref:System.Data.DataRowCollection.Find%2A> メソッドの戻り値を割り当てる方法を示しています。 主キーが見つかった場合、列インデックス 1 の内容がメッセージ ボックスに表示されます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet19":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet19":::

## <a name="find-rows-by-column-values"></a>列の値で行を検索する

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>任意の列の値に基づいて行を検索するには

- データ テーブルは、<xref:System.Data.DataTable.Select%2A> メソッドを使用して作成されます。このメソッドは、<xref:System.Data.DataTable.Select%2A> メソッドに渡された式に基づいて <xref:System.Data.DataRow> の配列を返します。 有効な式の作成の詳細については、<xref:System.Data.DataColumn.Expression%2A> プロパティに関するページの「式の構文」セクションを参照してください。

     次の例は、<xref:System.Data.DataTable> の <xref:System.Data.DataTable.Select%2A> メソッドを使用して、特定の行を見つける方法を示しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet20":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet20":::

## <a name="access-related-records"></a>関連レコードにアクセスする
データセット内のテーブルが関連付けられている場合、<xref:System.Data.DataRelation> オブジェクトによって、関連するレコードを別のテーブルで使用できるようにすることができます。 たとえば、`Customers` テーブルと `Orders` テーブルを含むデータセットを使用できるようにすることができます。

<xref:System.Data.DataRelation> オブジェクトを使用して、親テーブルで <xref:System.Data.DataRow> の <xref:System.Data.DataRow.GetChildRows%2A> メソッドを呼び出すことによって、関連するレコードを検索できます。 このメソッドによって、関連する子レコードの配列が返されます。 または、子テーブルで、<xref:System.Data.DataRow> の <xref:System.Data.DataRow.GetParentRow%2A> メソッドを呼び出すことができます。 このメソッドによって、親テーブルから単一の <xref:System.Data.DataRow> が返されます。

このページでは、型指定されたデータセットを使用する例を示します。 型指定されていないデータセット内のリレーションシップの移動については、「[DataRelation の移動](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations)」を参照してください。

> [!NOTE]
> Windows フォーム アプリケーションで作業していて、データバインディング機能を使用してデータを表示している場合は、デザイナーで生成されたフォームによって、アプリケーションに十分な機能を提供できます。 詳細については、「[Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。 具体的には、[データセット内のリレーションシップ](relationships-in-datasets.md)に関するページを参照してください。

次のコード例は、型指定されたデータセット内のリレーションシップを上下に移動する方法を示しています。 このコード例では、型指定された <xref:System.Data.DataRow> (`NorthwindDataSet.OrdersRow`) および生成された FindBy *PrimaryKey* (`FindByCustomerID`) メソッドを使用して目的の行を検索し、関連レコードを返しています。 例では、次のものがある場合にのみ、正しくコンパイルされて実行されます。

- `Customers` テーブルのある `NorthwindDataSet` という名前のデータセットのインスタンス。

- `Orders` テーブル。

- 2 つのテーブルを関連付ける `FK_Orders_Customers` という名前のリレーションシップ。

また、両方のテーブルに、返されるすべてのレコードのデータが格納される必要があります。

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>選択した親レコードの子レコードを返すには

- 特定の `Customers` データ行の <xref:System.Data.DataRow.GetChildRows%2A> メソッドを呼び出し、`Orders` テーブルから行の配列を返します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet6":::

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>選択した子レコードの親レコードを返すには

- 特定の `Orders` データ行の <xref:System.Data.DataRow.GetParentRow%2A> メソッドを呼び出し、`Customers` テーブルから単一の行を返します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet7":::

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
