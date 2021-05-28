---
title: 'チュートリアル: Excel の操作ウィンドウ上のコントロールにデータをバインドする'
description: Microsoft Excel の操作ウィンドウ上のコントロールにデータをバインドします。 このコントロールは、SQL Server データベースのテーブル間のマスター/詳細の関係を示します。
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
ms.openlocfilehash: 377c3405211c91712f8754131d8379c3dae7e820
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824550"
---
# <a name="walkthrough-bind-data-to-controls-on-an-excel-actions-pane"></a>チュートリアル: Excel の操作ウィンドウ上のコントロールにデータをバインドする
  このチュートリアルでは、Microsoft Office Excel の操作ウィンドウ上のコントロールにデータをバインドする方法について説明します。 このコントロールは、SQL Server データベースのテーブル間のマスター/詳細の関係を示します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- ワークシートにコントロールを追加する。

- 操作ウィンドウ コントロールを作成する。

- データ バインドされた Windows フォーム コントロールを操作ウィンドウ コントロールに追加する。

- アプリケーションが開いたときに操作ウィンドウを表示する。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプル データベースがあるサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みのアクセス許可。

## <a name="create-the-project"></a>プロジェクトを作成する
 まず、Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Excel Actions Pane** という名前で Excel ブック プロジェクトを作成します。 ウィザードで、 **[新規ドキュメントの作成]** をクリックします。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Excel Actions Pane** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-a-new-data-source-to-the-project"></a>プロジェクトに新しいデータ ソースを追加する

### <a name="to-add-a-new-data-source-to-the-project"></a>プロジェクトに新しいデータ ソースを追加するには

1. **[データ ソース]** ウィンドウが表示されていない場合は、メニュー バーの **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** の順にクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. **[データベース]** を選択し、 **[次へ]** をクリックします。

4. SQL Server の Northwind サンプル データベースへのデータ接続を選択するか、または **[新しい接続]** ボタンをクリックして新しい接続を追加します。

5. **[次へ]** をクリックします。

6. 接続を保存するオプションがオンになっている場合は、それをオフにして、 **[次へ]** をクリックします。

7. **[データベース オブジェクト]** ウィンドウで、 **[Tables]** ノードを展開します。

8. **Suppliers** テーブルの隣にあるチェック ボックスをオンにします。

9. **Products** テーブルを展開し、**ProductName**、**SupplierID**、**QuantityPerUnit**、および **UnitPrice** を選択します。

10. **[完了]** をクリックします。

    ウィザードにより、**Suppliers** テーブルと **Products** テーブルが **[データ ソース]** ウィンドウに追加されます。 また、**ソリューション エクスプローラー** に表示される、型指定されたデータセットがプロジェクトに追加されます。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 次に、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールと <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを最初のワークシートに追加します。

### <a name="to-add-a-namedrange-control-and-a-listobject-control"></a>NamedRange コントロールと ListObject コントロールを追加するには

1. **My Excel Actions Pane.xlsx** ブックが Visual Studio デザイナーで開かれ、`Sheet1` 表示されていることを確認します。

2. **[データ ソース]** ウィンドウで、**Suppliers** テーブルを展開します。

3. **[Company Name]** ノードのドロップダウン矢印をクリックし、 **[NamedRange]** をクリックします。

4. **Company Name** を、 **[データ ソース]** ウィンドウから `Sheet1` のセル **A2** にドラッグします。

     `CompanyNameNamedRange` という名前の <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールが作成され、テキスト \<CompanyName> がセル **A2** に表示されます。 同時に、`suppliersBindingSource` という名前の <xref:System.Windows.Forms.BindingSource>、テーブル アダプター、および <xref:System.Data.DataSet> がプロジェクトに追加されます。 コントロールは <xref:System.Windows.Forms.BindingSource> にバインドされ、さらにこれが <xref:System.Data.DataSet> インスタンスにバインドされます。

5. **[データ ソース]** ウィンドウで、**Suppliers** テーブルの下にある列の末尾までスクロールします。 一覧の一番下には、**Products** テーブルがあります。これは、**Suppliers** テーブルの子であるためです。 この **Products** テーブル (**Suppliers** テーブルと同じレベルにあるものではなく) を選択し、表示されるドロップダウン矢印をクリックします。

