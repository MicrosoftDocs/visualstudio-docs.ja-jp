---
title: オプション ボタンを使ってワークシートのグラフを更新する
description: Microsoft Excel ワークシート上のオプション ボタンを使って、ユーザーがオプションをすばやく切り替えられるようにする基本的な方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, updating using managed controls
- controls [Office development in Visual Studio], updating worksheets
- worksheets, using radio buttons
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3d61579181f00d97a74cc48e022bb5d93a05c0f0
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828177"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>チュートリアル : オプション ボタンを使用してワークシートのグラフを更新する方法
  このチュートリアルでは、Microsoft Office Excel ワークシート上のオプション ボタンを使って、ユーザーがオプションをすばやく切り替えられるようにする基本的な方法について説明します。 今回は、オプションによってグラフのスタイルが変更されるようにします。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 完全なサンプルの結果を確認するには、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」にある Excel コントロールのサンプルを参照してください。

 このチュートリアルでは、次の作業について説明します。

- ワークシートに一連のオプション ボタンを追加する。

- オプション選択時のグラフ スタイルの変更

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="add-a-chart-to-a-worksheet"></a>ワークシートにグラフを追加する
 既存のブックをカスタマイズする Excel ブック プロジェクトを作成できます。 このチュートリアルでは、ブックにグラフを追加した後、そのブックを新しい Excel ソリューションで使用します。 このチュートリアルのデータ ソースは、**Data for Chart** という名前のワークシートです。

### <a name="to-add-the-data"></a>データを追加するには

1. Microsoft Excel を開きます。

2. **[Sheet3]** タブを右クリックし、ショートカット メニューの **[名前の変更]** をクリックします。

3. シートの名前を **Data for Chart** に変更します。

4. **Data for Chart** に次のデータを追加し、A4 が左上隅、E8 が右下隅になるようにします。

   |リージョン/四半期|Q1|Q2|Q3|Q4|
   |-|--------|--------|--------|--------|
   |West|500|550|550|600|
   |East|600|625|675|700|
   |North|450|470|490|510|
   |South|800|750|775|790|

   次に、最初のワークシートにグラフを追加して、データを表示します。

### <a name="to-add-a-chart-in-excel"></a>Excel でグラフを追加するには

1. **[挿入]** タブの **[グラフ]** グループで、 **[縦棒]** をクリックし、 **[すべてのグラフの種類]** をクリックします。

2. **[グラフの挿入]** ダイアログ ボックスで、 **[OK]** をクリックします。

3. **[デザイン]** タブの **[データ]** グループで、 **[データの選択]** をクリックします。

4. **[データ ソースの選択]** ダイアログ ボックスの **[グラフデータの範囲]** ボックス内をクリックし、既定の選択をオフにします。

5. **[Data for Chart]** シートで、数値が格納されているセルのブロックを選択します (A4 が左上隅、E8 が右下隅になっているブロック)。

6. **[データ ソースの選択]** ダイアログ ボックスで、 **[OK]** をクリックします。

7. 右上隅がセル **E2** と揃うように、グラフの位置を変更します。

8. ファイルを C ドライブに保存し、名前を **ExcelChart.xlsx** とします。

9. Excel を終了します。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 この手順では、**ExcelChart** ブックに基づいて Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Excel Chart** という名前で Excel ブック プロジェクトを作成します。 ウィザードで、 **[既存のドキュメントをコピーする]** を選択します。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

2. **[参照]** ボタンをクリックし、このチュートリアルで先ほど作成したブックを参照します。

3. **[OK]** をクリックします。

     Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Excel Chart** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="set-properties-of-the-chart"></a>グラフのプロパティを設定する
 既存のブックを使用する新しい Excel ブック プロジェクトを作成すると、ブック内のすべての名前付き範囲、リスト オブジェクト、およびグラフに対して、ホスト コントロールが自動的に作成されます。 <xref:Microsoft.Office.Tools.Excel.Chart> コントロールの名前は、 **[プロパティ]** ウィンドウを使って変更できます。

### <a name="to-change-the-name-of-the-chart-control"></a>グラフ コントロールの名前を変更するには

1. デザイナーで <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを選択し、 **[プロパティ]** ウィンドウで次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**dataChart**|
    |**HasLegend**|**false**|

## <a name="add-controls"></a>コントロールを追加する
 このワークシートでは、オプション ボタンを使って、グラフのスタイルをユーザーがすばやく変更できるようにします。 ただし、オプション ボタンは排他的にする必要があります。つまり、1 つのボタンが選択されているときに、グループ内の他のボタンを同時に選択することはできません。 ワークシートに複数のオプション ボタンを追加した場合、この動作は既定では発生しません。

 この動作を追加する 1 つの方法は、ユーザー コントロール上のオプション ボタンをグループ化し、ユーザー コントロールの背後のコードを記述した後、ユーザー コントロールをワークシートに追加することです。

### <a name="to-add-a-user-control"></a>ユーザー コントロールを追加するには

1. **ソリューション エクスプローラー** で、 **[My Excel Chart]** プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで **[ユーザー コントロール]** をクリックし、コントロールに「**ChartOptions**」という名前を指定して **[追加]** をクリックします。

