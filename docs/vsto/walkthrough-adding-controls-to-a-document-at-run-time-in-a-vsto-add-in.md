---
title: 実行時に VSTO アドインで文書にコントロールを追加する
description: リボンを使用して、ユーザーが Button クラスまたは RichTextContentControl インターフェイスを文書に追加できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- application-level add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to documents at run time
- documents [Office development in Visual Studio], adding controls at run time
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c2088a4d2ca81418ca16b51b53b0af38595d75b2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825395"
---
# <a name="walkthrough-add-controls-to-a-document-at-run-time-in-a-vsto-add-in"></a>チュートリアル: 実行時に VSTO アドインで文書にコントロールを追加する
  VSTO アドインを使用して、開いている Microsoft Office Word 文書にコントロールを追加できます。 このチュートリアルでは、リボンを使用してユーザーが文書に <xref:Microsoft.Office.Tools.Word.Controls.Button> または <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加できるようにする方法を説明します。

 **対象:** このトピックの情報は、Word 2010 の VSTO アドインのプロジェクトに適用されます。 詳細については、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

 このチュートリアルでは、次の作業について説明します。

- 新しい Word VSTO アドイン プロジェクトの作成。

- ドキュメントにコントロールを追加するためのユーザー インターフェイス (UI) の提供。

- 実行時のドキュメントへのコントロールの追加。

- ドキュメントからのコントロールの削除。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-a-new-word-add-in-project"></a>新しい Word アドイン プロジェクトを作成する
 まず Word VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-word-vsto-add-in-project"></a>新しい Word VSTO アドイン プロジェクトを作成するには

1. **WordDynamicControls** という名前で Word 用 VSTO アドイン プロジェクトを作成します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

2. **Microsoft.Office.Tools.Word.v4.0.Utilities.dll** アセンブリへの参照を追加します。 この参照は、このチュートリアルの後半でプログラムを使用して Windows フォーム コントロールをドキュメントに追加するのに必要です。

## <a name="provide-a-ui-to-add-controls-to-a-document"></a>ドキュメントにコントロールを追加するための UI を提供する
 Word のリボンにカスタム タブを追加します。 ユーザーはタブにあるチェック ボックスをオンにして、ドキュメントにコントロールを追加できます。

### <a name="to-provide-a-ui-to-add-controls-to-a-document"></a>ドキュメントにコントロールを追加するための UI を提供するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]** をクリックします。

3. 新しいリボンの名前を " **MyRibbon**" に変更し、 **[追加]** をクリックします。

    リボン デザイナーで **MyRibbon.cs** ファイルまたは **MyRibbon.vb** ファイルが開き、既定のタブとグループが表示されます。

4. リボン デザイナーで、 **group1** グループをクリックします。

5. **[プロパティ]** ウィンドウで、 **group1** の **[ラベル]** プロパティを **[コントロールの追加]** に変更します。

6. **ツールボックス** の **[Office リボン コントロール]** タブから、 **CheckBox** コントロールを **group1** にドラッグします。

7. **[CheckBox1]** をクリックしてオンにします。

8. **[プロパティ]** ウィンドウで、次のプロパティを変更します。

   | プロパティ | 値 |
   |-----------|-----------------------|
   | **名前** | **addButtonCheckBox** |
   | **Label** | **追加ボタン** |

9. **group1** に 2 つ目のチェック ボックスを追加し、次のプロパティを変更します。

   | プロパティ | 値 |
   |-----------|---------------------------|
   | **名前** | **addRichTextCheckBox** |
   | **Label** | **リッチ テキスト コントロールの追加** |

10. リボン デザイナーで **[ボタンの追加]** をダブルクリックします。

     <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> [ボタンの追加] **チェック ボックスの** イベント ハンドラーがコード エディターで開きます。

11. リボン デザイナーに戻り、 **[リッチ テキスト コントロールの追加]** をダブルクリックします。

     <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> [リッチ テキスト コントロールの追加] **チェック ボックスの** イベント ハンドラーがコード エディターで開きます。

    このチュートリアルの後半で、アクティブなドキュメントにコントロールを追加および削除するためのコードをこれらのイベント ハンドラーに追加します。

## <a name="add-and-remove-controls-on-the-active-document"></a>アクティブなドキュメントでコントロールを追加または削除する
 VSTO アドインのコードでは、コントロールを追加するには、その前にアクティブなドキュメントを <xref:Microsoft.Office.Tools.Word.Document>*ホスト項目* に変換する必要があります。 Office ソリューションではマネージド コントロールを追加できるのはホスト項目に対してだけです。これはコントロールのコンテナーとして機能します。 VSTO アドイン プロジェクトでは、`GetVstoObject` メソッドを使用すると、実行時にホスト項目を作成できます。

 アクティブなドキュメントに `ThisAddIn` または <xref:Microsoft.Office.Tools.Word.Controls.Button> を追加または削除するために呼び出せるメソッドを <xref:Microsoft.Office.Tools.Word.RichTextContentControl> クラスに追加します。 このチュートリアルの後半で、これらのメソッドをリボンのチェック ボックスの <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> イベント ハンドラーから呼び出します。

### <a name="to-add-and-remove-controls-on-the-active-document"></a>アクティブなドキュメントでコントロールを追加または削除するには

1. **ソリューション エクスプローラー** で *ThisAddIn.cs* または *ThisAddIn.vb* をダブルクリックして、コード エディターでファイルを開きます。

