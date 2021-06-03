---
title: 'チュートリアル: Word の操作ウィンドウ上のコントロールにデータをバインドする'
description: Microsoft Word の操作ウィンドウ上のコントロールにデータをバインドします。 このコントロールは、SQL Server データベースのテーブル間のマスター/詳細の関係を示します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], data binding
- actions panes [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], smart documents
- data binding [Office development in Visual Studio], actions panes
- actions panes [Office development in Visual Studio], binding controls
- smart documents [Office development in Visual Studio], data binding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d94891520695117c7a395f81feda81e52f909fe6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824498"
---
# <a name="walkthrough-bind-data-to-controls-on-a-word-actions-pane"></a>チュートリアル: Word の操作ウィンドウ上のコントロールにデータをバインドする
  このチュートリアルでは、Word の操作ウィンドウ上のコントロールにデータをバインドする方法について説明します。 このコントロールは、SQL Server データベースのテーブル間のマスター/詳細の関係を示します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- データにバインドされた Windows フォーム コントロールを含む操作ウィンドウを作成する。

- マスター/詳細関係を使用してコントロールにデータを表示する。

- アプリケーションが開いたときに操作ウィンドウを表示する。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

- Northwind SQL Server サンプル データベースがあるサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みのアクセス許可。

## <a name="create-the-project"></a>プロジェクトを作成する
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. 「**My Word Actions Pane**」という名前の Word 文書プロジェクトを作成します。 ウィザードで、 **[新しいドキュメントの作成]** を選択します。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Word 文書が Visual Studio のデザイナーで開かれ、**My Word Actions Pane** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-controls-to-the-actions-pane"></a>操作ウィンドウにコントロールを追加する
 このチュートリアルでは、データ バインドされた Windows フォーム コントロールを含む操作ウィンドウ コントロールが必要です。 データ ソースをプロジェクトに追加し、 **[データ ソース]** ウィンドウから操作ウィンドウ コントロールにコントロールをドラッグします。

### <a name="to-add-an-actions-pane-control"></a>操作ウィンドウ コントロールを追加するには

1. **ソリューション エクスプローラー** で、 **[My Word Actions Pane]** プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[操作ウィンドウ コントロール]** を選択し、名前を **ActionsControl** と指定して、 **[追加]** をクリックします。

### <a name="to-add-a-data-source-to-the-project"></a>プロジェクトにデータ ソースを追加するには

1. **[データ ソース]** ウィンドウが表示されていない場合は、メニュー バーで **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** をクリックして表示します。

   > [!NOTE]
   > **[データ ソースの表示]** が使用できない場合は、Word 文書をクリックし、もう一度確認します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. **[データベース]** を選択し、 **[次へ]** をクリックします。

4. SQL Server の Northwind サンプル データベースへのデータ接続を選択するか、または **[新しい接続]** ボタンを使用して新しい接続を追加します。

5. **[次へ]** をクリックします。

6. 接続を保存するオプションがオンになっている場合は、それをオフにして、 **[次へ]** をクリックします。

7. **[データベース オブジェクト]** ウィンドウで、 **[Tables]** ノードを展開します。

8. **Suppliers** テーブルと **Products** テーブルの隣にあるチェック ボックスをオンにします。

9. **[完了]** をクリックします。

   ウィザードにより、**Suppliers** テーブルと **Products** テーブルが **[データ ソース]** ウィンドウに追加されます。 また、**ソリューション エクスプローラー** に表示される、型指定されたデータセットがプロジェクトに追加されます。

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>データ バインドされた Windows フォーム コントロールを操作ウィンドウ コントロールに追加するには

1. **[データ ソース]** ウィンドウで、**Suppliers** テーブルを展開します。

2. **[Company Name]** ノードのドロップダウン矢印をクリックし、 **[ComboBox]** を選択します。

3. **[データ ソース]** ウィンドウから操作ウィンドウ コントロールに **CompanyName** をドラッグします。

     操作ウィンドウ コントロールに <xref:System.Windows.Forms.ComboBox> コントロールが作成されます。 同時に、`SuppliersBindingSource` という名前の <xref:System.Windows.Forms.BindingSource>、テーブル アダプター、および <xref:System.Data.DataSet> がプロジェクトのコンポーネント トレイに追加されます。

4. **コンポーネント** トレイで `SuppliersBindingNavigator` を選択し、**Delete** キーを押します。 このチュートリアルでは `SuppliersBindingNavigator` を使用しません。

    > [!NOTE]
    > `SuppliersBindingNavigator` を削除しても、それのために生成されたコードがすべて削除されるわけではありません。 このコードは削除できます。

5. コンボ ボックスをラベルの下に移動し、**Size** プロパティを **171, 21** に変更します。

6. **[データ ソース]** ウィンドウで、**Suppliers** テーブルの子である **Products** テーブルを展開します。

7. **[ProductName]** ノードのドロップダウン矢印をクリックし、 **[ListBox]** を選択します。

8. 操作ウィンドウ コントロールに **ProductName** をドラッグします。

     操作ウィンドウ コントロールに <xref:System.Windows.Forms.ListBox> コントロールが作成されます。 同時に、`ProductBindingSource` という名前の <xref:System.Windows.Forms.BindingSource>、およびテーブル アダプターがプロジェクトのコンポーネント トレイに追加されます。

