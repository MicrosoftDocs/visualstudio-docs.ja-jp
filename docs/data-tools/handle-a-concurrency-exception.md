---
title: コンカレンシー例外を処理する
description: コンカレンシー例外 (System.Data.DBConcurrencyException) を処理します。これは、2 人のユーザーが同時にデータベース内の同じデータを変更しようとしたときに発生します。
ms.custom: SEO-VS-2020
ms.date: 09/11/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: f84fbaae3273b8830cce1c39cc3e42b62e487d3e
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216242"
---
# <a name="handle-a-concurrency-exception"></a>コンカレンシー例外を処理する

2 人のユーザーが同じデータベースの同じデータを同時に変更しようとすると、コンカレンシー例外 (<xref:System.Data.DBConcurrencyException?displayProperty=fullName>) が発生します。 このチュートリアルでは、<xref:System.Data.DBConcurrencyException> をキャッチする方法、エラーの原因となった行を特定する方法、およびその処理方法を説明する Windows アプリケーションを作成します。

ここでは次の手順を実行します。

1. 新しい **Windows フォーム アプリケーション プロジェクト** を作成します。

2. Northwind の Customers テーブルに基づいて、新しいデータセットを作成します。

3. データを表示する <xref:System.Windows.Forms.DataGridView> を備えたフォームを作成します。

4. Northwind データベースの Customers テーブルからデータセットにデータを読み込みます。

5. **サーバー エクスプローラー** の **[テーブル データの表示]** 機能を使用して Customers テーブルのデータにアクセスし、レコードを変更します。

6. 同じレコードを別の値に変更し、データセットを更新し、変更内容をデータベースに書き込もうとします。これにより、コンカレンシー エラーが発生します。

7. エラーをキャッチし、操作を継続してデータベースを更新するか、または更新をキャンセルするかを判断できるように、レコードの異なるバージョンを表示します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

最初に、次のようにして新しい Windows フォーム アプリケーションを作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[Windows フォーム アプリ]** プロジェクト タイプを選択します。

4. プロジェクトに **ConcurrencyWalkthrough** という名前を付け、 **[OK]** を選択します。

     **ConcurrencyWalkthrough** プロジェクトが作成されて **ソリューション エクスプローラー** に追加され、デザイナーで新しいフォームが開きます。

## <a name="create-the-northwind-dataset"></a>Northwind データセットを作成する

次に、**NorthwindDataSet** という名前のデータセットを作成します。

1. **[データ]** メニューの **[新しいデータ ソースの追加]** を選択します。

   データ ソース構成ウィザードが開きます。

2. **[データソースの種類の選択]** 画面で、 **[データベース]** を選択します。

   ![Visual Studio のデータ ソース構成ウィザード](media/data-source-configuration-wizard.png)

3. 使用可能な接続の一覧から、Northwind サンプル データベースへの接続を選択します。 接続の一覧で接続が使用できない場合は、 **[新しい接続]** を選択します。

    > [!NOTE]
    > ローカル データベース ファイルに接続する場合は、プロジェクトにファイルを追加するかどうかをたずねるメッセージが表示されたときに **[いいえ]** を選択します。

4. **[アプリケーション構成ファイルに接続文字列を保存]** 画面で、 **[次へ]** を選択します。

5. **[テーブル]** ノードを展開し、**Customers** テーブルを選択します。 既定のデータセット名は、**NorthwindDataSet** です。

6. **[完了]** を選択して、プロジェクトにデータセットを追加します。

## <a name="create-a-data-bound-datagridview-control"></a>データ バインド DataGridView コントロールを作成する

ここでは、 **[データ ソース]** ウィンドウから Windows フォームに **Customers** 項目をドラッグして、<xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> を作成します。

1. **[データ ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データ ソースの表示]** を選択します。

2. **[データ ソース]** ウィンドウの **[NorthwindDataSet]** ノードを展開し、**Customers** テーブルを選択します。

3. テーブル ノードの下向きの矢印を選択し、ドロップダウン リストの **[DataGridView]** を選択します。

4. テーブルをフォームの空の領域にドラッグします。

     **CustomersDataGridView** という名前の <xref:System.Windows.Forms.DataGridView> コントロールと、**CustomersBindingNavigator** という名前の <xref:System.Windows.Forms.BindingNavigator> が、<xref:System.Windows.Forms.BindingSource> にバインドされているフォームに追加されます。 次に、NorthwindDataSet の Customers テーブルにバインドされます。

## <a name="test-the-form"></a>フォームをテストする

フォームをテストして、ここまでの設定が期待どおりに動作することを確認します。

1. **F5** キーを選択してアプリケーションを実行します。

     フォームは、Customers テーブルのデータが読み込まれた状態で <xref:System.Windows.Forms.DataGridView> コントロールに表示されます。