2. 次のコードを `ThisAddIn` クラスに追加します。 このコードは、ドキュメントに追加されるコントロールを表す <xref:Microsoft.Office.Tools.Word.Controls.Button> オブジェクトと <xref:Microsoft.Office.Tools.Word.RichTextContentControl> オブジェクトを宣言します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet1":::

3. `ThisAddIn` クラスに次のメソッドを追加します。 ユーザーがリボンの **[ボタンの追加]** チェック ボックスをクリックしてこれがオンになると、このメソッドによって <xref:Microsoft.Office.Tools.Word.Controls.Button> がドキュメントの現在の選択項目に追加されます。チェック ボックスがオフになると <xref:Microsoft.Office.Tools.Word.Controls.Button> が削除されます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet2":::

4. `ThisAddIn` クラスに次のメソッドを追加します。 ユーザーがリボンの **[リッチ テキスト コントロールの追加]** チェック ボックスをクリックしてこれがオンになると、このメソッドによって <xref:Microsoft.Office.Tools.Word.RichTextContentControl> がドキュメントの現在の選択項目に追加されます。チェック ボックスがオフになると <xref:Microsoft.Office.Tools.Word.RichTextContentControl> が削除されます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet3":::

## <a name="remove-the-button-control-when-the-document-is-saved"></a>ドキュメントを保存するときにボタン コントロールを削除する
 ドキュメントを保存して閉じるときに Windows フォーム コントロールは保存されません。 ただし、各コントロールの ActiveX ラッパーはドキュメントに残るため、エンド ユーザーがドキュメントを再び開くときにこのラッパーの枠線が表示される場合があります。 VSTO アドインに作成された Windows フォーム コントロールを動的にクリーン アップする方法は、いくつかあります。このチュートリアルでは、ドキュメントを保存するときに、<xref:Microsoft.Office.Tools.Word.Controls.Button> コントロールをプログラムで削除します。

### <a name="to-remove-the-button-control-when-the-document-is-saved"></a>ドキュメントを保存するときにボタン コントロールを削除するには

1. *ThisAddIn.cs* または *ThisAddIn.vb* コード ファイルで、次のメソッドを `ThisAddIn` クラスに追加します。 このメソッドは、 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベントのイベント ハンドラーです。 保存されるドキュメントに <xref:Microsoft.Office.Tools.Word.Document> ホスト項目が関連付けられている場合、イベント ハンドラーはホスト項目を取得し、 <xref:Microsoft.Office.Tools.Word.Controls.Button> コントロールが存在する場合にそれを削除します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet4":::

2. C# では、 `ThisAddIn_Startup` イベント ハンドラーに次のコードを追加します。 C# では、 `Application_DocumentBeforeSave` イベント ハンドラーを <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベントに接続するためにこのコードが必要です。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet5":::

## <a name="add-and-remove-controls-when-the-user-clicks-the-check-boxes-on-the-ribbon"></a>ユーザーがリボンのチェック ボックスをクリックしたときにコントロールを追加または削除する
 最後に、リボンに追加したチェック ボックスの <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> イベント ハンドラーに対し、ドキュメント上のコントロールを追加または削除するための変更を加えます。

### <a name="to-add-or-remove-controls-when-the-user-clicks-the-check-boxes-on-the-ribbon"></a>ユーザーがリボンのチェック ボックスをクリックしたときにコントロールを追加または削除するには

1. *MyRibbon.cs* または *MyRibbon.vb* コード ファイルで、生成された `addButtonCheckBox_Click` および `addRichTextCheckBox_Click` イベント ハンドラーを次のコードで置き換えます。 このコードは、このチュートリアルの前半で `ToggleButtonOnDocument` クラスに追加した `ToggleRichTextControlOnDocument` および `ThisAddIn` メソッドを呼び出すように、これらのイベント ハンドラーを再定義します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/MyRibbon.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/MyRibbon.cs" id="Snippet6":::

## <a name="test-the-solution"></a>ソリューションをテストする
 リボンのカスタム タブからコントロールを選んでドキュメントに追加します。 ドキュメントを保存すると、 <xref:Microsoft.Office.Tools.Word.Controls.Button> コントロールが削除されます。

### <a name="to-test-the-solution"></a>ソリューションをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. アクティブなドキュメントで **Enter** キーを何度か押して、ドキュメントに新しい空の段落を追加します。

3. 最初の段落を選びます。

4. **[アドイン]** タブをクリックします。

5. **[コントロールの追加]** グループで **[ボタンの追加]** をクリックします。

     最初の段落にボタンが表示されます。

6. 最後の段落を選びます。

7. **[コントロールの追加]** グループで **[リッチ テキスト コントロールの追加]** をクリックします。

     リッチ テキスト コンテンツのコントロールが最後の段落に追加されます。

8. ドキュメントを保存します。

     ボタンがドキュメントから削除されます。

## <a name="next-steps"></a>次のステップ
 VSTO アドインのコントロールについて詳しくは、次の各トピックをご覧ください。

- 実行時に他のさまざまな種類のコントロールをドキュメントに追加したり、ドキュメントを再び開くときにコントロールを再作成したりする方法を示すサンプルについては、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」にある Word アドイン ダイナミック コントロールのサンプルをご覧ください。

- Excel 用の VSTO アドインを使用してワークシートにコントロールを追加する方法を示すチュートリアルについては、「[チュートリアル: VSTO アドイン プロジェクトの実行時にワークシートにコントロールを追加する](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Word ソリューション](../vsto/word-solutions.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Office ドキュメントでのダイナミック コントロールの永続化](../vsto/persisting-dynamic-controls-in-office-documents.md)
- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)
- [実行時に VSTO アドインで Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
