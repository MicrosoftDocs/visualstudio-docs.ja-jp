---
title: 'チュートリアル: Windows フォームを使用してデータを収集します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], Windows Forms
- Windows Forms [Office development in Visual Studio], collecting data
- forms [Office development in Visual Studio], walkthroughs
- worksheets [Office development in Visual Studio], collecting data
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 11e9b73671a8c4b03c33169739ea8fd02b486568
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53926630"
---
# <a name="walkthrough-collect-data-by-using-a-windows-form"></a>チュートリアル: Windows フォームを使用してデータを収集します。
  このチュートリアルでは、Microsoft Office Excel のドキュメント レベルのカスタマイズから Windows フォームを開き、ユーザーから情報を収集し、その情報をワークシートのセルに書き込む方法について説明します。  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
 このチュートリアルでは具体的には Excel のドキュメントレベルのプロジェクトを使用していますが、チュートリアルで示される概念は他の Office プロジェクトに適用できます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。  
  
> [!NOTE]  
>  次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。  
  
## <a name="create-a-new-project"></a>新しいプロジェクトを作成する  
 まず、Excel ブック プロジェクトを作成します。  
  
### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには  
  
1.  **WinFormInput**という名前で Excel ブック プロジェクトを作成し、ウィザードで **[新しいドキュメントの作成]** を選択します。 詳細については、次を参照してください。[方法: Visual Studio での Office プロジェクトの作成](../vsto/how-to-create-office-projects-in-visual-studio.md)です。  
  
     Visual Studio により新しい Excel ブックがデザイナーで開き、 **WinFormInput** プロジェクトが **ソリューション エクスプローラー**に追加されます。  
  
## <a name="add-a-namedrange-control-to-the-worksheet"></a>ワークシートに NamedRange コントロールを追加します。  
  
### <a name="to-add-a-named-range-to-sheet1"></a>Sheet1 に名前付き範囲を追加するには  
  
1.  **でセル** A1 `Sheet1`を選択します。  
  
2.  **[名前]** ボックスに **formInput**と入力します。  
  
     **[名前]** ボックスは数式バーの左側、ワークシートの列 **A** の真上にあります。  
  
3.  **Enter** キーを押します。  
  
     <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールがセル **A1**に追加されます。 ワークシート上には表示されませんが、セル **A1** を選択すると、 **[名前]** ボックス (左側のワークシートの真上) および **[プロパティ]** ウィンドウに **formInput** と表示されます。  
  
## <a name="add-a-windows-form-to-the-project"></a>Windows フォームをプロジェクトに追加します。  
 ユーザーに情報を要求するための Windows フォームを作成します。  
  
### <a name="to-add-a-windows-form"></a>Windows フォームを追加するには  
  
1. **ソリューション エクスプローラー** でプロジェクト **WinFormInput**を選択します。  
  
2. **[プロジェクト]** メニューの **[Windows フォームの追加]** をクリックします。  
  
3. フォームに **GetInputString.vb** または **GetInputString.cs**という名前を付けてから、 **[追加]** をクリックします。  
  
    デザイナーで新しいフォームが開きます。  
  
4. フォームに <xref:System.Windows.Forms.TextBox> および <xref:System.Windows.Forms.Button> を追加します。  
  
5. ボタンを選択し、 **[プロパティ]** ウィンドウでプロパティ **[テキスト]** を見つけ出し、テキストを **OK**に変更します。  
  
   次に、ユーザーの情報を収集するためのコードを `ThisWorkbook.vb` または `ThisWorkbook.cs` に追加します。  
  
## <a name="display-the-windows-form-and-collecting-information"></a>Windows フォームと収集情報を表示します。  
 `GetInputString` Windows フォームのインスタンスを作成しそれを表示してから、ワークシート内のセルにユーザーの情報を書き込みます。  
  
#### <a name="to-display-the-form-and-collect-information"></a>フォームを表示し、情報を収集するには  
  
1. **ソリューション エクスプローラー** で **ThisWorkbook.vb** または **ThisWorkbook.cs**を右クリックしてから、 **[コードの表示]** をクリックします。  
  
