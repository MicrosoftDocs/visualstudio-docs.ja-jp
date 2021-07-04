---
title: Web パフォーマンス テストへのデータ ソースの追加
description: データをバインドして、同じテストに異なる複数の値を指定する方法について説明します (フォーム ポスト パラメーターに異なる複数の値を指定するなど)。
ms.custom: SEO-VS-2020
ms.date: 10/03/2016
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, walkthroughs
- Web performance tests, data binding (database)
ms.assetid: 2ada376d-f168-455d-9643-6acb535360c1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: 71aa3dbf4657896093dae59451140f48f83f1622
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2021
ms.locfileid: "111761005"
---
# <a name="add-a-data-source-to-a-web-performance-test"></a>Web パフォーマンス テストへのデータ ソースの追加

データをバインドすると、同じテストに異なる複数の値を指定することができます (フォーム ポスト パラメーターに異なる複数の値を指定するなど)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

![Web パフォーマンス テストにデータをバインドする](../test/media/web_test_databinding_conceptual.png)

サンプル ASP.NET アプリを使用します。 このサンプルでは、3 種類の *.aspx* ページ (既定ページ、Red ページ、Blue ページ) を使用します。 既定のページには、Red または Blue を選択するオプション ボタン コントロールと送信ボタンが表示されます。 他の 2 種類の *.aspx* ページは非常にシンプルです。 一方には Red という名前のラベルがあり、他方には Blue という名前のラベルがあります。 既定のページで送信ボタンをクリックすると、いずれかのページが表示されます。 [ColorWebApp](https://code.msdn.microsoft.com/Sample-ColorWebApp-76ff7506) サンプルをダウンロードするか、ご自身の Web アプリケーションの手順に従うことができます。

![テストする Web アプリの実行](../test/media/web_test_databinding_runwebapp.png)

ソリューションには、Web アプリケーションのページ間を移動する Web パフォーマンス テストも含める必要があります。

![Web パフォーマンス テストが含まれたソリューション](../test/media/web_test_databinding_solution.png)

## <a name="create-a-sql-database"></a>SQL データベースを作成する

::: moniker range="vs-2017"

1. Visual Studio Enterprise をお持ちでない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページからダウンロードできます。

2. SQL データベースを作成します。

     ![新しい SQL データベースを追加する](../test/media/web_test_databinding_sql_addnewdb.png)

3. データベース プロジェクトを作成します。

     ![データベースから新しいプロジェクトを作成する](../test/media/web_test_databinding_sql_addnewdbproject.png)

4. データベース プロジェクトにテーブルを追加します。

     ![データベース プロジェクトに新しいテーブルを追加する](../test/media/web_test_databinding_sql_addnewdbtablename.png)

5. フィールドをテーブルに追加します。

     ![テーブルにフィールドを追加する](../test/media/web_test_databinding_sql_addnewdbaddfields.png)

6. データベース プロジェクトを発行します。

     ![ソリューション エクスプローラーからデータベース プロジェクトを発行する](../test/media/web_test_databinding_sql_addnewdbpublish.png)

7. データをフィールドに追加します。

     ![フィールドにデータを追加する](../test/media/web_test_databinding_sql_addnewfieldsadddata.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio Enterprise をお持ちでない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページからダウンロードできます。

2. SQL データベースを作成します。

     ![新しい SQL データベースを追加する](../test/media/web_test_databinding_sql_addnewdb.png)

3. データベース プロジェクトを作成します。

     ![データベースから新しいプロジェクトを作成する](../test/media/web_test_databinding_sql_addnewdbproject.png)

4. データベース プロジェクトにテーブルを追加します。

     ![データベース プロジェクトに新しいテーブルを追加する](../test/media/web_test_databinding_sql_addnewdbtablename.png)

5. フィールドをテーブルに追加します。

     ![テーブルにフィールドを追加する](../test/media/web_test_databinding_sql_addnewdbaddfields.png)

6. データベース プロジェクトを発行します。

     ![ソリューション エクスプローラーからデータベース プロジェクトを発行する](../test/media/web_test_databinding_sql_addnewdbpublish.png)

7. データをフィールドに追加します。

     ![フィールドにデータを追加する](../test/media/web_test_databinding_sql_addnewfieldsadddata.png)

::: moniker-end

## <a name="add-the-data-source"></a>データ ソースの追加

1. データ ソースを追加します。

     ![Web パフォーマンス テストにデータ ソースを追加する](../test/media/web_test_databinding_sql_adddatasource.png)

2. データ ソースの種類を選択し、名前を指定します。

     ![データベース ソースの名前を指定する](../test/media/web_test_databinding_sql_adddatasourcedialog.png)

3. 接続を作成します。

     ![新しい接続を選択する](../test/media/web_test_databinding_sql_adddatasourcedialogconnectionnew.png)

     接続の詳細を入力します。

     ![SQL データベース接続プロパティを入力する](../test/media/web_test_databinding_sql_adddatasourcedialogconnection.png)

4. テストで使用するテーブルを選択します。

     ![データ ソースとして Color テーブルを追加する](../test/media/web_test_databinding_sql_adddatasourcedialogaddtable.png)

     テーブルがテストにバインドされます。

     ![Web パフォーマンス テストに追加されたデータ ソース ノード](../test/media/web_test_databinding_requestnodeadded_mdb.png)

5. テストを保存します。

## <a name="bind-the-data"></a>データのバインド

1. **ColorName** フィールドをバインドします。

     ![ColorName フィールドを RadioButtonList1 値にバインドする](../test/media/web_test_databinding_sql_binddatasource.png)

2. **ソリューション エクスプローラー** で *Local.testsettings* ファイルを開き、**[データ ソース行ごとに 1 つ実行]** をクリックします。

     ![テスト設定ファイルを編集します。](../test/media/web_test_databinding_sql_testsettings.png)

3. Web パフォーマンス テストを保存します。

## <a name="run-the-test-with-the-data"></a>データを使用したテストの実行

1. テストを実行します。

     ![Web パフォーマンス テストを実行してバインドを検証する](../test/media/web_test_databinding_sql_runtest.png)

     データ行ごとに 2 つの実行が表示されます。 Run 1 は *Red.aspx* ページに対する要求を送信し、Run 2 は *Blue.aspx* ページに対する要求を送信します。

     ![テスト実行結果](../test/media/web_test_databinding_sql_runresults.png)

     データ ソースにバインドすると、既定の応答 URL 規則に違反することがあります。 この場合、既定の応答 URL 規則によって Run 2 でエラーが発生しています。この規則では元のテストの記録から *Red.aspx* ページを予期していますが、データ バインディングにより *Blue.aspx* ページが指定されます。

2. **応答 URL** 検証規則を削除し、テストを再実行して、検証エラーを修正します。

     ![応答 URL の検証規則を削除する](../test/media/web_test_databinding_sql_deleteresponseurl.png)

     データ バインディングを使用した Web パフォーマンス テストが成功します。

     ![データ バインディングを使用してテストに合格する](../test/media/web_test_databinding_sql_deleteresponseurlrunresults.png)

## <a name="q--a"></a>Q & A

### <a name="q-what-databases-can-i-use-as-a-data-source"></a>Q: データ ソースとして使用できるのはどのようなデータベースですか。

**A:** 次のデータベースを使用できます。

- Microsoft SQL Azure

- Microsoft SQL Server 2005 以降のバージョン

- Microsoft SQL Server データベース ファイル (SQL Express を含む)

- Microsoft ODBC

- Microsoft Access ファイル (.NET Framework Data Provider for OLE DB を使用)

- Oracle 7.3、8i、9i、10g

### <a name="q-how-do-i-use-a-comma-separated-value-csv-text-file-as-a-data-source"></a>Q: コンマ区切り値 (CSV) テキスト ファイルをデータ ソースとして使用するにはどうすればよいですか。

**A:** 次の手順を実行します。

1. プロジェクトのデータベース成果物を整理するフォルダーを作成し、項目を追加します。

     ![データ フォルダーに新しい項目を追加する](../test/media/web_test_databinding_foldernewitem.png)

2. テキスト ファイルを作成します。

     ![新しいテキスト ファイルに ColorData.csv という名前を付ける](../test/media/web_test_databinding_foldernewitemtextfile.png)

3. このテキスト ファイルを編集して、次の内容を追加します。

    ```text
    ColorId, ColorName
    0,Red
    1,Blue
    ```

4. 「[データ ソースの追加](#add-the-data-source)」の手順を使用しますが、データ ソースとして CSV ファイルを選択します。

     ![名前を入力して CSV ファイルを選択する](../test/media/web_test_databinding_adddatasourcedialog.png)

### <a name="q-what-if-my-existing-csv-file-does-not-contain-column-headers"></a>Q: 既存の CSV ファイルに列見出しが含まれていない場合は、どうすればよいですか。

**A:** 列見出しを追加できない場合は、スキーマ記述ファイルを使用して CSV ファイルをデータベースとして扱うことができます。

1. *schema.ini* という名前の新しいテキスト ファイルを追加します。

     ![schema.ini ファイルを追加する](../test/media/web_test_databinding_schemafile.png)

2. *schema.ini* ファイルを編集して、データの構造を記述する情報を追加します。 たとえば、CSV ファイルについて記述するスキーマ ファイルは次のようになります。

    ```text
    [testdata.csv]
    ColNameHeader=False
    ```

3. データ ソースをテストに追加します。

     ![Web パフォーマンス テストにデータ ソースを追加する](../test/media/web_test_databinding_sql_adddatasource.png)

4. *schema.ini* ファイルを使用する場合は、データ ソースとして (CSV ファイルではなく) **データベース** を選択し、名前を指定します。

     ![データベース データ ソースの追加](../test/media/web_test_databinding_adddatasourcecolortext.png)

5. 新しい接続を作成します。

     ![新しい接続を選択する](../test/media/web_test_databinding_sql_adddatasourcedialogconnectionnew.png)

6. [.NET Framework Data Provider for OLE DB] をクリックします。

     ![.NET Framework OLE DB データ プロバイダーを選択する](../test/media/web_test_databinding_adddatasourcecolortext2.png)

7. **[詳細設定]** を選択します。

     ![[詳細設定] を選択する](../test/media/web_test_databinding_advanced.png)

8. "プロバイダー" プロパティについて Microsoft.Jet.OLEDB.4.0 を選択し、**[拡張プロパティ]** を Text;HDR=NO に設定します。

     ![詳細設定プロパティの適用](../test/media/web_test_databinding_advancedproperties.png)

9. スキーマ ファイルが含まれているフォルダーの名前を入力し、接続をテストします。

     ![データ フォルダーへのパスを入力する](../test/media/web_test_databinding_adddatasourcecolortext5.png)

10. 使用する CSV ファイルを選択します。

     ![テキスト ファイルを選択する](../test/media/web_test_databinding_adddatasourcecolortext6.png)

     終了すると、CSV ファイルがテーブルとして表示されます。

     ![テストに追加されたデータ ソース](../test/media/web_test_databinding_adddatasourcecolortext7.png)

### <a name="q-how-do-i-use-an-xml-file-as-a-data-source"></a>Q: XML ファイルをデータ ソースとして使うにはどうすればよいですか。

**A:** はい。

1. プロジェクトのデータベース成果物を整理するフォルダーを作成し、項目を追加します。

     ![データ フォルダーに新しい項目を追加する](../test/media/web_test_databinding_foldernewitem.png)

2. XML ファイルを作成します。

     ![ColorData.xml ファイルを追加する](../test/media/web_test_databinding_additemxmlfile.png)

3. XML ファイルを編集し、データを追加します。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <ColorData>
        <Color>
            <ColorId>0</ColorId>
            <ColorName>Red</ColorName>
        </Color>
        <Color>
            <ColorId>1</ColorId>
            <ColorName>Blue</ColorName>
        </Color>
    </ColorData>
    ```

4. 「[データ ソースの追加](#add-the-data-source)」の手順を使用しますが、データ ソースとして XML ファイルを選択します。

     ![名前を入力して XML ファイルを選択する](../test/media/web_test_databinding_adddatasourcedialogxml.png)

### <a name="q-can-i-add-data-binding-to-a-web-service-request-that-uses-soap"></a>Q: SOAP を使用する Web サービス要求にデータ バインディングを追加できますか。

**A:** はい。ただし SOAP XML を手動で変更する必要があります。

1. 要求ツリーで Web サービス要求を選択し、[プロパティ] ウィンドウの "文字列ボディ" プロパティの省略記号 (...) をクリックします。

     ![Web サービスの String Body を編集する](../test/media/web_test_databinding_webservicerequest.png)

2. 次の構文を使用して、SOAP 本体の値をデータ バインディング値に置き換えます。

    ```xml
    {{DataSourceName.TableName.ColumnName}}
    ```

    たとえば、次のようなコードがあるとします。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <CheckStatus xmlns="http://tempuri.org/">
                <userName>string</userName> <password>string</password> <orderID>int</orderID>
            </CheckStatus>
        </soap:Body>
    </soap:Envelope>
    ```

    これを次のように変更できます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <CheckStatus xmlns="http://tempuri.org/">
                <userName>{{DataSourceName.Users.Name}}</userName> <password>{{DataSourceName.Users.Password}}</password> <orderID>{{DataSourceName.Orders.OrderID}}</orderID>
            </CheckStatus>
        </soap:Body>
    </soap:Envelope>
    ```

3. テストを保存します。
