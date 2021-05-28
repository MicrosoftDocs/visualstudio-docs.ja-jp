---
title: CheckBox コントロールを使用してワークシート書式を変更する
description: Visual Studio の Office 開発ツールを使ってコードを作成し、プロジェクトに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, changing formatting using managed controls
- worksheets, check box controls
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6f649fad99b8d94cc650ecda57e10b423b14194e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826435"
---
# <a name="walkthrough-change-worksheet-formatting-using-checkbox-controls"></a>チュートリアル: CheckBox コントロールを使用してワークシートの書式を変更する
  このチュートリアルでは、Microsoft Office Excel ワークシートでチェック ボックスを使って書式を変更する基本的な方法について説明します。 コードを作成してプロジェクトに追加するには、Visual Studio の Office 開発ツールを使用します。 完全なサンプルの結果を確認するには、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」にある Excel コントロールのサンプルを参照してください。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- ワークシートにテキストとコントロールを追加する。

- オプションが選択されたときにテキストを書式設定する。

- プロジェクトをテストする。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する
 この手順では、Visual Studio を使って Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Excel Formatting** という名前で Excel ブック プロジェクトを作成します。 **[新しいドキュメントの作成]** が選択されていることを確認してください。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Excel Formatting** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-text-and-controls-to-the-worksheet"></a>ワークシートにテキストとコントロールを追加する
 このチュートリアルでは、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールに 3 つの <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> コントロールといくつかのテキストが必要になります。

### <a name="to-add-three-check-boxes"></a>3 つのチェック ボックスを追加するには

1. Visual Studio デザイナーでブックが開かれていて、`Sheet1` が開いていることを確認します。

2. **ツールボックス** の **[コモン コントロール]** タブから、<xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> コントロールを **Sheet1** のセル **B2** 内か、その近くにドラッグします。

3. **[表示]** メニューから、**プロパティ** ウィンドウを選択します。

4. **プロパティ** ウィンドウのオブジェクト名リスト ボックスに **Checkbox1** が表示されていることを確認し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyBoldFont**|
    |**[テキスト]**|**太字**|

5. 2 つ目のチェック ボックスをセル **B4** またはその近くにドラッグし、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyItalicFont**|
    |**[テキスト]**|**斜体**|

6. 3 つ目のチェック ボックスをセル **B6** またはその近くにドラッグし、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyUnderlineFont**|
    |**[テキスト]**|**下線**|

7. **Ctrl** キーを押しながら、3 つのチェック ボックス コントロールをすべて選択します。

8. Excel の [書式] タブの [配置] グループで、 **[配置]** をクリックし、 **[左揃え]** をクリックします。

     3 つのチェック ボックス コントロールが、選択した最初のコントロールの位置に、左揃えで配置されます。

     次に、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをワークシートにドラッグします。

    > [!NOTE]
    > **[名前]** ボックスに「**textFont**」と入力して <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを追加することもできます。

#### <a name="to-add-text-to-a-namedrange-control"></a>NamedRange コントロールにテキストを追加するには

1. ツールボックス の **[Excel コントロール]** タブから、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをセル **B9** にドラッグします。

2. 編集可能なテキスト ボックスに **$B$9** と表示され、セル **B9** が選択されていることを確認します。 そうなっていない場合は、セル **B9** をクリックして選択します。

3. **[OK]** をクリックします。

4. セル **B9** が、`NamedRange1` という名前の範囲になります。

    ワークシート上には表示されませんが、セル **B9** を選択すると、**名前ボックス** (ワークシートの真上の左側) に `NamedRange1` と表示されます。

5. **プロパティ** ウィンドウのオブジェクト名リスト ボックスに **NamedRange1** が表示されていることを確認し、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**textFont**|
   |**Value2**|**このテキストの書式を変更するには、チェック ボックスをオンにします。**|

   次に、オプションが選択されたときにテキストの書式を設定するためのコードを記述します。

## <a name="format-the-text-when-an-option-is-selected"></a>オプションが選択されたときにテキストを書式設定する
 このセクションでは、ユーザーが書式設定オプションを選択したときに、ワークシート内のテキストの書式が変更されるようにするためのコードを記述します。

### <a name="to-change-formatting-when-a-check-box-is-selected"></a>チェック ボックスがオンになったときに書式設定を変更するには

1. **Sheet1** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. `applyBoldFont` チェック ボックスの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに、次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet7":::

3. `applyItalicFont` チェック ボックスの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに、次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet8":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet8":::

4. `applyUnderlineFont` チェック ボックスの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに、次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet9":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet9":::

5. C# では、次に示すように、チェック ボックスのイベント ハンドラーを <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベントに追加する必要があります。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ブックをテストして、チェック ボックスがオンまたはオフになったときにテキストが正しく書式設定されることを確認しましょう。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. チェック ボックスをオンまたはオフにします。

3. テキストが正しく書式設定されることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Excel ワークシートでチェック ボックスを使って、テキストを書式設定する基本的な方法について説明しました。 ここでは、次の作業を行います。

- プロジェクトを配置する。 詳しくは、「[ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)」をご覧ください。
- ボタンを使用してテキスト ボックスへデータを挿入する。 詳細については、「[チュートリアル: ボタンを使用してワークシートのテキスト ボックスにテキストを表示する](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ドキュメントでの Windows フォーム コントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
