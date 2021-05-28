---
title: 'チュートリアル: ブックマークのショートカット メニューを作成する'
description: Microsoft Word のドキュメント レベルのカスタマイズを使用してブックマーク コントロールのショートカット メニューを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context menus, Word
- Bookmark control, events
- shortcut menus, Word
- menus, creating in Office applications
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 48381d452b0c67a34581092a47896aba60e7125c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826305"
---
# <a name="walkthrough-create-shortcut-menus-for-bookmarks"></a>チュートリアル: ブックマークのショートカット メニューを作成する
  このチュートリアルでは、Word のドキュメント レベルのカスタマイズを使用して <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールのショートカット メニューを作成する方法を示します。 ユーザーがブックマーク内のテキストを右クリックすると、ショートカット メニューにテキストの書式設定オプションが表示されます。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- [プロジェクトを作成する](#BKMK_CreateProject)。

- [文書にテキストとブックマークを追加する](#BKMK_addtextandbookmarks)。

- [ショートカット メニューにコマンドを追加する](#BKMK_AddCmndsShortMenu)。

- [ブックマーク内のテキストを書式設定する](#BKMK_formattextbkmk)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]

## <a name="create-the-project"></a><a name="BKMK_CreateProject"></a> プロジェクトを作成する
 まず、Visual Studio で Word 文書プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

- **My Bookmark Shortcut Menu** という名前の Word 文書プロジェクトを作成します。 ウィザードで、 **[新しいドキュメントを作成]** を選択します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Word 文書が Visual Studio のデザイナーで開かれ、**My Bookmark Shortcut Menu** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-text-and-bookmarks-to-the-document"></a><a name="BKMK_addtextandbookmarks"></a> 文書にテキストとブックマークを追加する
 文書にテキストを追加し、部分的に重なった 2 つのブックマークを追加します。

### <a name="to-add-text-to-your-document"></a>文書にテキストを追加するには

- プロジェクトのデザイナーで表示されているドキュメントに次のテキストを入力します。

     **This is an example of creating a shortcut menu when you right-click the text in a bookmark.**

### <a name="to-add-a-bookmark-control-to-your-document"></a>ドキュメントにブックマーク コントロールを追加するには

1. **ツールボックス** の **[Word コントロール]** タブから、<xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを ドキュメントにドラッグします。

    **[ブックマーク コントロールの追加]** ダイアログ ボックスが表示されます。

2. "creating a shortcut menu when you right-click the text" という語句を選択し、 **[OK]** をクリックします。

    `bookmark1` がドキュメントに追加されます。

3. 別の <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを、"right-click the text in a bookmark" という語句に追加します。

    `bookmark2` がドキュメントに追加されます。

   > [!NOTE]
   > "right-click the text" という語句が、`bookmark1` と `bookmark2` の両方に表示されます。

   デザイン時に文書にブックマークを追加すると、<xref:Microsoft.Office.Tools.Word.Bookmark> コントロールが作成されます。 ブックマークの複数のイベントに対してプログラミングを行うことができます。 ブックマークの <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick> イベントにコードを作成することで、ユーザーがブックマーク内のテキストを右クリックしたときにショートカット メニューを表示できます。

## <a name="add-commands-to-a-shortcut-menu"></a><a name="BKMK_AddCmndsShortMenu"></a> ショートカット メニューにコマンドを追加する
 ドキュメントを右クリックすると表示されるショートカット メニューにボタンを追加します。

### <a name="to-add-commands-to-a-shortcut-menu"></a>ショートカット メニューにコマンドを追加するには

1. **リボン XML** 項目をプロジェクトに追加します。 詳しくは、「[方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)」をご覧ください。

2. **ソリューション エクスプローラー** で、**ThisDocument.cs** または **ThisDocument.vb** を選択します。

3. メニュー バーで **[表示]**  >  **[コード]** の順に選択します。

     コード エディターで、**ThisDocument** クラス ファイルが開きます。

4. **ThisDocument** クラスに、次のコードを追加します。 このコードは、CreateRibbonExtensibilityObject メソッドをオーバーライドし、Office アプリケーションにリボン XML クラスを返します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet1":::

5. **[ソリューション エクスプローラー]** でリボン XML ファイルを選択します。 既定では、リボン XML ファイルには Ribbon1.xml という名前が付けられます。

6. メニュー バーで **[表示]**  >  **[コード]** の順に選択します。

     コード エディターでリボン XML ファイルが開きます。

7. コード エディターを使用して、リボン XML ファイルの内容を次のコードに置き換えます。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui" onLoad="Ribbon_Load">
      <contextMenus>
        <contextMenu idMso="ContextMenuText">
          <button id="BoldButton" label="Bold" onAction="ButtonClick"
               getVisible="GetVisible" />
          <button id="ItalicButton" label="Italic" onAction="ButtonClick"
              getVisible="GetVisible"/>
        </contextMenu>
      </contextMenus>
    </customUI>
    ```

     このコードでは、ドキュメントを右クリックすると表示されるショートカット メニューに 2 つのボタンが追加されます。

8. **ソリューション エクスプローラー** で `ThisDocument` を右クリックし、 **[コードの表示]** をクリックします。

9. 次の変数とブックマーク変数をクラス レベルで宣言します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet2":::

10. **ソリューション エクスプローラー** で、リボン コード ファイルを選択します。 既定では、リボン コード ファイルには **Ribbon1.cs** または **Ribbon1.vb** という名前が付けられます。

11. メニュー バーで **[表示]**  >  **[コード]** の順に選択します。

     コード エディターでリボン コード ファイルが開きます。

12. リボン コード ファイルで、次のメソッドを追加します。 これは、ドキュメントのショートカット メニューに追加した 2 つのボタンのコールバック メソッドです。 このメソッドでは、これらのボタンがショートカット メニューに表示されるかどうかが決定されます。 [太字] ボタンおよび [斜体] ボタンは、ブックマーク内のテキストを右クリックしたときにのみ表示されます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb" id="Snippet5":::

## <a name="format-the-text-in-the-bookmark"></a><a name="BKMK_formattextbkmk"></a> ブックマーク内のテキストを書式設定する

### <a name="to-format-the-text-in-the-bookmark"></a>ブックマーク内のテキストに書式を設定するには

1. リボン コード ファイルで、ブックマークに書式を適用するための `ButtonClick` イベント ハンドラーを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb" id="Snippet6":::

2. **ソリューション エクスプローラー** で、**ThisDocument.cs** または **ThisDocument.vb** を選択します。

3. メニュー バーで **[表示]**  >  **[コード]** の順に選択します。

     コード エディターで、**ThisDocument** クラス ファイルが開きます。

4. **ThisDocument** クラスに、次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet3":::

    > [!NOTE]
    > ブックマークが部分的に重なっている場合を処理するためのコードを作成する必要があります。 これを行わないと、既定でコードは選択範囲内にあるすべてのブックマークについて呼び出されます。

5. C# では、次に示すように、ブックマーク コントロールのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに追加する必要があります。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet4":::

## <a name="test-the-application"></a>アプリケーションをテストする
 ドキュメントをテストして、ブックマーク内のテキストを右クリックしたときにショートカット メニューに太字と斜体のメニュー項目が表示され、テキストが正しく書式設定されることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. 最初のブックマークを右クリックし、 **[太字]** をクリックします。

3. `bookmark1` 内のすべてのテキストが太字になることを確認します。

4. ブックマークが重なっている部分のテキストを右クリックし、 **[斜体]** をクリックします。

5. `bookmark2` ではすべてのテキストが斜体になるが、`bookmark1` では `bookmark2` と重なっている部分のテキストしか斜体にならないことを確認します。

## <a name="next-steps"></a>次のステップ
 ここでは、次の作業を行います。

- Excel 内のホスト コントロールのイベントに応答するコードを作成します。 詳しくは、「[チュートリアル: NamedRange コントロールのイベントに対するプログラミング](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)」をご覧ください。

- チェック ボックスを使用してブックマーク内の書式を変更します。 詳しくは、「[チュートリアル: CheckBox コントロールを使用してドキュメントの書式を変更する](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)」をご覧ください。

## <a name="see-also"></a>関連項目
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [Bookmark コントロール](../vsto/bookmark-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
