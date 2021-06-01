---
title: 'チュートリアル: ドキュメント レベルのプロジェクトでの単純データ バインディング'
description: ドキュメント レベルのプロジェクトにおけるデータ バインディングの基本について説明します。また、SQL Server データベース内の単一のデータ フィールドは、Microsoft Excel の名前付き範囲にバインドされるということについても説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], worksheet cell to Database field
- worksheets [Office development in Visual Studio], binding worksheet cell to Database field
- Database field [Office development in Visual Studio]
- data [Office development in Visual Studio], binding data
- simple data binding [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 36d4da65a6cd39c53f1f9d8edf4f9d9b1fe46284
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826851"
---
# <a name="walkthrough-simple-data-binding-in-a-document-level-project"></a>チュートリアル: ドキュメント レベルのプロジェクトでの単純データ バインディング
  このチュートリアルでは、ドキュメント レベルのプロジェクトにおけるデータバインディングの基本について説明します。 SQL Server データベース内の単一のデータ フィールドは、Microsoft Office Excel の名前付き範囲にバインドされます。 このチュートリアルでは、コントロールを追加して、テーブル内のすべてのレコードをスクロールできるようにする方法についても説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- Excel プロジェクト用のデータソースを作成する。

- ワークシートにコントロールを追加する。

- データベース レコードをスクロールする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプル データベースがあるサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みのアクセス許可。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 この手順では、Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. Visual Basic または C# のいずれかを使用して、**My Simple Data Binding** という名前の Excel ブック プロジェクトを作成します。 **[新しいドキュメントを作成]** が選択されていることを確認してください。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

   Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Simple Data Binding** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="create-the-data-source"></a>データ ソースを作成する
 **[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. **[データ ソース]** ウィンドウが表示されていない場合は、メニュー バーで **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. **[データベース]** を選択し、 **[次へ]** をクリックします。

4. SQL Server の Northwind サンプル データベースへのデータ接続を選択するか、または **[新しい接続]** ボタンをクリックして新しい接続を追加します。

5. 接続を選択または作成したら、 **[次へ]** をクリックします。

6. 接続を保存するオプションがオンになっている場合は、それをオフにして、 **[次へ]** をクリックします。

7. **[データベース オブジェクト]** ウィンドウで、 **[Tables]** ノードを展開します。

8. **Customers** テーブルの隣にあるチェック ボックスをオンにします。

9. **[完了]** をクリックします。

   ウィザードによって、**Customers** テーブルが **[データ ソース]** ウィンドウに追加されます。 また、**ソリューション エクスプローラー** に表示される、型指定されたデータセットがプロジェクトに追加されます。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 このチュートリアルでは、最初のワークシートに 2 つの名前付き範囲と 4 つのボタンが必要です。 まず、 **[データ ソース]** ウィンドウから 2 つの名前付き範囲を追加して、データ ソースに自動的にバインドされるようにします。 次に、**ツールボックス** からボタンを追加します。

### <a name="to-add-two-named-ranges"></a>2 つの名前付き範囲を追加するには

1. *My Simple Data Binding.xlsx* ブックが Visual Studio デザイナーで開かれ、**Sheet1** が表示されていることを確認します。

2. **[データ ソース]** ウィンドウを開き、 **[Customers]** ノードを展開します。

3. **[CompanyName]** 列を選択し、表示されるドロップダウン矢印をクリックします。

4. ドロップダウン リストから **[NamedRange]** を選択し、 **[CompanyName]** 列をセル **A1** にドラッグします。

     `companyNameNamedRange` という名前の <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールが、セル **A1** に作成されます。 同時に、`customersBindingSource` という名前の <xref:System.Windows.Forms.BindingSource>、テーブル アダプター、および <xref:System.Data.DataSet> インスタンスがプロジェクトに追加されます。 コントロールは <xref:System.Windows.Forms.BindingSource> にバインドされ、さらにこれが <xref:System.Data.DataSet> インスタンスにバインドされます。

5. **[データ ソース]** ウィンドウで **[CustomerID]** 列を選択し、表示されるドロップダウン矢印をクリックします。

6. ドロップダウン リストで **[NamedRange]** をクリックし、 **[CustomerID]** 列をセル **B1** にドラッグします。

7. `customerIDNamedRange` という名前の別の <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールがセル **B1** に作成され、<xref:System.Windows.Forms.BindingSource> にバインドされます。

### <a name="to-add-four-buttons"></a>4 つのボタンを追加するには

1. **[ツールボックス]** の **[コモン コントロール]** タブから、<xref:System.Windows.Forms.Button> コントロールをワークシートのセル **A3** に追加します。

    このボタンには `Button1` という名前が付けられます。

2. 以下の順序で、後続のセルに 3 つのボタンを追加し、下記の名前になるようにします。

   |Cell (セル)|[(名前)]|
   |----------|--------------|
   |B3|Button2|
   |C3|Button3|
   |D3|Button4|

   次の手順では、ボタンにテキストを追加します。また、C# の場合はイベント ハンドラーも追加します。

## <a name="initialize-the-controls"></a>コントロールを初期化する
 ボタン テキストを設定し、<xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベントの際のイベント ハンドラーを追加します。

### <a name="to-initialize-the-controls"></a>コントロールを初期化するには

1. **ソリューション エクスプローラー** で **Sheet1.vb** または **Sheet1.cs** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. `Sheet1_Startup` メソッドに次のコードを追加して、各ボタンのテキストを設定します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet2":::

3. C# の場合のみ、ボタン クリック イベントのイベント ハンドラーを `Sheet1_Startup` メソッドに追加します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet3":::

   次は、ボタンの <xref:System.Windows.Forms.Control.Click> イベントを処理するコードを追加して、ユーザーがレコードを参照できるようにします。

## <a name="add-code-to-enable-scrolling-through-the-records"></a>レコードのスクロールを有効にするコードを追加する
 レコード間を移動するためのコードを、各ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに追加します。

### <a name="to-move-to-the-first-record"></a>最初のレコードに移動するには

1. `Button1` ボタンの <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを追加し、最初のレコードに移動するための次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet4":::

### <a name="to-move-to-the-previous-record"></a>前のレコードに移動するには

1. `Button2` ボタンの <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを追加し、位置を 1 つ前に戻すための次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet5":::

### <a name="to-move-to-the-next-record"></a>次のレコードに移動するには

1. `Button3` ボタンの <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを追加し、位置を 1 つ先へ進めるための次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet6":::

### <a name="to-move-to-the-last-record"></a>最後のレコードに移動するには

1. `Button4` ボタンの <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを追加し、最後のレコードに移動するための次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet7":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ブックをテストして、データベース内のレコードを参照できるかどうか確認しましょう。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. 最初のレコードがセル **A1** と **B1** に表示されることを確認します。

3. **>** (`Button3`) ボタンをクリックし、次のレコードがセル **A1** と **B1** に表示されることを確認します。

4. 他のスクロール ボタンをクリックして、レコードが意図したとおりに変更されることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、名前付き範囲をデータベースのフィールドにバインドする方法の基本について説明しました。 ここでは、次の作業を行います。

- データをキャッシュして、オフラインで使用できるようにする。 詳細については、「[方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)」を参照してください。

- 1 つのフィールドではなく、テーブル内の複数の列にセルをバインドする。 詳しくは、「[チュートリアル: ドキュメント レベルのプロジェクトでの複合データ バインディング](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)」をご覧ください。

- <xref:System.Windows.Forms.BindingNavigator> コントロールを使用してレコードをスクロールする。 詳しくは、「[方法: Windows フォーム BindingNavigator コントロールを使用してデータ間を移動する](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office ソリューションにおけるデータ](../vsto/data-in-office-solutions.md)
- [チュートリアル: ドキュメント レベルのプロジェクトでの複合データ バインディング](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
