---
title: TableAdapter DBDirect メソッドを使用してデータを保存する
description: このチュートリアルでは、TableAdapter の DBDirect メソッドを使用して、データベースに対して直接 SQL ステートメントを実行します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 4539d269f27cd09f96c8633d0efd603708f1f2e1
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215774"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>TableAdapter DBDirect メソッドを使用してデータを保存する

このチュートリアルでは、TableAdapter の DBDirect メソッドを使用してデータベースに対して直接 SQL ステートメントを実行する手順について詳しく説明します。 TableAdapter の DBDirect メソッドを使用すると、データベースの更新をきめ細かいレベルで制御できます。 これらのメソッドを使用すると、(UPDATE、INSERT、および DELETE ステートメントをすべて 1 回の呼び出しで実行するオーバーロードされた `Update` メソッドとは異なり、) 必要に応じてアプリケーションで `Insert`、`Update`、および `Delete` メソッドを個別に呼び出すことによって、特定の SQL ステートメントおよびストアド プロシージャを実行できます。

このチュートリアルでは、次の作業を行う方法について説明します。

- 新しい **Windows フォーム アプリケーション** を作成します。

- [データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を使用してデータセットの作成と構成を行います。

- **[データ ソース]** ウィンドウから項目をドラッグしたときにフォーム上に作成されるコントロールを選択します。 詳細については、「[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド フォームを作成します。

- データベースに直接アクセスし、挿入、更新、および削除を実行するメソッドを追加します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-application"></a>Windows フォーム アプリケーションを作成する

最初に **Windows フォーム アプリケーション** を作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[Windows フォーム アプリ]** プロジェクト タイプを選択します。

4. プロジェクトに **TableAdapterDbDirectMethodsWalkthrough** という名前を付け、 **[OK]** をクリックします。

     **TableAdapterDbDirectMethodsWalkthrough** プロジェクトが作成されて **ソリューション エクスプローラー** に追加されます。

## <a name="create-a-data-source-from-your-database"></a>データベースからのデータ ソースの作成

この手順では、**データ ソース構成ウィザード** を使用して、Northwind サンプル データベースの `Region` テーブルに基づいてデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプル データベースの設定の詳細については、「[方法 : サンプル データベースをインストールする](../data-tools/installing-database-systems-tools-and-samples.md)」を参照してください。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. **[データ]** メニューで、 **[データ ソースの表示]** を選択します。

   **[データ ソース]** ウィンドウが開きます。

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を起動します。

3. **[データソースの種類を選択]** 画面で、 **[データベース]** 、 **[次へ]** の順に選択します。

4. **[データ接続の選択]** 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         または

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、 **[次へ]** を選択します。

6. **[アプリケーション構成ファイルに接続文字列を保存]** 画面で、 **[次へ]** を選択します。

7. **[データベース オブジェクトの選択]** 画面で、 **[テーブル]** ノードを展開します。

8. `Region` テーブルを選択し、 **[完了]** をクリックします。

     プロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウに `Region` テーブルが表示されます。

## <a name="add-controls-to-the-form-to-display-the-data"></a>データを表示するためのコントロールをフォームに追加する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

Windows フォーム上にデータ バインド コントロールを作成するには、メインの **Region** ノードを、 **[データ ソース]** ウィンドウからフォーム上にドラッグします。

レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 コンポーネント トレイには、[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、`RegionTableAdapter`、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> が表示されます。

### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>個々の TableAdapter DbDirect メソッドを呼び出すボタンを追加するには

1. **ツールボックス** から 3 つの <xref:System.Windows.Forms.Button> コントロールを **RegionDataGridView** の下の **Form1** にドラッグします。

2. 各ボタンの **[名前]** および **[テキスト]** プロパティを設定します。

    |名前|テキスト|
    |----------|----------|
    |`InsertButton`|**[挿入]**|
    |`UpdateButton`|**アップデート**|
    |`DeleteButton`|**削除**|

### <a name="to-add-code-to-insert-new-records-into-the-database"></a>データベースに新しいレコードを挿入するコードを追加するには

1. **[InsertButton]** を選択して、クリック イベントのイベント ハンドラーを作成し、コード エディターでフォームを開きます。

2. `InsertButton_Click` イベント ハンドラーを次のコードで置き換えます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet1":::

### <a name="to-add-code-to-update-records-in-the-database"></a>データベースのレコードを更新するコードを追加するには

1. **[UpdateButton]** をダブルクリックして、クリック イベントのイベント ハンドラーを作成し、コード エディターでフォームを開きます。

2. `UpdateButton_Click` イベント ハンドラーを次のコードで置き換えます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet2":::

### <a name="to-add-code-to-delete-records-from-the-database"></a>データベースからレコードを削除するためのコードを追加するには

1. **[DeleteButton]** を選択して、クリック イベントのイベント ハンドラーを作成し、コード エディターでフォームを開きます。

2. `DeleteButton_Click` イベント ハンドラーを次のコードで置き換えます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs" id="Snippet3":::

## <a name="run-the-application"></a>アプリケーションの実行

- **F5** キーを選択してアプリケーションを実行します。

- **[挿入]** ボタンをクリックし、グリッドに新しいレコードが表示されることを確認します。

- **[更新]** ボタンをクリックし、グリッドでレコードが更新されることを確認します。

- **[削除]** ボタンをクリックし、グリッドからレコードが削除されることを確認します。

## <a name="next-steps"></a>次のステップ

アプリケーションの要件に応じて、データ バインド フォームの作成後に、追加の操作を実行できます。 このチュートリアルで行うことができる拡張には次のものがあります。

- フォームに検索機能を追加します。

- **[データ ソース]** ウィンドウの **[ウィザードで DataSet を構成]** を選択して、データセットにテーブルを追加します。 関連するコードをフォームにドラッグすることによって、関連するデータを表示するコントロールを追加できます。 詳細については、[データセットのリレーションシップ](relationships-in-datasets.md)に関する記事をご覧ください。

## <a name="see-also"></a>こちらもご覧ください

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