2. <xref:Microsoft.Office.Tools.Excel.Workbook.Open> の `ThisWorkbook`イベント ハンドラーで、次のコードを追加して、フォーム `GetInputString` の変数を宣言してから、フォームを表示します。  
  
   > [!NOTE]  
   >  C# では、次のようにイベント ハンドラーを <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> イベントに追加する必要があります。 イベント ハンドラーの作成方法の詳細については、次を参照してください。[方法。Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)します。  
  
    [!code-csharp[Trin_VstcoreProgrammingCollectingData#1](../vsto/codesnippet/CSharp/WinFormInputCS/ThisWorkbook.cs#1)]
    [!code-vb[Trin_VstcoreProgrammingCollectingData#1](../vsto/codesnippet/VisualBasic/WinFormInput/ThisWorkbook.vb#1)]  
  
3. テキストを名前付き範囲に書き込む `WriteStringToCell` という名前のメソッドを作成します。 このメソッドはフォームから呼び出され、ユーザーの入力は <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールである `formInput`のセル **A1**に渡されます。  
  
    [!code-csharp[Trin_VstcoreProgrammingCollectingData#2](../vsto/codesnippet/CSharp/WinFormInputCS/ThisWorkbook.cs#2)]
    [!code-vb[Trin_VstcoreProgrammingCollectingData#2](../vsto/codesnippet/VisualBasic/WinFormInput/ThisWorkbook.vb#2)]  
  
   次に、ボタンのクリック イベントを処理するためのコードをフォームに追加します。  
  
## <a name="send-information-to-the-worksheet"></a>ワークシートに情報を送信します。  
  
### <a name="to-send-information-to-the-worksheet"></a>ワークシートに情報を送信するには  
  
1.  **ソリューション エクスプローラー** で **GetInputString**を右クリックし、 **[デザイナーの表示]** をクリックします。  
  
2.  ボタンを右クリックして、ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーが追加されたコード ファイルを開きます。  
  
3.  テキスト ボックスから入力を受け取り、関数 `WriteStringToCell`に送信してから、フォームを閉じるコードをイベント ハンドラーに追加します。  
  
     [!code-csharp[Trin_VstcoreProgrammingCollectingData#3](../vsto/codesnippet/CSharp/WinFormInputCS/GetInputString.cs#3)]
     [!code-vb[Trin_VstcoreProgrammingCollectingData#3](../vsto/codesnippet/VisualBasic/WinFormInput/GetInputString.vb#3)]  
  
## <a name="test"></a>テスト  
 これで、プロジェクトを実行できます。 Windows フォームが表示され、ワークシートに入力が表示されます。  
  
### <a name="to-test-your-workbook"></a>ブックをテストするには  
  
1.  キーを押して**F5**プロジェクトを実行します。  
  
2.  Windows フォームが表示されることを確認します。  
  
3.  テキスト ボックスに **Hello World** と入力し、 **[OK]** をクリックします。  
  
4.  ワークシートのセル **A1** に **Hello World** と表示されることを確認します。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルでは、Windows フォームを表示しワークシートにデータを渡すための基本操作を説明しました。 これ以外にも、次の操作が可能です。  
  
-   Excel ブックまたは Word 文書で Windows フォーム コントロールを使用する。 詳細については、次を参照してください。 [Windows フォーム コントロールの Office ドキュメントの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)します。  
  
-   ドキュメント レベルのカスタマイズまたは VSTO アドインから Microsoft Office アプリケーションのユーザー インターフェイスを変更します。 詳細については、次を参照してください。 [Office UI のカスタマイズ](../vsto/office-ui-customization.md)します。  
  
## <a name="see-also"></a>関連項目  
 [Office ソリューションを開発します。](../vsto/developing-office-solutions.md)   
 [Office ソリューションでコードを記述します。](../vsto/writing-code-in-office-solutions.md)   
 [VSTO アドインをプログラミングします。](../vsto/programming-vsto-add-ins.md)   
 [プログラムのドキュメント レベルのカスタマイズ](../vsto/programming-document-level-customizations.md)   
 [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)   
 [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)  
