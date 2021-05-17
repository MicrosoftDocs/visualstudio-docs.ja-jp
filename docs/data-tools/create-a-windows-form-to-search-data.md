---
title: データを検索する Windows フォームを作成する
description: データを検索するための Windows フォームを作成する方法の例をお読みください。 Windows フォーム アプリケーション、データ ソース、およびフォームを作成します。 パラメーター化を追加します。 アプリをテストします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Windows Forms, searching data
- Windows Forms, displaying data
- parameters, displaying filtered data
- data [Visual Studio], parameterizing queries
- data [Visual Studio], searching
ms.assetid: 65ca79a9-7458-466c-af55-978cd24c549e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: eb6e5a1ba304627c08828b6ad7bff7f6accd3980
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859113"
---
# <a name="create-a-windows-form-to-search-data"></a>データを検索する Windows フォームを作成する

一般的なアプリケーションのシナリオでは、選択したデータをフォーム上に表示します。 たとえば、特定の顧客の注文、特定の注文の明細などを表示する場合があります。 このシナリオでは、ユーザーがフォームに情報を入力した後、ユーザーの入力をパラメーターとして使用してクエリが実行されます。つまり、パラメーター クエリに基づいてデータが選択されます。 クエリは、ユーザーが入力した条件を満たすデータのみを返します。 ここでは、特定の都市にいる顧客を返すクエリを作成する方法、およびユーザー インターフェイスを変更して、ユーザーが都市の名前を入力してクエリを実行するボタンを押すことができるようにする方法について説明します。

パラメーター クエリを使用することにより、データベースが最も得意とする作業 (レコードの迅速なフィルター処理) をデータベースに任せることができるため、アプリケーションの効率が高まります。 一方、データベース テーブル全体を要求し、それをネットワークを通じて転送し、アプリケーション ロジックを使用して必要なレコードを見つける場合は、アプリケーションが低速になり、効率が低下する可能性があります。

**[検索条件ビルダー]** ダイアログ ボックスを使って、TableAdapter (およびパラメーター値を受け取ってクエリを実行するコントロール) にパラメーター クエリを追加できます。 このダイアログ ボックスを開くには、**[データ]** メニュー (または TableAdapter スマート タグ) の **[クエリの追加]** をクリックします。

このチュートリアルでは、以下のタスクを行います。

- **データ ソース構成ウィザード** を使用して、アプリケーションでデータ ソースの作成と構成を行います。

- **[データ ソース]** ウィンドウの項目にドロップ タイプを設定します。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグし、データを表示するコントロールを作成します。

- データを表示するコントロールをフォームに追加します。

- **[検索条件ビルダー]** ダイアログ ボックスを終了します。

- フォームにパラメーターを入力し、パラメーター クエリを実行します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、**Visual Studio インストーラー** の **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-the-windows-forms-application"></a>Windows フォーム アプリケーションを作成する

C# または Visual Basic 用の新しい **Windows フォーム アプリ** プロジェクトを作成します。 プロジェクトに **WindowsSearchForm** という名前を付けます。

## <a name="create-the-data-source"></a>データ ソースを作成する

この手順では、**データ ソース構成** ウィザードを使用して、データベースからデータ ソースを作成します。

1. **[データ ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データ ソースの表示]** をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして **データ ソース構成** ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

4. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

8. **Customers** テーブルを選択し、**[完了]** をクリックします。

     プロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウに **Customers** テーブルが表示されます。

## <a name="create-the-form"></a>フォームを作成する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

1. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

2. **[Customers]** ノードを **[データ ソース]** ウィンドウからフォームにドラッグします。

     <xref:System.Windows.Forms.DataGridView> と、レコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォーム上に表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

## <a name="add-parameterization-search-functionality-to-the-query"></a>クエリへのパラメーター (検索機能) の追加

**[検索条件ビルダー]** ダイアログ ボックスを使用して、元のクエリに WHERE 句を追加できます。

1. <xref:System.Windows.Forms.DataGridView> コントロールを選択し、**[データ]** メニューの **[クエリの追加]** をクリックします。

2. **[検索条件ビルダー]** ダイアログ ボックスの **[新しいクエリ名]** 領域に **FillByCity** と入力します。

3. **[クエリ テキスト]** 領域でクエリに `WHERE City = @City` を追加します。

     クエリは次のようになります。

     ```sql
     SELECT CustomerID, CompanyName, ContactName, ContactTitle,
          Address, City, Region, PostalCode, Country, Phone, Fax
     FROM Customers
     WHERE City = @City
     ```

    > [!NOTE]
    > Access データ ソースと OLE DB データ ソースは疑問符 ("?") を使用してパラメーターを表すため、WHERE 句は `WHERE City = ?` のようになります。

4. **[OK]** をクリックして **[検索条件ビルダー]** ダイアログ ボックスを閉じます。

     **FillByCityToolStrip** がフォームに追加されます。

## <a name="test-the-application"></a>アプリケーションをテストする

アプリケーションを実行すると、フォームが開き、パラメーターを入力として取得できる状態になります。

1. **F5** キーを押してアプリケーションを実行します。

2. **[City]** ボックスに「**London**」と入力し、**[FillByCity]** をクリックします。

     データ グリッドに、条件を満たす顧客が取得されます。 この例では、**[City]** 列の値が **London** の顧客だけがデータ グリッドに表示されます。

## <a name="next-steps"></a>次のステップ

アプリケーションの要件に応じて、パラメーター付きのフォームを作成した後に、追加の操作を実行できます。 このチュートリアルで行うことができる拡張には次のものがあります。

- 関連するデータを表示するコントロールを追加します。 詳細については、[データセットのリレーションシップ](relationships-in-datasets.md)に関する記事をご覧ください。

- データセットを編集し、データベース オブジェクトの追加または削除を行います。 詳細については、[データセットの作成と構成](../data-tools/create-and-configure-datasets-in-visual-studio.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
