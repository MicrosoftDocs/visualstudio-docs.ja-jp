---
title: データセットのデータの検証
description: データセットのデータを検証する方法について説明します。 データを検証するには、データ オブジェクトに入力された値が、データセットのスキーマ内の制約に準拠していることを確認する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DataTable.ColumnChanging
- System.Data.DataTable.ColumnChanging
- System.Data.DataTable.RowChanging
- DataTable.RowChanging
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data validation, datasets
- data validation
- validating data, datasets
- updating datasets, validating data
ms.assetid: 79500596-1e4d-478e-a991-a636fd73a622
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 82cfcf1ce030cfe597c3ae7bfe85c528184c548a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215670"
---
# <a name="validate-data-in-datasets"></a>データセットのデータの検証
データの検証とは、データ オブジェクトに入力される値が、データセットのスキーマ内の制約に準拠していることを確認するプロセスのことです。 また、検証プロセスでは、これらの値が、アプリケーションに対して設定されている規則に従っているかどうかも確認されます。 データの検証は、基になるデータベースに更新を送信する前に実行することをお勧めします。 そうすることで、エラーを減らせるだけでなく、アプリケーションとデータベースの間で生じる可能性のある、ラウンド トリップの回数も減らせます。

データセットに書き込まれようとしてるデータが有効であるかどうかは、データセット自体に検証チェックを組み込むことによって確認できます。 データセットでは、更新の実行方法 (フォーム内のコントロールによって直接実行されるか、コンポーネント内で実行されるか、またはその他の方法で実行されるか) に関係なく、データを確認できます。 データセットは (データベース バックエンドとは違って) アプリケーションの一部であるため、アプリケーション固有の検証を構築するための論理的な場所となります。

アプリケーションに検証を追加するための最適な場所は、データセットの部分クラス ファイルです。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] または [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] で、**データセット デザイナー** を開き、検証を作成する列またはテーブルをダブルクリックします。 この操作により、<xref:System.Data.DataTable.ColumnChanging> または <xref:System.Data.DataTable.RowChanging> イベント ハンドラーが自動的に作成されます。

## <a name="validate-data"></a>データの検証
データセット内での検証は、次の方法で実現されます。

- アプリケーション固有の検証を独自に作成して、個々のデータ列の変更時にその値をチェックできるようにする。 詳細については、「[方法: 列の変更時にデータを検証する](validate-data-in-datasets.md)」を参照してください。

- アプリケーション固有の検証を独自に作成して、データ行全体が変更される際に、データの値をチェックできるようにする。 詳細については、「[方法: 行の変更時にデータを検証する](validate-data-in-datasets.md)」を参照してください。

- データセットの実際のスキーマ定義の一部として、キー、一意の制約などを作成する。

- <xref:System.Data.DataColumn> オブジェクトのプロパティ (<xref:System.Data.DataColumn.MaxLength%2A>、<xref:System.Data.DataColumn.AllowDBNull%2A>、<xref:System.Data.DataColumn.Unique%2A> など) を設定する。

レコードで変更が発生すると、<xref:System.Data.DataTable> オブジェクトによっていくつかのイベントが発生します。

- <xref:System.Data.DataTable.ColumnChanging> および <xref:System.Data.DataTable.ColumnChanged> イベントは、個々の列の変更時と変更後にそれぞれ発生します。 <xref:System.Data.DataTable.ColumnChanging> イベントは、特定の列の変更を検証する場合に便利です。 提案された変更に関する情報は、イベントの引数として渡されます。
- <xref:System.Data.DataTable.RowChanging> および <xref:System.Data.DataTable.RowChanged> イベントは、行の変更時と変更後にそれぞれ発生します。 <xref:System.Data.DataTable.RowChanging> イベントの方がより一般的です。 これは、行のどこかで変更が発生していることを示すもので、どの列が変更されたかはわかりません。

既定では、列が変更されるたびに、4 つのイベントが発生することになります。 まずは、変更されようとしている列の <xref:System.Data.DataTable.ColumnChanging> および <xref:System.Data.DataTable.ColumnChanged> イベントです。 次に、<xref:System.Data.DataTable.RowChanging> および <xref:System.Data.DataTable.RowChanged> イベントです。 行に対して複数の変更が行われようとしている場合は、各変更に対してイベントが発生します。

