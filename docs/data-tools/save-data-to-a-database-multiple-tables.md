---
title: データベースへのデータの保存 (複数テーブル)
description: このチュートリアルでは、Visual Studio のデータセット ツールを使用して、複数テーブルのデータをデータベースに保存します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 6f4b174e10eae63044c547d8ed87c46db03d23c6
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216047"
---
# <a name="save-data-to-a-database-multiple-tables"></a>データベースへのデータの保存 (複数テーブル)

アプリケーション開発における最も一般的なシナリオの 1 つに、Windows アプリケーションのフォームにデータを表示して編集し、更新したデータをデータベースに返送する操作があります。 このチュートリアルでは、2 つの関連するテーブルのデータを表示するフォームを作成し、レコードを編集して変更内容をデータベースに保存する方法を示します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。

アプリケーション内のデータをデータベースに保存するには、TableAdapter の `Update` メソッドを呼び出します。 **[データ ソース]** ウィンドウからフォームにテーブルをドラッグすると、データを保存するために必要なコードが自動的に追加されます。 その他のテーブルをフォームに追加する場合は、このコードを手動で追加する必要があります。 ここでは、複数のテーブルから更新を保存するコードを追加する手順を示します。

このチュートリアルでは、以下のタスクを行います。

- [データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を使用して、アプリケーションでデータ ソースの作成と構成を行います。

- [[データ ソース] ウィンドウ](add-new-data-sources.md#data-sources-window)の項目のコントロールを設定します。 詳細については、「[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」をご覧ください。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

- データセットの各テーブルのいくつかのレコードを変更します。

- データセット内の更新されたデータをデータベースに返送するコードを変更します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-the-windows-forms-application"></a>Windows フォーム アプリケーションを作成する

C# または Visual Basic 用の新しい **Windows フォーム アプリ** プロジェクトを作成します。 プロジェクトに **UpdateMultipleTablesWalkthrough** という名前を付けます。

## <a name="create-the-data-source"></a>データ ソースを作成する

この手順では、**データ ソース構成ウィザード** を使用して、Northwind データベースからデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプル データベースの設定の詳細については、「[方法 : サンプル データベースをインストールする](../data-tools/installing-database-systems-tools-and-samples.md)」を参照してください。

1. **[データ]** メニューで、 **[データ ソースの表示]** を選択します。

   **[データ ソース]** ウィンドウが開きます。

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を起動します。

3. **[データソースの種類を選択]** 画面で、 **[データベース]** 、 **[次へ]** の順に選択します。

4. **[データ接続の選択]** 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         または

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを開きます。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、 **[次へ]** を選択します。

6. **[アプリケーション構成ファイルに接続文字列を保存]** で、 **[次へ]** を選択します。

7. **[データベース オブジェクトの選択]** 画面で、 **[テーブル]** ノードを展開します。

8. **Customers** テーブルと **Orders** テーブルを選択し、 **[完了]** を選択します。

     自分のプロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウにテーブルが表示されます。

## <a name="set-the-controls-to-be-created"></a>作成するコントロールを設定する

このチュートリアルでは、データが個別のコントロールに表示される **詳細** レイアウトで、`Customers` テーブル内のデータを表示します。 `Orders` テーブルのデータは、<xref:System.Windows.Forms.DataGridView> コントロール内に表示される **グリッド** レイアウトで表示します。

### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>[データ ソース] ウィンドウの項目にドロップ タイプを設定するには

1. **[データ ソース]** ウィンドウで、 **[Customers]** ノードを展開します。

2. **[Customers]** ノードで、コントロール リストの **[詳細]** を選択し、**Customers** テーブルのコントロールを個別のコントロールに変更します。 詳細については、「[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」をご覧ください。

## <a name="create-the-data-bound-form"></a>データ バインド フォームを作成する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

1. **[データ ソース]** ウィンドウから **Form1** にメインの **[Customers]** ノードをドラッグします。

     説明のラベルが付いたデータ バインド コントロールとレコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 コンポーネント トレイには、[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、`CustomersTableAdapter`、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> が表示されます。

2. **[データ ソース]** ウィンドウから **Form1** に関連する **[Orders]** ノードをドラッグします。

    > [!NOTE]
    > 関連する **[Orders]** ノードは **[Fax]** 列の下にあり、**[Customers]** ノードの子ノードです。

     レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 `OrdersTableAdapter` と <xref:System.Windows.Forms.BindingSource> がコンポーネント トレイに表示されます。

## <a name="add-code-to-update-the-database"></a>データベースを更新するコードを追加する

**Customers** TableAdapter および **Orders** TableAdapter の `Update` メソッドを呼び出して、データベースを更新できます。 既定では、<xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタンのイベント ハンドラーが、データベースへの更新を送信するフォームのコードに追加されます。 この手順によって、正しい順序で更新を送信するようにコードが変更されます。これによって、参照整合性エラーが発生する可能性がなくなります。 また、Update 呼び出しを try-catch ブロックにラップして、エラー処理も実装します。 アプリケーションの要件に適合するようにコードを変更できます。

> [!NOTE]
> わかりやすくするために、このチュートリアルではトランザクションを使用しません。 ただし、複数の関連するテーブルを更新する場合は、トランザクション内にすべての更新ロジックを含めます。 トランザクションは、データベースに対するすべての関連する変更が正常に完了した後に、変更をコミットするプロセスです。 詳しくは、「[トランザクションとコンカレンシー](/dotnet/framework/data/adonet/transactions-and-concurrency)」をご覧ください。

### <a name="to-add-update-logic-to-the-application"></a>アプリケーションに更新ロジックを追加するには

1. <xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタンを選択します。 これにより、コード エディターが開き、`bindingNavigatorSaveItem_Click` イベント ハンドラーが表示されます。

2. イベント ハンドラーのコードを、関連する TableAdapter の `Update` メソッドを呼び出すコードに置き換えます。 次のコードは、最初に、各 <xref:System.Data.DataRowState> (<xref:System.Data.DataRowState.Deleted>、<xref:System.Data.DataRowState.Added>、および <xref:System.Data.DataRowState.Modified>) の更新済み情報を保持する 3 つの一時的なデータ テーブルを作成します。 更新は正しい順序で実行されます。 コードは、次のようになります。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form4.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form4.cs" id="Snippet10":::

## <a name="test-the-application"></a>アプリケーションをテストする

1. **F5** キーを押します。

2. 各テーブルの 1 つ以上のレコードのデータを変更します。

3. **[保存]** ボタンを選択します。

4. データベースの値をチェックし、変更が保存されたことを確認します。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
