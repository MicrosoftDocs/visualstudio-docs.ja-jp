---
title: 'チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する'
description: Microsoft Word 文書に操作ウィンドウを作成します。 操作ウィンドウには、入力を収集し、そのテキストをドキュメントに送信する 2 つのコントロールが含まれていることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1ac42954e32b30a293abbe031218213948fb103a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824979"
---
# <a name="walkthrough-insert-text-into-a-document-from-an-actions-pane"></a>チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する
  このチュートリアルでは、Microsoft Office Word 文書に操作ウィンドウを作成する方法について説明します。 操作ウィンドウには、入力を収集し、そのテキストをドキュメントに送信する 2 つのコントロールが含まれています。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- 操作ウィンドウ コントロールの Windows フォーム コントロールを使用して、インターフェイスをデザインする。

- アプリケーションが開いたときに操作ウィンドウを表示する。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Basic Actions Pane** という名前の Word 文書プロジェクトを作成します。 ウィザードで、 **[新しいドキュメントの作成]** を選択します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Word 文書が Visual Studio のデザイナーで開かれ、**My Basic Actions Pane** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-text-and-bookmarks-to-the-document"></a>文書にテキストとブックマークを追加する
 操作ウィンドウは、文書内のブックマークにテキストを送信します。 文書をデザインするために、いくつかのテキストを入力して基本フォームを作成します。

### <a name="to-add-text-to-your-document"></a>文書にテキストを追加するには

1. Word 文書に次のテキストを入力します。

    **2008 年 3 月 21 日**

    **名前**

    **アドレス**

    **これは、Word の基本的な操作ウィンドウの例です。**

   <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを文書に追加するには、Visual Studio の **ツールボックス** からドラッグするか、Word の **[ブックマーク]** ダイアログ ボックスを使用します。

### <a name="to-add-a-bookmark-control-to-your-document"></a>ドキュメントにブックマーク コントロールを追加するには

1. **ツールボックス** の **[Word コントロール]** タブから、<xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを文書にドラッグします。

     **[ブックマーク コントロールの追加]** ダイアログ ボックスが表示されます。

2. 段落記号を含めずに "**名前**" という語を選択し、 **[OK]** をクリックします。

    > [!NOTE]
    > 段落記号はブックマークの外側にある必要があります。 文書に段落記号が表示されていない場合は、 **[ツール]** メニューの **[Microsoft Office Word ツール]** をポイントし、 **[オプション]** をクリックします。 **[表示]** タブをクリックし、 **[オプション]** ダイアログ ボックスの **[編集記号の表示]** セクションで **[段落記号]** チェック ボックスをオンにします。

3. **[プロパティ]** ウィンドウで、**Name** プロパティを **Bookmark1** から **showName** に変更します。

4. 段落記号を含めずに "**アドレス**" という語を選択します。

5. リボンの **[挿入]** タブで、 **[リンク]** グループの **[ブックマーク]** をクリックします。

6. **[ブックマーク]** ダイアログ ボックスで、 **[ブックマーク名]** に「**showAddress**」と入力し、 **[追加]** をクリックします。

## <a name="add-controls-to-the-actions-pane"></a>操作ウィンドウにコントロールを追加する
 操作ウィンドウのインターフェイスをデザインするために、プロジェクトに操作ウィンドウ コントロールを追加した後、操作ウィンドウ コントロールに Windows フォーム コントロールを追加します。

### <a name="to-add-an-actions-pane-control"></a>操作ウィンドウ コントロールを追加するには

1. **ソリューション エクスプローラー** で、**My Basic Actions Pane** プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[操作ウィンドウ コントロール**] をクリックし、コントロールの名前を **InsertTextControl** と指定して、 **[追加]** をクリックします。

#### <a name="to-add-windows-form-controls-to-the-actions-pane-control"></a>Windows フォーム コントロールを操作ウィンドウ コントロールに追加するには

1. デザイナーに操作ウィンドウ コントロールが表示されていない場合は、**InsertTextControl** をダブルクリックします。

2. **ツールボックス** の **[コモン コントロール]** タブから、**Label** コントロールを操作ウィンドウ コントロールにドラッグします。

3. Label コントロールの **Text** プロパティを "**名前**" に変更します。

4. 操作ウィンドウ コントロールに **Textbox** コントロールを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**getName**|
    |**[サイズ]**|**130, 20**|

5. 操作ウィンドウ コントロールに 2 つ目の **Label** コントロールを追加し、**Text** プロパティを "**アドレス**" に変更します。

6. 操作ウィンドウ コントロールに 2 つ目の **Textbox** コントロールを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**getAddress**|
    |**Accepts Return**|**True**|
    |**Multiline**|**True**|
    |**[サイズ]**|**130, 40**|

7. 操作ウィンドウ コントロールに **Button** コントロールを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**addText**|
    |**[テキスト]**|**[挿入]**|

## <a name="add-code-to-insert-text-into-the-document"></a>文書にテキストを挿入するコードを追加する
 操作ウィンドウで、テキスト ボックスのテキストを文書内の適切な <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールに挿入するコードを記述します。 `Globals` クラスを使用して、操作ウィンドウのコントロールから文書のコントロールにアクセスできます。 詳細については、「[Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。

### <a name="to-insert-text-from-the-actions-pane-in-a-bookmark-in-the-document"></a>操作ウィンドウから文書内のブックマークにテキストを挿入するには

1. **addText** ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/InsertTextControl.vb" id="Snippet8":::

2. C# では、ボタン クリックのイベント ハンドラーを追加する必要があります。 このコードは、`InsertTextControl` コンストラクター内の、`InitializeComponent` の呼び出しの後に配置できます。 イベント ハンドラーの作成方法については、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs" id="Snippet9":::

## <a name="add-code-to-show-the-actions-pane"></a>操作ウィンドウを表示するコードを追加する
 操作ウィンドウを表示するには、作成したコントロールをコントロール コレクションに追加します。

### <a name="to-show-the-actions-pane"></a>操作ウィンドウを表示するには

1. `ThisDocument` クラスに、操作ウィンドウ コントロールの新規インスタンスを作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet10":::

2. `ThisDocument` の <xref:Microsoft.Office.Tools.Word.Document.Startup> イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet11":::

## <a name="test-the-application"></a>アプリケーションをテストする
 文書をテストして、文書を開いたときに操作ウィンドウが開くことと、ボタンをクリックしたときにテキスト ボックスに入力したテキストがブックマークに挿入されることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. 操作ウィンドウが表示されていることを確認します。

3. 操作ウィンドウのテキスト ボックスに名前とアドレスを入力し、 **[挿入]** をクリックします。

## <a name="next-steps"></a>次のステップ
 ここでは、次の作業を行います。

- Excel で操作ウィンドウを作成する。 詳細については、「[方法: Excel ブックに操作ウィンドウを追加する](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))」を参照してください。

- 操作ウィンドウ上のコントロールにデータをバインドする。 詳細については、「[チュートリアル: Word の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [方法: Excel ブックに操作ウィンドウを追加する](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))
- [方法: 操作ウィンドウ上のコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Bookmark コントロール](../vsto/bookmark-control.md)