> [!NOTE]
> データ行の <xref:System.Data.DataRow.BeginEdit%2A> メソッドは、個々の列が変更された後、<xref:System.Data.DataTable.RowChanging> イベントと <xref:System.Data.DataTable.RowChanged> イベントをオフにします。 その場合、イベントは <xref:System.Data.DataRow.EndEdit%2A> メソッドが呼び出されるまで発生しません。その際、<xref:System.Data.DataTable.RowChanging> イベントと <xref:System.Data.DataTable.RowChanged> イベントが 1 回だけ発生します。 詳細については、「[データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)」を参照してください。

どのイベントを選択するかは、検証をどの粒度で行うかによって決まってきます。 列が変更されたとき、すぐにエラーをキャッチすることが重要な場合は、<xref:System.Data.DataTable.ColumnChanging> イベントを使って検証を作成します。 それ以外の場合は、<xref:System.Data.DataTable.RowChanging> イベントを使用します。その場合、一度に複数のエラーがキャッチされる可能性があります。 また、データが構造化されていて、ある列の値が別の列の内容に基づいて検証される場合は、<xref:System.Data.DataTable.RowChanging> イベント中に検証を実行します。

レコードが更新されると、<xref:System.Data.DataTable> オブジェクトによってイベントが発生します。これらに対しては、変更の発生時と発生後に応答することができます。

アプリケーションで型指定されたデータセットが使われる場合は、厳密に型指定されたイベント ハンドラーを作成できます。 これにより、型指定された 4 つのイベント (`dataTableNameRowChanging`、`dataTableNameRowChanged`、`dataTableNameRowDeleting`、および `dataTableNameRowDeleted`) が追加されるので、それらに対してハンドラーを作成できます。 これらの型指定されたイベント ハンドラーでは、テーブルの列名を含んだ引数が渡されます。これにより、コードの記述と読み取りが容易になります。

## <a name="data-update-events"></a>データ更新イベント

|event|説明|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|列の値が変更されようとしています。 このイベントでは、行と列、そして提案された新しい値が渡されます。|
|<xref:System.Data.DataTable.ColumnChanged>|列の値が変更されました。 このイベントでは、行と列、そして提案された値が渡されます。|
|<xref:System.Data.DataTable.RowChanging>|<xref:System.Data.DataRow> オブジェクトに対して行われた変更が、データセットにコミットされようとしています。 <xref:System.Data.DataRow.BeginEdit%2A> メソッドを呼び出していない場合は、列が変更されるたび、<xref:System.Data.DataTable.ColumnChanging> イベントの発生直後に <xref:System.Data.DataTable.RowChanging> イベントが発生します。 変更を加える前に <xref:System.Data.DataRow.BeginEdit%2A> を呼び出した場合、<xref:System.Data.DataTable.RowChanging> イベントは、<xref:System.Data.DataRow.EndEdit%2A> メソッドを呼び出したときにのみ発生します。<br /><br /> このイベントでは、行と共に、実行されようとしているアクションの種類 (変更、挿入など) を示す値が渡されます。|
|<xref:System.Data.DataTable.RowChanged>|行が変更されました。 このイベントでは、行と共に、実行されようとしているアクションの種類 (変更、挿入など) を示す値が渡されます。|
|<xref:System.Data.DataTable.RowDeleting>|行が削除されようとしています。 このイベントでは、行と共に、実行されようとしているアクションの種類 (削除) を示す値が渡されます。|
|<xref:System.Data.DataTable.RowDeleted>|行が削除されました。 このイベントでは、行と共に、実行されようとしているアクションの種類 (削除) を示す値が渡されます。|

<xref:System.Data.DataTable.ColumnChanging>、<xref:System.Data.DataTable.RowChanging>、および <xref:System.Data.DataTable.RowDeleting> イベントは、更新プロセス中に発生します。 これらのイベントは、データを検証したり、その他の種類の処理を実行するために使用できます。 これらのイベント中は更新が処理中であるため、例外をスローして更新を取り消すこともできます。そうすることで、更新が完了するのを防ぐことができます。

<xref:System.Data.DataTable.ColumnChanged>、<xref:System.Data.DataTable.RowChanged>、および <xref:System.Data.DataTable.RowDeleted> イベントは、更新が正常に完了したときに発生する通知イベントです。 これらのイベントは、更新が正常に行われた後、さらにアクションを実行する場合に便利です。

## <a name="validate-data-during-column-changes"></a>列の変更時にデータを検証する

