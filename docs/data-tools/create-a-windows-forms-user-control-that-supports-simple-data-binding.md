---
title: 単純なデータ バインディングをサポートするユーザー コントロールの作成
description: Visual Studio で DefaultBindingPropertyAttribute クラスを使用して、単純なデータ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom controls [Visual Studio], Data Sources Window
- Data Sources Window, controls
ms.assetid: b1488366-6dfb-454e-9751-f42fd3f3ddfb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 7f26de2f26a132fc210920d94742ec7883612d66
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216307"
---
# <a name="create-a-windows-forms-user-control-that-supports-simple-data-binding"></a>単純なデータ バインディングをサポートする Windows フォーム ユーザー コントロールの作成

Windows アプリケーションのフォームにデータを表示する場合は、**[ツールボックス]** から既存のコントロールを選択するか、またはアプリケーションが標準コントロールでは提供できない機能を必要とする場合は、カスタム コントロールを記述できます。 このチュートリアルでは、<xref:System.ComponentModel.DefaultBindingPropertyAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.DefaultBindingPropertyAttribute> を実装するコントロールには、データにバインドできるプロパティを 1 つ含めることができます。 このようなコントロールは、<xref:System.Windows.Forms.TextBox> や <xref:System.Windows.Forms.CheckBox> に似ています。

コントロール作成の詳細については、[デザイン時の Windows フォーム コントロールの開発](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)に関するページを参照してください。

データ バインディングのシナリオで使用するためのコントロールを作成するときは、次のいずれかのデータ バインディング属性を実装する必要があります。

|データ バインディング属性の使用|
| - |
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 詳細については、「[複合データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)」を参照してください。|
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 詳細については、「[ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)」を参照してください。|

このチュートリアルでは、テーブルの単一の列のデータを表示する簡単なコントロールを作成します。 この例では、Northwind サンプル データベースの `Phone` テーブルの `Customers` 列を使用します。 この簡単なユーザー コントロールは、<xref:System.Windows.Forms.MaskedTextBox> を使用し、電話番号にマスクを設定して、顧客の電話番号を標準の電話番号形式で表示します。

このチュートリアルでは、次の作業を行う方法について説明します。

- 新しい **Windows フォーム アプリケーション** を作成します。

- 新しい **ユーザー コントロール** をプロジェクトに追加します。

- ユーザー コントロールをビジュアルに設計します。

- `DefaultBindingProperty` 属性を実装します。

- **データ ソース構成** ウィザードを使用してデータセットを作成します。

- **[データ ソース]** ウィンドウで **[Phone]** 列が新しいコントロールを使用するように設定します。

- フォームを作成して、新しいコントロールにデータを表示します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、**Visual Studio インストーラー** の **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-application"></a>Windows フォーム アプリケーションを作成する

最初に **Windows フォーム アプリケーション** を作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[Windows フォーム アプリ]** プロジェクト タイプを選択します。

4. プロジェクトに **SimpleControlWalkthrough** という名前を付け、 **[OK]** を選択します。

     **SimpleControlWalkthrough** プロジェクトが作成されて **ソリューション エクスプローラー** に追加されます。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する

このチュートリアルでは、**ユーザー コントロール** から単純なデータ バインド可能なコントロールを作成します。 **SimpleControlWalkthrough** プロジェクトに **ユーザー コントロール** 項目を追加します。

1. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** を選択します。

2. [ファイル名] 領域に「**PhoneNumberBox**」と入力し、**[追加]** をクリックします。

     **PhoneNumberBox** コントロールが **ソリューション エクスプローラー** に追加され、デザイナーが開きます。

## <a name="design-the-phonenumberbox-control"></a>PhoneNumberBox コントロールを設計する

このチュートリアルでは、既存の <xref:System.Windows.Forms.MaskedTextBox> を展開して **PhoneNumberBox** コントロールを作成します。

1. **ツールボックス** からユーザー コントロールのデザイン サーフェイスに <xref:System.Windows.Forms.MaskedTextBox> をドラッグします。

2. ドラッグした <xref:System.Windows.Forms.MaskedTextBox> のスマート タグを選択し、**[マスクの設定]** を選択します。

3. **[定型入力]** ダイアログ ボックスで **[電話番号]** を選択し、**[OK]** をクリックしてマスクを設定します。

## <a name="add-the-required-data-binding-attribute"></a>必要なデータ バインディング属性の追加

データ バインディングをサポートする簡単なコントロールに対しては <xref:System.ComponentModel.DefaultBindingPropertyAttribute> を実装します。

1. **PhoneNumberBox** コントロールをコード ビューに切り替えます。 (**[表示]** メニューの **[コード]** を選択します。)

2. **PhoneNumberBox** のコードを次のように置き換えます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/PhoneNumberBox.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/PhoneNumberBox.vb" id="Snippet3":::

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-data-source-from-your-database"></a>データベースからのデータ ソースの作成

この手順では、**データ ソース構成** ウィザードを使用して、Northwind サンプル データベースの `Customers` テーブルに基づいてデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプル データベースの設定の詳細については、「[方法 : サンプル データベースをインストールする](../data-tools/installing-database-systems-tools-and-samples.md)」を参照してください。

1. **[データ ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データ ソースの表示]** をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして **データ ソース構成** ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、**[データベース]** を選択し、**[次へ]** をクリックします。

4. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

8. `Customers` テーブルを選択し、**[完了]** をクリックします。

     プロジェクトに **NorthwindDataSet** が追加され、 **[データ ソース]** ウィンドウに `Customers` テーブルが表示されます。

## <a name="set-the-phone-column-to-use-the-phonenumberbox-control"></a>PhoneNumberBox コントロールを使用するように [Phone] 列を設定する

**[データ ソース]** ウィンドウでは、フォームにコントロールをドラッグする前に作成するコントロールを設定できます。

1. デザイナーで **Form1** を開きます。

2. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

3. **[Customers]** ノードのドロップダウン矢印をクリックし、コントロール リストの **[Details]** を選択します。

4. **[Phone]** 列のドロップダウン矢印をクリックし、**[Customize]** をクリックします。

5. **[データ UI カスタマイズ オプション]** ダイアログ ボックスの **[関連付けられたコントロール]** の一覧の **[PhoneNumberBox]** を選択します。

6. **[Phone]** 列のドロップダウン矢印をクリックし、**[PhoneNumberBox]** をクリックします。

## <a name="add-controls-to-the-form"></a>コントロールをフォームに追加する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

フォームにデータ バインド コントロールを作成するには、 **[データ ソース]** ウィンドウからフォームにメインの **[Customers]** ノードをドラッグし、**PhoneNumberBox** コントロールを使用して **[Phone]** 列にデータが表示されることを確認します。

説明のラベルが付いたデータ バインド コントロールとレコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

## <a name="run-the-application"></a>アプリケーションの実行

**F5** キーを押してアプリケーションを実行します。

## <a name="next-steps"></a>次のステップ

アプリケーションの要件に応じて、データ バインディングをサポートするコントロールの作成後に、追加の操作を実行できます。 次の手順として、一般的には、次のようなことを実行します。

- 他のアプリケーションで再利用できるように、コントロール ライブラリにカスタム コントロールを配置します。

- より複雑なデータ バインディングのシナリオをサポートするコントロールを作成します。 詳細については、「[複合データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)」および「[ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
