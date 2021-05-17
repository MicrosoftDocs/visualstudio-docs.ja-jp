---
title: 'チュートリアル: トランザクションにデータを保存する'
description: このチュートリアルでは、Visual Studio で System.Transactions 名前空間を使用してトランザクションにデータを保存する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 09/08/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: a5933a8713a1d4b371672be83a56d0323f5043b9
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216086"
---
# <a name="walkthrough-save-data-in-a-transaction"></a>チュートリアル: トランザクションにデータを保存する

このチュートリアルでは、<xref:System.Transactions> 名前空間を使用してトランザクションにデータを保存する方法について説明します。 このチュートリアルでは、Windows フォーム アプリケーションを作成します。 データ ソース構成ウィザードを使用して、Northwind サンプル データベースに 2 つのテーブルのデータセットを作成します。 データ バインド コントロールを Windows フォームに追加し、BindingNavigator の [保存] ボタンのコードを変更して、TransactionScope 内のデータベースを更新します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 Visual Studio インストーラーで、 **.NET デスクトップ開発** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

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

4. プロジェクトに **SavingDataInATransactionWalkthrough** という名前を付け、 **[OK]** を選択します。

     **SavingDataInATransactionWalkthrough** プロジェクトが作成されて **ソリューション エクスプローラー** に追加されます。

## <a name="create-a-database-data-source"></a>データベースのデータ ソースを作成する

この手順では、**データ ソース構成ウィザード** を使用して、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルに基づいてデータ ソースを作成します。

1. **[データ ソース]** ウィンドウを開くには、 **[データ]** メニューで **[データ ソースの表示]** を選択します。

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を起動します。

3. **[データソースの種類を選択]** 画面で、 **[データベース]** 、 **[次へ]** の順に選択します。

4. **[データ接続の選択]** 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         または

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示し、Northwind データベースへの接続を作成します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、 **[次へ]** を選択します。

6. **[アプリケーション構成ファイルに接続文字列を保存]** 画面で、 **[次へ]** を選択します。

7. **[データベース オブジェクトの選択]** 画面で、 **[テーブル]** ノードを展開します。

8. `Customers` テーブルと `Orders` テーブルを選択し、 **[完了]** を選択します。

     プロジェクトに **NorthwindDataSet** が追加され、 **[データ ソース]** ウィンドウに `Customers` テーブルと `Orders` テーブルが表示されます。

## <a name="add-controls-to-the-form"></a>コントロールをフォームに追加する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

1. **[データ ソース]** ウィンドウで、 **[Customers]** ノードを展開します。

2. **[データ ソース]** ウィンドウから **Form1** にメインの **[Customers]** ノードをドラッグします。

   レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 コンポーネント トレイには、[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、`CustomersTableAdapter`、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> が表示されます。

3. 対応する **[Orders]** ノード (メインの **[Orders]** ノードではなく、 **[Fax]** 列の下の対応する子テーブル ノード) を **CustomersDataGridView** の下のフォームにドラッグします。

   <xref:System.Windows.Forms.DataGridView> がフォームに表示されます。 `OrdersTableAdapter` と <xref:System.Windows.Forms.BindingSource> がコンポーネント トレイに表示されます。

## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>System.Transactions アセンブリへの参照を追加する

トランザクションは、<xref:System.Transactions> 名前空間を使用します。 System.Transactions アセンブリへのプロジェクト参照は既定で追加されないため、手動で追加する必要があります。

### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>System.Transactions の DLL ファイルへの参照を追加するには

1. **[プロジェクト]** メニューの **[参照の追加]** を選択します。

2. **[.NET]** タブの **System.Transactions** を選択し、 **[OK]** を選択します。

     **System.Transactions** への参照がプロジェクトに追加されます。

## <a name="modify-the-code-in-the-bindingnavigators-saveitem-button"></a>BindingNavigator の SaveItem ボタンのコードを変更する

既定では、フォームに最初にドロップされるテーブルのコードは、<xref:System.Windows.Forms.BindingNavigator> の保存ボタンの `click` イベントに追加されます。 追加テーブルを更新する場合は、手動でコードを追加する必要があります。 このチュートリアルでは、[保存] ボタンのクリック イベント ハンドラーから既存の保存コードをリファクタリングします。 また、行を追加または削除する必要があるかどうかに基づいて、特定の更新機能を提供するためのメソッドもいくつか作成します。

### <a name="to-modify-the-auto-generated-save-code"></a>自動生成された保存コードを変更するには

1. **CustomerBindingNavigator** の **[保存]** ボタン (フロッピー ディスクのアイコンのボタン) を選択します。

2. `CustomersBindingNavigatorSaveItem_Click` メソッドを次のコードで置き換えます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet4":::

関連するデータへの変更を解決する順序は次のとおりです。

- 子レコードを削除します (この場合は、`Orders` テーブルからレコードを削除します)。

- 親レコードを削除します (この場合は、`Customers` テーブルからレコードを削除します)。

- 親レコードを挿入します (この場合は、`Customers` テーブルにレコードを挿入します)。

- 子レコードを挿入します (この場合は、`Orders` テーブルにレコードを挿入します)。

### <a name="to-delete-existing-orders"></a>既存の注文を削除するには

- 次の `DeleteOrders` メソッドを **Form1** に追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet5":::

### <a name="to-delete-existing-customers"></a>既存の顧客を削除するには

- 次の `DeleteCustomers` メソッドを **Form1** に追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet6":::

### <a name="to-add-new-customers"></a>新規顧客を追加するには

- 次の `AddNewCustomers` メソッドを **Form1** に追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet7":::

### <a name="to-add-new-orders"></a>新規注文を追加するには

- 次の `AddNewOrders` メソッドを **Form1** に追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet8":::

## <a name="run-the-application"></a>アプリケーションの実行

**F5** キーを押してアプリケーションを実行します。

## <a name="see-also"></a>関連項目

- [方法 : トランザクションを使用してデータを保存する](../data-tools/save-data-by-using-a-transaction.md)
- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