> [!NOTE]
> **データセット デザイナー** では、データセットに検証ロジックを追加できる、部分クラスが作成されます。 デザイナーによって生成されたデータセットは、部分クラス内のコードを削除したり変更したりするものではありません。

データ列の値が変更される際には、<xref:System.Data.DataTable.ColumnChanging> イベントに応答することで、データを検証することができます。 このイベントが発生すると、現在の列に対して提案されている値を含んだイベント引数 (<xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A>) が渡されます。 `e.ProposedValue` の内容に基づいて、次の操作を実行できます。

- 何もせずに、指示された値を受け入れます。

- 列変更イベント ハンドラー内から列エラー (<xref:System.Data.DataRow.SetColumnError%2A>) を設定して、提案された値を拒否します。

- オプションで <xref:System.Windows.Forms.ErrorProvider> コントロールを使用して、ユーザーにエラー メッセージを表示します。 詳細については、「[ErrorProvider コンポーネント](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)」を参照してください。

検証は、<xref:System.Data.DataTable.RowChanging> イベント中に実行することもできます。

## <a name="validate-data-during-row-changes"></a>行の変更時にデータを検証する
検証する各列にアプリケーションの要件を満たすデータが格納されていることを検証するコードを記述できます。 これを行うには、提案された値が受け入れられものである場合に、エラーが含まれていることを示すように列を設定します。 `Quantity` 列が 0 以下の場合に列エラーを設定する例を次に示します。 行変更イベント ハンドラーは、次のように記述します。

### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>行の変更時にデータを検証するには (Visual Basic)

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「[チュートリアル: データセット デザイナーを使用したデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. 検証するテーブルのタイトル バーをダブルクリックします。 この操作により、データセットの部分クラス ファイルに <xref:System.Data.DataTable.RowChanging> の <xref:System.Data.DataTable> イベント ハンドラーが自動的に作成されます。

    > [!TIP]
    > テーブル名の左側をダブルクリックして、行変更イベント ハンドラーを作成します。 テーブル名をダブルクリックすると、名前を編集できます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataValidating/VB/NorthwindDataSet.vb" id="Snippet3":::

### <a name="to-validate-data-when-a-row-changes-c"></a>行の変更時にデータ検証するには (C#)

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「[チュートリアル: データセット デザイナーを使用したデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. 検証するテーブルのタイトル バーをダブルクリックします。 この操作により、<xref:System.Data.DataTable> の部分クラス ファイルが作成されます。

    > [!NOTE]
    > **データセット デザイナー** では、<xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーが自動作成されません。 <xref:System.Data.DataTable.RowChanging> イベントを処理するメソッドを作成し、そのイベントをフックするコードをテーブルの初期化メソッドで実行する必要があります。

3. 部分クラスに次のコードをコピーします。

    ```csharp
    public override void EndInit()
    {
        base.EndInit();
        Order_DetailsRowChanging += TestRowChangeEvent;
    }

    public void TestRowChangeEvent(object sender, Order_DetailsRowChangeEvent e)
    {
        if ((short)e.Row.Quantity <= 0)
        {
            e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
        }
        else
        {
            e.Row.SetColumnError("Quantity", "");
        }
    }
    ```

## <a name="to-retrieve-changed-rows"></a>変更された行を取得する
データ テーブルの各行には、<xref:System.Data.DataRowState> 列挙体の値を使ってその行の現在の状態を追跡する、<xref:System.Data.DataRow.RowState%2A> プロパティがあります。 <xref:System.Data.DataSet> または <xref:System.Data.DataTable> の `GetChanges` メソッドを呼び出すと、データセットやデータ テーブルから変更された行を返すことができます。 データセットの <xref:System.Data.DataSet.HasChanges%2A> メソッドを呼び出せば、`GetChanges` を呼び出す前に、変更が存在するかどうかを確認できます。

> [!NOTE]
> (<xref:System.Data.DataSet.AcceptChanges%2A> メソッドを呼び出して) データセットやデータ テーブルに変更をコミットすると、`GetChanges` メソッドはデータを返さなくなります。 変更された行をアプリケーションで処理する必要がある場合は、`AcceptChanges` メソッドを呼び出す前に変更を処理する必要があります。

データセットまたはデータ テーブルの <xref:System.Data.DataSet.GetChanges%2A> メソッドを呼び出すと、変更されたレコードのみを含んだ、新しいデータセットまたはデータ テーブルが返されます。 新しいレコードのみ、または変更されたレコードのみを取得するなど、特定のレコードを取得したい場合は、<xref:System.Data.DataRowState> 列挙体の値を `GetChanges` メソッドへのパラメーターとして渡すことができます。

異なるバージョンの行 (たとえば、行を処理する前の元の値) にアクセスするには、<xref:System.Data.DataRowVersion> 列挙体を使用します。

### <a name="to-get-all-changed-records-from-a-dataset"></a>データセットから変更されたすべてのレコードを取得するには

- データセットの <xref:System.Data.DataSet.GetChanges%2A> メソッドを呼び出します。

     次の例では、`changedRecords` という新しいデータセットを作成し、`dataSet1` という別のデータセットから、変更されたすべてのレコードを設定します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet14":::

### <a name="to-get-all-changed-records-from-a-data-table"></a>データ テーブルから変更されたすべてのレコードを取得するには

- DataTable の <xref:System.Data.DataTable.GetChanges%2A> メソッドを呼び出します。

     次の例では、`changedRecordsTable` という新しいデータ テーブルを作成し、`dataTable1` という別のデータ テーブルから、変更されたすべてのレコードを設定します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet15":::

### <a name="to-get-all-records-that-have-a-specific-row-state"></a>行が特定の状態にあるすべてのレコードを取得するには

- データセットまたはデータ テーブルの `GetChanges` メソッドを呼び出し、<xref:System.Data.DataRowState> 列挙値を引数として渡します。

     次の例は、`addedRecords` という新しいデータセットを作成し、`dataSet1` データセットに追加されたレコードのみを設定する方法を示しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet16":::

     次の例は、`Customers` テーブルに最近追加されたすべてのレコードを返す方法を示しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet17":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet17":::

## <a name="access-the-original-version-of-a-datarow"></a>DataRow の元のバージョンにアクセスする
データ行を変更すると、データセットにその行の元のバージョン (<xref:System.Data.DataRowVersion.Original>) と新しいバージョン (<xref:System.Data.DataRowVersion.Current>) が保存されます。 たとえば、`AcceptChanges` メソッドを呼び出す前にレコードの別のバージョン (<xref:System.Data.DataRowVersion> 列挙定数で定義) にアクセスし、そのバージョンに応じて変更を処理できます。

> [!NOTE]
> 別のバージョンの行が存在するのは、その行が編集されてから `AcceptChanges` メソッドが呼び出されるまでの間です。 `AcceptChanges` メソッドの呼び出し後は、現在のバージョンと元のバージョンが同じになります。

<xref:System.Data.DataRowVersion> 値を列インデックス (文字列である列名) と共に渡すと、その列の特定の行バージョンから値が返されます。 変更された列は、<xref:System.Data.DataTable.ColumnChanging> イベントと <xref:System.Data.DataTable.ColumnChanged> イベントの発生時に識別されます。 検証目的で複数の行バージョンを検査するには、これが最適なタイミングです。 ただし、一時的に制約を中断しているときはこれらのイベントは発生しないため、変更された列をプログラムで識別する必要があります。 <xref:System.Data.DataTable.Columns%2A> コレクションを反復処理し、異なる <xref:System.Data.DataRowVersion> 値を比較することにより変更された列を識別できます。

### <a name="to-get-the-original-version-of-a-record"></a>レコードの元のバージョンを取得するには

- 取得する行の <xref:System.Data.DataRowVersion> を渡して列の値にアクセスします。

     次の例は、<xref:System.Data.DataRowVersion> 値を使って、<xref:System.Data.DataRow> の `CompanyName` フィールドの元の値を取得する方法を示しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet21":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet21":::

## <a name="access-the-current-version-of-a-datarow"></a>DataRow の現在のバージョンにアクセスする

### <a name="to-get-the-current-version-of-a-record"></a>レコードの現在のバージョンを取得するには

- 列の値にアクセスした後、どのバージョンの行を取得するかを示すインデックスに、パラメーターを追加します。

     次の例は、<xref:System.Data.DataRowVersion> 値を使って、<xref:System.Data.DataRow> の `CompanyName` フィールドの現在の値を取得する方法を示しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet22":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet22":::

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [方法: Windows フォーム DataGridView コントロールのデータを検証する](/dotnet/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control)
- [方法: Windows フォーム ErrorProvider コンポーネントを使用してフォーム妥当性検査でエラー アイコンを表示する](/dotnet/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider)