2. **[デバッグ]** メニューの **[デバッグの停止]** を選択します。

## <a name="handle-concurrency-errors"></a>コンカレンシー エラーを処理する

エラーを処理する方法は、アプリケーションを管理するそれぞれのビジネス ルールによって異なります。 このチュートリアルでは、コンカレンシー エラーを処理する方法の例として、次の方法を使用します。

アプリケーションでは、ユーザーに対して次の 3 つのバージョンのレコードが用意されます。

- データベース内の現在のレコード

- データセットに読み込まれた元のレコード

- データセット内の提案された変更

ユーザーは、提案されたバージョンでデータベースを上書きするか、更新をキャンセルし、データベースから新しい値をデータセットに再読み込むことができます。

### <a name="to-enable-the-handling-of-concurrency-errors"></a>コンカレンシー エラーを処理できるようにするには

1. カスタム エラー ハンドラーの作成

2. ユーザーに対する選択肢の表示

3. ユーザーの応答の処理

4. 更新の再送、またはデータセット内のデータのリセット

### <a name="add-code-to-handle-the-concurrency-exception"></a>コンカレンシー例外を処理するコードを追加する

更新の実行を試みると例外が発生する場合、通常は、発生した例外によって提供される情報に対して何らかの対処を行います。 このセクションでは、データベースの更新を試みるコードを追加します。 また、発生する可能性がある <xref:System.Data.DBConcurrencyException> や、その他の例外も処理します。

> [!NOTE]
> チュートリアルの後半では、`CreateMessage` メソッドと `ProcessDialogResults` メソッドを追加します。

1. `Form1_Load` メソッドの下に次のコードを追加します。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet1":::

2. 次のように `CustomersBindingNavigatorSaveItem_Click` メソッドを `UpdateDatabase` メソッドの呼び出しに置き換えます。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet2":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet2":::

### <a name="display-choices-to-the-user"></a>ユーザーに対する選択肢の表示

上のコードにより `CreateMessage` プロシージャが呼び出され、ユーザーにエラー情報が表示されます。 このチュートリアルでは、メッセージ ボックスを使用して、さまざまなバージョンのレコードをユーザーに表示します。 これにより、ユーザーは、レコードを変更内容で上書きするか、編集をキャンセルするかを選択できます。 ユーザーがメッセージ ボックスのオプションを選択する (ボタンをクリックする) と、`ProcessDialogResult` メソッドに応答が渡されます。

**コード エディター** に次のコードを追加して、メッセージを作成します。 このコードは、`UpdateDatabase` メソッドの下に入力します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet4":::

### <a name="process-the-users-response"></a>ユーザーの応答の処理

メッセージ ボックスへのユーザーの応答を処理するコードも必要です。 オプションは、データベースの現在のレコードを提案された変更内容で上書きするか、またはローカルの変更内容を破棄し、データベースの現在のレコードでデータ テーブルを更新するかのいずれかです。 ユーザーが **[はい]** を選択した場合、*preserveChanges* 引数が **true** に設定された <xref:System.Data.DataTable.Merge%2A> メソッドが呼び出されます。 この結果、レコードの元のバージョンがデータベースのレコードと一致するようになり、更新の試みは成功します。

前の手順で追加したコードの下に次のコードを追加します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet3":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet3":::

## <a name="test-the-form-behavior"></a>フォームの動作をテストする

フォームをテストして、期待どおりに動作することを確認します。 コンカレンシー違反をシミュレートするには、NorthwindDataSet にデータを読み込んだ後で、データベースのデータを変更します。

1. **F5** キーを選択してアプリケーションを実行します。

2. フォームが表示されたら、実行を継続したまま Visual Studio IDE に切り替えます。

3. **[表示]** メニューの **[サーバー エクスプローラー]** を選択します。

4. **サーバー エクスプローラー** で、アプリケーションで使用する接続を展開し、次に **[テーブル]** ノードを展開します。

5. **Customers** テーブルを右クリックし、 **[テーブル データの表示]** を選択します。

6. 最初のレコード (**ALFKI**) で、 **[ContactName]** を **[Maria Anders2]** に変更します。

    > [!NOTE]
    > 別の行に移動し、変更をコミットします。

7. ConcurrencyWalkthrough の実行フォームに切り替えます。

8. フォームの最初のレコード (**ALFKI**) で、 **[ContactName]** を **[Maria Anders1]** に変更します。

9. **[保存]** ボタンを選択します。

     コンカレンシー エラーが発生し、メッセージ ボックスが表示されます。

   **[いいえ]** を選択すると、更新がキャンセルされ、現在データベース内にある値でデータセットが更新されます。 **[はい]** を選択すると、提案された値がデータベースに書き込まれます。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
