---
title: CheckBox コントロールを使用してドキュメント書式を変更する
description: Microsoft Word のドキュメントレベルのカスタマイズで、Windows フォーム コントロールを使ってテキストの書式設定を変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word documents, changing formatting using controls
- documents [Office development in Visual Studio], formatting
- check boxes, Word documents
- documents [Office development in Visual Studio], check box controls
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3f6fbb91c37fd8956860eed8e4d39f8b0a8c1a0e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824420"
---
# <a name="walkthrough-change-document-formatting-using-checkbox-controls"></a>チュートリアル: CheckBox コントロールを使用してドキュメントの書式を変更する
  このチュートリアルでは、Microsoft Office Word のドキュメントレベルのカスタマイズで、Windows フォーム コントロールを使ってテキストの書式設定を変更する方法について説明します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- デザイン時に、ドキュメント レベルのプロジェクト内のドキュメントにテキストとコントロールを追加する。

- オプションが選択されたときにテキストを書式設定する。

  完全なサンプルの結果を確認するには、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」にある Word コントロールのサンプルを参照してください。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する
 最初に、Word 文書のプロジェクトを作成します。

### <a name="create-a-new-project"></a>新しいプロジェクトを作成する

1. 「**My Word Formatting**」という名前の Word 文書プロジェクトを作成します。 ウィザードで、 **[新規ドキュメントの作成]** をクリックします。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Word 文書が Visual Studio のデザイナーで開かれ、**My Word Formatting** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-text-and-controls-to-the-word-document"></a>Word 文書にテキストとコントロールを追加する
 このチュートリアルでは、3 つのチェック ボックスと、<xref:Microsoft.Office.Tools.Word.Bookmark> コントロール内のテキストを Word 文書に追加します。 これらのチェック ボックスには、テキストを書式設定するためのオプションがユーザー向けに表示されます。

### <a name="add-three-check-boxes"></a>3 つのチェック ボックスを追加する

1. Visual Studio デザイナーで文書が開いていることを確認します。

2. **ツールボックス** の **[コモン コントロール]** タブから、1 つ目の <xref:Microsoft.Office.Tools.Word.Controls.CheckBox> コントロールを文書にドラッグします。

3. **[プロパティ]** ウィンドウで、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyBoldFont**|
    |**[テキスト]**|**太字**|

4. **Enter** キーを押して、1 つ目のチェック ボックスの下に挿入ポイントを移動します。

5. `ApplyBoldFont` チェック ボックスの下のドキュメントに 2 つ目のチェック ボックスを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyItalicFont**|
    |**[テキスト]**|**斜体**|

6. **Enter** キーを押して、2 つ目のチェック ボックスの下に挿入ポイントを移動します。

7. `ApplyItalicFont` チェック ボックスの下のドキュメントに 3 つ目のチェック ボックスを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyUnderlineFont**|
    |**[テキスト]**|**下線**|

### <a name="add-text-and-a-bookmark-control"></a>テキストとブックマーク コントロールを追加する

1. カーソル位置をチェック ボックス コントロールの下に移動し、次のテキストを入力します。

    **このテキストの書式を変更するには、チェック ボックスをオンにします。**

2. **ツールボックス** の **[Word コントロール]** タブから、<xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを文書にドラッグします。

    **[ブックマーク コントロールの追加]** ダイアログ ボックスが表示されます。

3. ドキュメントに追加したテキストを選択し、 **[OK]** をクリックします。

    **Bookmark1** という名前の <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールが、ドキュメント内の選択したテキストに追加されます。

4. **プロパティ** ウィンドウで、 **(オブジェクト名)** プロパティの値を **fontText** に変更します。

   次に、チェック ボックスがオンまたはオフになったときにテキストの書式を設定するためのコードを記述します。

## <a name="format-the-text-when-a-check-box-is-checked-or-cleared"></a>チェック ボックスがオンまたはオフになったときにテキストの書式を設定する
 ユーザーが書式設定オプションを選択した場合には、ドキュメント内のテキストの書式を変更します。

### <a name="change-formatting-when-a-check-box-is-selected"></a>チェック ボックスがオンになったときに書式設定を変更する

1. **ソリューション エクスプローラー** で `ThisDocument` を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. C# の場合のみ、次の定数を **ThisDocument** クラスに追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet2":::

3. `applyBoldFont` チェック ボックスの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに、次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet3":::

4. `applyItalicFont` チェック ボックスの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに、次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet4":::

5. `applyUnderlineFont` チェック ボックスの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに、次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet5":::

6. C# では、テキスト ボックスのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに追加する必要があります。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet6":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ドキュメントをテストして、チェック ボックスがオンまたはオフになったときにテキストが正しく書式設定されることを確認しましょう。

### <a name="test-your-document"></a>ドキュメントをテストする

1. **F5** キーを押してプロジェクトを実行します。

2. チェック ボックスをオンまたはオフにします。

3. テキストが正しく書式設定されることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Word 文書でチェック ボックスを使用して、テキストの書式をプログラムによって変更するための基本的な方法について説明しました。 ここでは、次の作業を行います。

- ボタンを使用してテキスト ボックスへデータを挿入する。 詳しくは、「[チュートリアル: ボタンを使用してドキュメントのテキスト ボックスにテキストを表示する](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)」をご覧ください。

- オプション ボタンを使用してグラフのスタイルを選択する。 詳しくは、「[チュートリアル: ラジオ ボタンを使用してドキュメントのグラフを更新する](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)」をご覧ください。

## <a name="see-also"></a>関連項目
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ドキュメントでの Windows フォーム コントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
