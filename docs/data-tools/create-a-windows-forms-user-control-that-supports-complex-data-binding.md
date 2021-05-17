---
title: データ バインディングを使用した Windows フォーム ユーザー コントロールの作成
description: ComplexBindingPropertiesAttribute クラスを実装することにより、複合データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- data binding, complex
- user controls [Visual Studio], complex data binding
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: ff8c641cc0b817b5f2a145af49c5e0accdc295d0
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216333"
---
# <a name="create-a-windows-forms-user-control-that-supports-complex-data-binding"></a>複合データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成

Windows アプリケーションのフォームにデータを表示する場合は、**ツールボックス** から既存のコントロールを選択できます。 また、アプリケーションに標準コントロールでは使用できない機能が必要な場合は、カスタム コントロールを作成できます。 このチュートリアルでは、<xref:System.ComponentModel.ComplexBindingPropertiesAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> を実装するコントロールには、データにバインドできる `DataSource` プロパティと `DataMember` プロパティが含まれます。 このようなコントロールは、<xref:System.Windows.Forms.DataGridView> や <xref:System.Windows.Forms.ListBox> に似ています。

コントロール作成の詳細については、[デザイン時の Windows フォーム コントロールの開発](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time)に関するページを参照してください。

データ バインディングのシナリオで使用するためのコントロールを作成するときは、次のいずれかのデータ バインディング属性を実装する必要があります。

|データ バインディング属性の使用|
| - |
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 詳細については、「[単純なデータ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)」を参照してください。|
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 詳細については、「[ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)」を参照してください。|

このチュートリアルでは、テーブルからのデータ行を表示する複合コントロールを作成します。 この例では、Northwind サンプル データベースの `Customers` テーブルを使用します。 複合ユーザー コントロールは、カスタム コントロールの <xref:System.Windows.Forms.DataGridView> で Customers テーブルを表示します。

このチュートリアルでは、次の作業を行う方法について説明します。

- 新しい **ユーザー コントロール** をプロジェクトに追加します。

- ユーザー コントロールをビジュアルに設計します。

- `ComplexBindingProperty` 属性を実装します。

- [データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を使用してデータセットを作成します。

- [[データ ソース] ウィンドウ](add-new-data-sources.md#data-sources-window)の **Customers** テーブルが新しい複合コントロールを使用するように設定します。

- **[データ ソース]** ウィンドウから **Form1** に新しいコントロールをドラッグして追加します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

1. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    1. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    1. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-app-project"></a>Windows フォーム アプリ プロジェクトを作成する

最初の手順では、C# または Visual Basic 用の **Windows フォーム アプリ** プロジェクトを作成します。 プロジェクトに **ComplexControlWalkthrough** という名前を付けます。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する

このチュートリアルでは **ユーザー コントロール** からデータ バインディング可能な複合コントロールを作成するので、**ユーザー コントロール** の項目をプロジェクトに追加します。

1. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** を選択します。

1. **[ファイル名]** 領域に「**ComplexDataGridView**」と入力し、**[追加]** をクリックします。

    **ComplexDataGridView** コントロールが **ソリューション エクスプローラー** に追加され、デザイナーが開きます。

## <a name="design-the-complexdatagridview-control"></a>ComplexDataGridView コントロールを設計する

ユーザー コントロールに <xref:System.Windows.Forms.DataGridView> を追加するには、**ツールボックス** からユーザー コントロールのデザイン サーフェイスに、<xref:System.Windows.Forms.DataGridView> をドラッグします。

## <a name="add-the-required-data-binding-attribute"></a>必要なデータ バインディング属性の追加

データ バインディングをサポートする複合コントロールには、<xref:System.ComponentModel.ComplexBindingPropertiesAttribute> を実装できます。

1. **ComplexDataGridView** コントロールをコード ビューに切り替えます  (**[表示]** メニューの **[コード]** を選択します)。

1. `ComplexDataGridView` のコードを次のコードで置き換えます。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/ComplexDataGridView.cs" id="Snippet4":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/ComplexDataGridView.vb" id="Snippet4":::

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-data-source-from-your-database"></a>データベースからのデータ ソースの作成

**データ ソース構成** ウィザードを使用して、Northwind サンプル データベースの `Customers` テーブルに基づいてデータ ソースを作成します。

1. **[データ ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データ ソースの表示]** をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして **データ ソース構成** ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

4. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

   - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

   - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

8. `Customers` テーブルを選択し、**[完了]** をクリックします。

   プロジェクトに **NorthwindDataSet** が追加され、 **[データ ソース]** ウィンドウに `Customers` テーブルが表示されます。

## <a name="set-the-customers-table-to-use-the-complexdatagridview-control"></a>ComplexDataGridView コントロールを使用するように Customers テーブルを設定する

**[データ ソース]** ウィンドウでは、フォームにコントロールをドラッグする前に作成するコントロールを設定できます。

1. デザイナーで **Form1** を開きます。

1. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

1. **[Customers]** ノードのドロップダウン矢印をクリックし、**[カスタマイズ]** をクリックします。

1. **[データ UI カスタマイズ オプション]** ダイアログ ボックスの **[関連付けられたコントロール]** の一覧の **[ComplexDataGridView]** を選択します。

1. `Customers` テーブルのドロップダウン矢印をクリックし、コントロール リストから **ComplexDataGridView** を選択します。

## <a name="add-controls-to-the-form"></a>コントロールをフォームに追加する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。 **[データ ソース]** ウィンドウからフォームにメインの **[Customers]** ノードをドラッグします。 テーブルのデータを表示するために **ComplexDataGridView** コントロールが使用されていることを確認します。

## <a name="run-the-application"></a>アプリケーションの実行

**F5** キーを押してアプリケーションを実行します。

## <a name="next-steps"></a>次のステップ

アプリケーションの要件に応じて、データ バインディングをサポートするコントロールの作成後に、追加の操作を実行できます。 次の手順として、一般的には、次のようなことを実行します。

- 他のアプリケーションで再利用できるように、コントロール ライブラリにカスタム コントロールを配置します。

- 検索のシナリオをサポートするコントロールを作成します。 詳細については、「[ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
- [Windows フォーム コントロール](/dotnet/framework/winforms/controls/index)