9. リスト ボックスをラベルの下に移動し、**Size** プロパティを **171,95** に変更します。

10. **[ツールボックス]** から操作ウィンドウ コントロールに <xref:System.Windows.Forms.Button> をドラッグし、リスト ボックスの下に配置します。

11. <xref:System.Windows.Forms.Button> を右クリックし、ショートカット メニューの **[プロパティ]** をクリックして、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**[挿入]**|
    |**[テキスト]**|**[挿入]**|

12. ユーザー コントロールのサイズを、コントロールに合わせて変更します。

## <a name="set-up-the-data-source"></a>データ ソースを設定する
 データ ソースを設定するには、操作ウィンドウ コントロールの <xref:System.Windows.Forms.UserControl.Load> イベントにコードを追加して、コントロールに <xref:System.Data.DataTable> のデータを読み込み、各コントロールの <xref:System.Windows.Forms.Binding.DataSource%2A> プロパティと <xref:System.Windows.Forms.BindingSource.DataMember%2A> プロパティを設定します。

### <a name="to-load-the-control-with-data"></a>コントロールにデータを読み込むには

1. `ActionsControl` クラスの <xref:System.Windows.Forms.UserControl.Load> イベント ハンドラーに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet1":::

2. C# では、このイベント ハンドラーを <xref:System.Windows.Forms.UserControl.Load> イベントにアタッチする必要があります。 このコードは、`ActionsControl` コンストラクター内の、`InitializeComponent` の呼び出しの後に配置できます。 イベント ハンドラーの作成方法の詳細については、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet33":::

### <a name="to-set-data-binding-properties-of-the-controls"></a>コントロールのデータ バインディング プロパティを設定するには

1. `CompanyNameComboBox` コントロールを選択します。

2. **[プロパティ]** ウィンドウで、**DataSource** プロパティの右側にあるボタンをクリックし、**suppliersBindingSource** を選択します。

3. **DisplayMember** プロパティの右側にあるボタンをクリックし、**CompanyName** を選択します。

4. **DataBindings** プロパティを展開し、**Text** プロパティの右側にあるボタンをクリックして、 **[なし]** を選択します。

5. `ProductNameListBox` コントロールを選択します。

6. **[プロパティ]** ウィンドウで、**DataSource** プロパティの右側にあるボタンをクリックし、**productsBindingSource** を選択します。

7. **DisplayMember** プロパティの右側にあるボタンをクリックし、**ProductName** を選択します。

8. **DataBindings** プロパティを展開し、**SelectedValue** プロパティの右側にあるボタンをクリックして、 **[なし]** を選択します。

## <a name="add-a-method-to-insert-data-into-a-table"></a>テーブルにデータを挿入するメソッドを追加する
 次のタスクは、バインドされたコントロールからデータを読み取り、Word 文書のテーブルにデータを挿入することです。 まず、テーブルの見出しを書式設定するためのプロシージャを作成してから、Word のテーブルを作成して書式設定するための `AddData` メソッドを追加します。

### <a name="to-format-the-table-headings"></a>テーブルの見出しの書式を設定するには

1. `ActionsControl` クラスで、テーブルの見出しの書式を設定するメソッドを作成します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet2":::

### <a name="to-create-the-table"></a>テーブルを作成するには

1. `ActionsControl` クラスで、テーブルがまだ存在しない場合にテーブルを作成し、操作ウィンドウからテーブルにデータを追加するメソッドを記述します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet3":::

### <a name="to-insert-text-into-a-word-table"></a>Word のテーブルにテキストを挿入するには

1. **[Insert]** ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet4":::

2. C# では、ボタンの <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを作成する必要があります。  このコードは、`ActionsControl` クラスの <xref:System.Windows.Forms.UserControl.Load> イベント ハンドラー内に配置できます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet5":::

## <a name="show-the-actions-pane"></a>操作ウィンドウを表示する
 操作ウィンドウは、コントロールが追加されると表示されます。

### <a name="to-show-the-actions-pane"></a>操作ウィンドウを表示するには

1. **ソリューション エクスプローラー** で **ThisDocument.vb** または **ThisDocument.cs** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. 次の例のように、`ThisDocument` クラスの上部にコントロールの新しいインスタンスを作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet6":::

3. 次の例のように、`ThisDocument` の <xref:Microsoft.Office.Tools.Word.Document.Startup> イベント ハンドラーにコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet7":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、文書をテストして、文書を開いたときに操作ウィンドウが表示されることを確認しましょう。 操作ウィンドウのコントロールのマスター/詳細関係をテストし、 **[Insert]** ボタンがクリックされたときに Word のテーブルにデータが挿入されることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. 操作ウィンドウが表示されていることを確認します。

3. コンボ ボックスで会社を選択して、 **[Products]** リスト ボックス内の項目が変化することを確認します。

4. 製品を選択し、操作ウィンドウの **[Insert]** をクリックして、Word のテーブルに製品の詳細が追加されることを確認します。

5. さまざまな会社から追加の製品を挿入します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Word の操作ウィンドウ上のコントロールにデータをバインドする方法の基本について説明しました。 ここでは、次の作業を行います。

- Excel のコントロールにデータをバインドする。 詳細については、「[チュートリアル: Excel の操作ウィンドウ上のコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)」を参照してください。

- プロジェクトを配置する。 詳細については、「[ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
