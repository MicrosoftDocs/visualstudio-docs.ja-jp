---
title: データ バインディングでのルックアップ テーブルの使用 - Windows フォーム
description: Visual Studio で LookupBindingPropertiesAttribute クラスを使用して、ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- LookupBindingPropertiesAttribute class, examples
- user controls [Visual Basic], creating
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 796fc389a7cd7d0c587f955792a96d0f2f07a20c
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215969"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する

フォームにデータを表示する場合は、**ツールボックス** から既存のコントロールを選択するか、またはアプリケーションが標準コントロールでは提供できない機能を必要とする場合は、カスタム コントロールを記述できます。 このチュートリアルでは、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールには、データにバインドできるプロパティを 3 つ含めることができます。 このようなコントロールは、<xref:System.Windows.Forms.ComboBox> に似ています。

コントロール作成の詳細については、[デザイン時の Windows フォーム コントロールの開発](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)に関するページを参照してください。

データ バインディングのシナリオで使用するためのコントロールを作成するときは、次のいずれかのデータ バインド属性を実装する必要があります。

|データ バインディング属性の使用|
| - |
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 詳細については、「[単純なデータ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)」を参照してください。|
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 詳細については、「[複合データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)」を参照してください。|
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|

このチュートリアルでは、2 つのテーブルのデータにバインドする検索コントロールを作成します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。 検索コントロールは `Orders` テーブルの `CustomerID` フィールドにバインドされます。 この値を使用して、`Customers` テーブルから `CompanyName` が検索されます。

このチュートリアルでは、次の作業を行う方法について説明します。

- 新しい **Windows フォーム アプリケーション** を作成します。

- 新しい **ユーザー コントロール** をプロジェクトに追加します。

- ユーザー コントロールをビジュアルに設計します。

- `LookupBindingProperty` 属性を実装します。

- **データ ソース構成** ウィザードを使用してデータセットを作成します。

- **[データ ソース]** ウィンドウで **Orders** テーブルの **[CustomerID]** 列が新しいコントロールを使用するように設定します。

- フォームを作成して、新しいコントロールにデータを表示します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-app-project"></a>Windows フォーム アプリ プロジェクトを作成する

最初の手順は、**Windows フォーム アプリケーション** プロジェクトを作成することです。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[Windows フォーム アプリ]** プロジェクト タイプを選択します。

4. プロジェクトに **LookupControlWalkthrough** という名前を付け、 **[OK]** を選択します。

     **LookupControlWalkthrough** プロジェクトが作成されて **ソリューション エクスプローラー** に追加されます。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する

このチュートリアルでは **ユーザー コントロール** から検索コントロールを作成するので、**ユーザー コントロール** の項目を **LookupControlWalkthrough** プロジェクトに追加します。

1. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。

2. **[名前]** 領域に「`LookupBox`」と入力し、 **[追加]** をクリックします。

     **LookupBox** コントロールが **ソリューション エクスプローラー** に追加され、デザイナーが開きます。

## <a name="design-the-lookupbox-control"></a>LookupBox コントロールの設計

LookupBox コントロールを設計するには、**ツールボックス** からユーザー コントロールのデザイン サーフェイスに、<xref:System.Windows.Forms.ComboBox> をドラッグします。

## <a name="add-the-required-data-binding-attribute"></a>必要なデータ バインディング属性の追加

データ バインディングをサポートする検索コントロールには、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装できます。

1. **LookupBox** コントロールをコード ビューに切り替えます。 (**[表示]** メニューの **[コード]** を選択します。)

2. `LookupBox` のコードを次のコードで置き換えます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/LookupBox.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/LookupBox.cs" id="Snippet5":::

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-data-source-from-your-database"></a>データベースからのデータ ソースの作成

この手順では、**データ ソース構成** ウィザードを使用して、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルに基づいてデータ ソースを作成します。

1. **[データ ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データ ソースの表示]** をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして **データ ソース構成** ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

4. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

8. `Customers` テーブルと `Orders` テーブルを選択し、**[完了]** をクリックします。

     プロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウに `Customers` テーブルと `Orders` テーブルが表示されます。

## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>LookupBox コントロールを使用するように Orders テーブルの [CustomerID] 列を設定する

**[データ ソース]** ウィンドウでは、フォームにコントロールをドラッグする前に作成するコントロールを設定できます。

1. デザイナーで **Form1** を開きます。

2. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

3. **[Fax]** 列の下の **[Customers]** 列にある **[Orders]** ノードを展開します。

4. **[Orders]** ノードのドロップダウン矢印をクリックし、コントロール一覧の **[Details]** を選択します。

5. **[Orders]** ノードの **[CustomerID]** 列のドロップダウン矢印をクリックし、**[Customize]** をクリックします。

6. **[データ UI カスタマイズ オプション]** ダイアログ ボックスの **[関連付けられたコントロール]** の一覧の **[LookupBox]** を選択します。

7. **[OK]** をクリックします。

8. **[CustomerID]** 列のドロップダウン矢印をクリックし、**[LookupBox]** をクリックします。

## <a name="add-controls-to-the-form"></a>コントロールをフォームに追加する

**[データ ソース]** ウィンドウから **Form1** に項目をドラッグして、データ バインディング コントロールを作成します。

Windows フォームにデータ バインド コントロールを作成するには、 **[データ ソース]** ウィンドウから Windows フォームに **[Orders]** ノードをドラッグし、**LookupBox** コントロールを使用して `CustomerID` 列にデータが表示されることを確認します。

## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>Customers テーブルから CompanyName を検索するためにコントロールをバインドする

検索バインドを設定するには、 **[データ ソース]** ウィンドウでメインの **[Customers]** ノードを選択し、**Form1** の **CustomerIDLookupBox** 内のコンボ ボックスにドラッグします。

これによって、`Orders` テーブルの `CustomerID` 値を維持しながら、`Customers` テーブルの `CompanyName` を表示するためのデータ バインディングがセットアップされます。

## <a name="run-the-application"></a>アプリケーションの実行

- **F5** キーを押してアプリケーションを実行します。

- レコード間を移動し、`LookupBox` コントロールに `CompanyName` が表示されることを確認します。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
