---
title: データセットのデータの編集
description: データセットのデータを編集する方法について説明します。 データセット行を編集する、新しい行をデータセットに挿入する、変更された行があるかどうかを確認する、およびエラーのある行を特定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 38ceec2cafd3476342d9319d9b5d034564759fad
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215904"
---
# <a name="edit-data-in-datasets"></a>データセットのデータの編集
データ テーブル内のデータは、任意のデータベースのテーブルのデータを編集するのとほとんど同様に編集できます。 このプロセスには、テーブル内のレコードの挿入、更新、および削除を含めることができます。 データバインド フォームで、ユーザーが編集できるフィールドを指定できます。 このような場合、後で変更をデータベースに返送できるように、データ バインディング インフラストラクチャによって、すべての変更追跡が処理されます。 プログラムによってデータを編集し、それらの変更をデータベースに返送する場合は、自動的に変更の追跡を行うオブジェクトとメソッドを使用する必要があります。

実際のデータを変更するだけでなく、<xref:System.Data.DataTable> をクエリして、特定のデータ行を返すこともできます。 たとえば、個々の行、特定のバージョンの行 (元の列と提案された行)、変更された行、またはエラーが発生した行に対してクエリできます。

## <a name="to-edit-rows-in-a-dataset"></a>データセット内の行を編集するには
<xref:System.Data.DataTable> の既存の行を編集するには、編集する <xref:System.Data.DataRow> を検索し、更新した値を目的の列に割り当てる必要があります。

編集する行のインデックスがわからない場合は、`FindBy` メソッドを使用して、主キーで検索します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet3":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet3":::

行インデックスがわかっている場合は、次のように行にアクセスして編集できます。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet5":::

## <a name="to-insert-new-rows-into-a-dataset"></a>データセットに新しい行を挿入するには
データバインド コントロールを使用するアプリケーションでは、通常 [BindingNavigator コントロール](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)の **[新規追加]** ボタンを使用して、新しいレコードを追加します。

新しいレコードをデータセットに手動で追加するには、DataTable に対してメソッドを呼び出して、新しいデータ行を作成します。 次に、<xref:System.Data.DataTable> の <xref:System.Data.DataRow> コレクション (<xref:System.Data.DataTable.Rows%2A>) に行を追加します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet1":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet1":::

データセットで、データ ソースに更新を送信するために必要な情報を保持するには、<xref:System.Data.DataRow.Delete%2A> メソッドを使用して、データ テーブル内の行を削除します。 たとえば、アプリケーションで TableAdapter (または <xref:System.Data.Common.DataAdapter>) を使用している場合、TableAdapter の `Update` メソッドによって、<xref:System.Data.DataRow.RowState%2A> が <xref:System.Data.DataRowState.Deleted> であるデータベース内の行を削除します。

アプリケーションでデータ ソースに更新を返送する必要がない場合は、データ行コレクションに直接アクセスして、レコードを削除できます (<xref:System.Data.DataRowCollection.Remove%2A>)。

#### <a name="to-delete-records-from-a-data-table"></a>データ テーブルからレコードを削除するには

- <xref:System.Data.DataRow> の <xref:System.Data.DataRow.Delete%2A> メソッドを呼び出します。

     このメソッドでは、物理的にレコードが削除されません。 代わりに、レコードが削除対象としてマークされます。

    > [!NOTE]
    > <xref:System.Data.DataRowCollection> のカウント プロパティを取得すると、結果のカウントには、削除対象としてマークされたレコードが含まれます。 削除対象としてマークされていないレコードの正確なカウントを取得するには、コレクションをループ処理して、各レコードの <xref:System.Data.DataRow.RowState%2A> プロパティを調べます。 (削除対象としてマークされたレコードは、<xref:System.Data.DataRow.RowState%2A> が <xref:System.Data.DataRowState.Deleted> になっています)。または、行の状態に基づいてフィルター処理するデータセットのデータ ビューを作成し、そこからカウント プロパティを取得することもできます。

次の例に、<xref:System.Data.DataRow.Delete%2A> メソッドを呼び出して、`Customers` テーブルの最初の行を削除済みとしてマークする方法を示します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet8":::

## <a name="determine-if-there-are-changed-rows"></a>変更された行があるかどうかを判断する
データセット内のレコードを変更すると、その変更をコミットするまで変更情報が保持されます。 データセットまたはデータ テーブルの `AcceptChanges` メソッドを呼び出すか、TableAdapter またはデータ アダプターの `Update` メソッドを呼び出す場合、変更をコミットします。

変更は各データ行で 2 とおりの方法で追跡されます。

- 各データ行には、その <xref:System.Data.DataRow.RowState%2A> に関連する情報 (<xref:System.Data.DataRowState.Added>、<xref:System.Data.DataRowState.Modified>、<xref:System.Data.DataRowState.Deleted>、<xref:System.Data.DataRowState.Unchanged> など) の情報が含まれます。

- 変更された各データ行には、その行の複数のバージョン (<xref:System.Data.DataRowVersion>)、つまり元のバージョン (変更前) と現在のバージョン (変更後) が含まれます。 変更が保留されている期間 (<xref:System.Data.DataTable.RowChanging> イベントに応答できる期間) は、3 つ目のバージョン (提案されたバージョン) も利用できます。

データセットが変更された場合、データセットの <xref:System.Data.DataSet.HasChanges%2A> メソッドでは、`true` が返されます。 変更された行が存在することを確認した後は、`GetChanges` または <xref:System.Data.DataSet> の <xref:System.Data.DataTable> メソッドを呼び出して、変更された一連の行を取得できます。

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>行が変更されたかどうかを確認するには

- データセットの <xref:System.Data.DataSet.HasChanges%2A> メソッドを呼び出し、変更された行があるかどうかをチェックします。

<xref:System.Data.DataSet.HasChanges%2A> メソッドから返された値をチェックし、`NorthwindDataset1` という名前のデータセットが変更された行があるかどうかを確認する方法を次の例に示します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet12":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet12":::

## <a name="determine-the-type-of-changes"></a>変更の種類を確認する
<xref:System.Data.DataRowState> 列挙の値を <xref:System.Data.DataSet.HasChanges%2A> メソッドに渡すことにより、データセットに加えられた変更の種類を確認することもできます。

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>行への変更の種類を確認するには

- <xref:System.Data.DataRowState> 値を <xref:System.Data.DataSet.HasChanges%2A> メソッドに渡します。

次の例に、`NorthwindDataset1` という名前のデータセットを確認し、新しく追加された行があるかどうかを判断する方法を示します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet13":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet13":::

## <a name="to-locate-rows-that-have-errors"></a>エラーが発生している行を見つけるには
データの個々の列と行を操作している場合に、エラーが発生することがあります。 `HasErrors` プロパティをチェックして、<xref:System.Data.DataSet>、<xref:System.Data.DataTable>、または <xref:System.Data.DataRow> にエラーが存在するかどうかを確認できます。

1. `HasErrors` プロパティをチェックして、データセットに何らかのエラーがあるかどうかを確認します。

2. `HasErrors` プロパティが `true` の場合は、テーブルのコレクションを反復処理し、次に行を反復処理して、エラーのある行を見つけます。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet23":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet23":::

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