6. ドロップダウン リストで **[ListObject]** をクリックし、**Products** テーブルを `Sheet1` のセル **A6** にドラッグします。

     <xref:Microsoft.Office.Tools.Excel.ListObject> という名前の `ProductNameListObject` コントロールがセル **A6** に作成されます。 同時に、`productsBindingSource` という名前の <xref:System.Windows.Forms.BindingSource> と、テーブル アダプターがプロジェクトに追加されます。 コントロールは <xref:System.Windows.Forms.BindingSource> にバインドされ、さらにこれが <xref:System.Data.DataSet> インスタンスにバインドされます。

7. C# の場合のみ、コンポーネント トレイの **[suppliersBindingSource]** を選択し、**プロパティ** ウィンドウで **Modifiers** プロパティを **Internal** に変更します。

## <a name="add-controls-to-the-actions-pane"></a>操作ウィンドウにコントロールを追加する
 次に、コンボ ボックスを含んだ操作ウィンドウ コントロールが必要です。

### <a name="to-add-an-actions-pane-control"></a>操作ウィンドウ コントロールを追加するには

1. **ソリューション エクスプローラー** で、 **[My Excel Actions Pane]** プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[操作ウィンドウ コントロール**] を選択し、名前を **ActionsControl** と指定して、 **[追加]** をクリックします。

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>データ バインドされた Windows フォーム コントロールを操作ウィンドウ コントロールに追加するには

1. **ツールボックス** の **[コモン コントロール]** タブから、<xref:System.Windows.Forms.ComboBox> コントロールを操作ウィンドウ コントロールにドラッグします。

2. **Size** プロパティを **171, 21** に変更します。

3. ユーザー コントロールのサイズを、コンボ ボックスに合わせて変更します。

## <a name="bind-the-control-on-the-actions-pane-to-data"></a>操作ウィンドウ上のコントロールをデータにバインドする
 このセクションでは、<xref:System.Windows.Forms.ComboBox> のデータ ソースを、ワークシート上の <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールと同じデータ ソースに設定します。

### <a name="to-set-data-binding-properties-of-the-control"></a>コントロールのデータ バインディング プロパティを設定するには

1. 操作ウィンドウ コントロールを右クリックし、 **[コードの表示]** をクリックします。

2. 操作ウィンドウ コントロールの <xref:System.Windows.Forms.UserControl.Load> イベントに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ActionsControl.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet1":::

3. C# では、`ActionsControl` のイベント ハンドラーを作成する必要があります。 このコードを、`ActionsControl` コンストラクターに配置できます。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet2":::

## <a name="show-the-actions-pane"></a>操作ウィンドウを表示する
 操作ウィンドウは、実行時にコントロールを追加するまでは表示されません。

#### <a name="to-show-the-actions-pane"></a>操作ウィンドウを表示するには

1. **ソリューション エクスプローラー** で、*ThisWorkbook.vb* または *ThisWorkbook.cs* を右クリックし、 **[コードの表示]** をクリックします。

2. `ThisWorkbook` クラスに、ユーザー コントロールの新規インスタンスを作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet3":::

3. `ThisWorkbook` の <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> イベント ハンドラーで、操作ウィンドウにコントロールを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet4":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ドキュメントをテストして、ドキュメントを開いたときに操作ウィンドウが開くことと、コントロールにマスター/詳細関係があることを確認していきます。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. 操作ウィンドウが表示されていることを確認します。

3. リスト ボックスで会社を選択します。 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールに会社名が表示されていて、<xref:Microsoft.Office.Tools.Excel.ListObject> コントロールに製品の詳細が表示されていることを確認します。

4. さまざまな会社を選択して、会社名と製品詳細が適切に変更されることを確認します。

## <a name="next-steps"></a>次の手順
 ここでは、次の作業を行います。

- Word のコントロールにデータをバインドする。 詳しくは、「[チュートリアル: Word の操作ウィンドウ上のコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)」をご覧ください。

- プロジェクトを配置する。 詳しくは、「[ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)」をご覧ください。

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: 操作ウィンドウ上のコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
