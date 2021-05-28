---
title: ボタンを使用してワークシートのテキスト ボックスにテキストを表示する
description: Microsoft Excel ワークシートでボタンやテキスト ボックスを使用する操作の基本について説明します。 また、Visual Studio の Office 開発ツールを使用して Excel プロジェクトを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], displaying worksheets
- worksheets, displaying text
- text boxes, displaying text in worksheets
- text [Office development in Visual Studio], text boxes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b1209bf903f5a5b9c0005d9ba4ba6a891752aedd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827787"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-worksheet-using-a-button"></a>チュートリアル: ボタンを使用してワークシートのテキスト ボックスにテキストを表示する
  このチュートリアルでは、Microsoft Office Excel ワークシートでボタンとテキスト ボックスを使用する方法、および Visual Studio の Office 開発ツールを使用して Excel プロジェクトを作成する方法の基本について説明します。 完全なサンプルの結果を確認するには、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」にある Excel コントロールのサンプルを参照してください。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- ワークシートにコントロールを追加する。

- ボタンがクリックされたときに、テキスト ボックスにデータを設定する。

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

1. **My Excel Button** という名前で Excel ブック プロジェクトを作成します。 **[新しいドキュメントを作成]** が選択されていることを確認してください。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Excel Button** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 このチュートリアルでは、最初のワークシートにボタンとテキスト ボックスが必要です。

### <a name="to-add-a-button-and-a-text-box"></a>ボタンとテキスト ボックスを追加するには

1. **My Excel Button.xlsx** ブックが Visual Studio デザイナーで開かれ、`Sheet1` が表示されていることを確認します。

2. ツールボックスの **[コモン コントロール]** タブから、<xref:Microsoft.Office.Tools.Excel.Controls.TextBox> を `Sheet1` にドラッグします。

3. **[表示]** メニューから、 **[プロパティ ウィンドウ]** を選択します。

4. **プロパティ** ウィンドウのドロップダウン ボックスに **[TextBox1]** が表示されていることを確認し、このテキスト ボックスの **[名前]** プロパティを「**displayText**」に変更します。

5. **Button** コントロールを `Sheet1` にドラッグし、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**insertText**|
   |**[テキスト]**|**テキストを挿入**|

   次は、ボタンがクリックされたときに実行されるコードを記述します。

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキスト ボックスにデータを設定する
 ユーザーがボタンをクリックするたびに、テキスト ボックスに **Hello World!** が追加されるようにします。

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキスト ボックスに書き込むには

1. **ソリューション エクスプローラー** で **[Sheet1]** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet11":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet11":::

3. C# では、次に示すように、イベント ハンドラーを <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベントに追加する必要があります。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet12":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ブックをテストしましょう。ボタンをクリックした時に、メッセージ "**Hello World!** " がテキスト ボックスに表示されることを確認します。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. ボタンをクリックします。

3. テキスト ボックスに **Hello World!** と表示されることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Excel ワークシートでボタンとテキスト ボックスを使用する際の基本事項について説明しました。 ここでは、次の作業を行います。

- プロジェクトを配置する。 詳細については、「[Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)」を参照してください。

- チェック ボックスを使用して書式を変更する。 詳細については、「[チュートリアル: CheckBox コントロールを使用したワークシートの書式設定の変更](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
- [Office ドキュメントでの Windows フォーム コントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