### <a name="to-add-radio-buttons-to-the-user-control"></a>ユーザー コントロールにオプション ボタンを追加するには

1. デザイナーにユーザー コントロールが表示されていない場合は、**ソリューション エクスプローラー** で **[ChartOptions]** をダブルクリックします。

2. **[ツールボックス]** の **[コモン コントロール]** タブから、 **[オプション ボタン]** コントロールをユーザー コントロールへドラッグし、次のプロパティを変更します。

   | プロパティ | 値 |
   |----------|------------------|
   | **名前** | **columnChart** |
   | **[テキスト]** | **Column Chart** |

3. 2 つ目のオプション ボタンをユーザー コントロールに追加し、次のプロパティを変更します。

   | プロパティ | 値 |
   |----------|---------------|
   | **名前** | **barChart** |
   | **[テキスト]** | **Bar Chart** |

4. 3 つ目のオプション ボタンをユーザー コントロールに追加し、次のプロパティを変更します。

   | プロパティ | 値 |
   |----------|----------------|
   | **名前** | **lineChart** |
   | **[テキスト]** | **Line Chart** |

5. 4 つ目のオプション ボタンをユーザー コントロールに追加し、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**areaBlockChart**|
   |**[テキスト]**|**Area Block Chart**|

   次に、オプション ボタンがクリックされたときにグラフを更新するためのコードを記述します。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>オプション ボタンが選択されたときにグラフのスタイルを変更する
 これで、グラフのスタイルを変更するためのコードを追加する準備ができました。 これを行うには、ユーザー コントロール上にパブリック イベントを作成し、選択の種類を設定するためのプロパティを追加して、各オプション ボタンの `CheckedChanged` イベントに対するイベント ハンドラーを作成します。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>ユーザー コントロールにイベントおよびプロパティを作成するには

1. **ソリューション エクスプローラー** でユーザー コントロールを右クリックし、 **[コードの表示]** をクリックします。

2. `ChartOptions` クラスにコードを追加して、`SelectionChanged` イベントと `Selection` プロパティを作成します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet13":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet13":::

### <a name="to-handle-the-checkedchanged-event-of-the-radio-buttons"></a>オプション ボタンの CheckedChanged イベントを処理するには

1. `CheckedChanged` オプション ボタンの `areaBlockChart` イベント ハンドラーでグラフの種類を設定し、イベントを発生させます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet14":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet14":::

2. `CheckedChanged` オプション ボタンの `barChart` イベント ハンドラーでグラフの種類を設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet15":::

3. `CheckedChanged` オプション ボタンの `columnChart` イベント ハンドラーでグラフの種類を設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet16":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet16":::

4. `CheckedChanged` オプション ボタンの `lineChart` イベント ハンドラーでグラフの種類を設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet17":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet17":::

5. C# では、オプション ボタンに対してイベント ハンドラーを追加する必要があります。 このコードを、`ChartOptions` への呼び出しの後で `InitializeComponent` コンストラクターに追加できます。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet18":::

## <a name="add-the-user-control-to-the-worksheet"></a>ワークシートにユーザー コントロールを追加する
 ソリューションをビルドすると、新しいユーザー コントロールが自動的に **ツールボックス** に追加されます。 その後、このコントロールを **ツールボックス** からワークシートへとドラッグできます。

### <a name="to-add-the-user-control-your-worksheet"></a>ワークシートにユーザー コントロールを追加するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     **ChartOptions** ユーザー コントロールが **ツールボックス** に追加されます。

2. **ソリューション エクスプローラー** で、**Sheet1.vb** または **Sheet1.cs** を右クリックし、 **[デザイナーの表示]** をクリックします。

3. **ChartOptions** コントロールを、**ツールボックス** からワークシートにドラッグします。

     `my_Excel_Chart_ChartOptions1` という新しいコントロールがプロジェクトに追加されます。

4. コントロールの名前を **ChartOptions1** に変更します。

## <a name="change-the-chart-type"></a>グラフの種類を変更する
 グラフの種類を変更するには、ユーザー コントロールで選択されたオプションに基づいてスタイルを設定するイベント ハンドラーを作成します。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>ワークシートに表示されるグラフの種類を変更するには

1. `Sheet1` クラスに次のイベント ハンドラーを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet19":::

2. C# では、次に示すように、ユーザー コントロールのイベント ハンドラーを <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベントに追加する必要があります。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet20":::

## <a name="test-the-application"></a>アプリケーションをテストする
 これで、ブックをテストし、オプション ボタンが選択されたときにグラフのスタイルが正しく設定されるかどうかを確認する準備ができました。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. オプション ボタンを選択するには

3. 選択した内容に合わせてグラフのスタイルが変わることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、ワークシートでオプション ボタンとグラフ スタイルを使用する基本的な方法について説明しました。 ここでは、次の作業を行います。

- プロジェクトを配置する。 詳細については、「[Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)」を参照してください。

- ボタンを使用してテキスト ボックスへデータを挿入する。 詳細については、「[チュートリアル: ボタンを使用してワークシートのテキスト ボックスにテキストを表示する](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)」を参照してください。

- チェック ボックスを使用して、ワークシートの書式設定を変更する。 詳細については、「[チュートリアル: CheckBox コントロールを使用したワークシートの書式設定の変更](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
