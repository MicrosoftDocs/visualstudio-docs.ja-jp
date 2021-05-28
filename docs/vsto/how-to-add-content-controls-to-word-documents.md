---
title: '方法: Word 文書にコンテンツ コントロールを追加する'
description: ドキュメント レベルの Word プロジェクトで、デザイン時または実行時に、プロジェクト内の文書にコンテンツ コントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- DropDownListContentControl, adding to documents
- BuildingBlockGalleryContentControl, adding to documents
- partial document protection [Office development in Visual Studio]
- RichTextContentControl, adding to documents
- Word [Office development in Visual Studio], partial document protection
- content controls [Office development in Visual Studio], protecting
- PictureContentControl, adding to documents
- GroupContentControl, adding to documents
- document protection [Office development in Visual Studio]
- PlainTextContentControl, adding to documents
- content controls [Office development in Visual Studio], adding
- ComboBoxContentControl, adding to documents
- DatePickerContentControl, adding to documents
- Word [Office development in Visual Studio], restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a902e85f8c53aa7a3d1ebe3b6480a7c68fa60601
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827904"
---
# <a name="how-to-add-content-controls-to-word-documents"></a>方法: Word 文書にコンテンツ コントロールを追加する
  ドキュメント レベルの Word プロジェクトでは、デザイン時または実行時にプロジェクトの文書にコンテンツ コントロールを追加できます。 Word VSTO アドイン プロジェクトでは、実行時に任意の開いている文書にコンテンツ コントロールを追加できます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 このトピックでは、次のタスクについて説明します。

- [デザイン時にコンテンツ コントロールを追加する](#designtime)

- [実行時に、ドキュメント レベルのプロジェクトにコンテンツ コントロールを追加する](#runtimedoclevel)

- [VSTO アドイン プロジェクトで、実行時にコンテンツ コントロールを追加する](#runtimeaddin)

  コンテンツ コントロールについて詳しくは、「[コンテンツ コントロール](../vsto/content-controls.md)」をご覧ください。

## <a name="add-content-controls-at-design-time"></a><a name="designtime"></a> デザイン時にコンテンツ コントロールを追加する
 デザイン時にドキュメント レベルのプロジェクトの文書にコンテンツ コントロールを追加する方法はいくつかあります。

- **[ツールボックス]** の **[Word コントロール]** タブからコンテンツ コントロールを追加する。

- Word でネイティブなコンテンツ コントロールを追加するのと同様に、ドキュメントにコンテンツ コントロールを追加します。

- **[データ ソース]** ウィンドウからコンテンツ コントロールを文書にドラッグする。 これは、コントロールの作成時にデータにコントロールをバインドする場合に役立ちます。 詳しくは、「[方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)」および「[方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)」をご覧ください。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-content-control-to-a-document-by-using-the-toolbox"></a>[ツールボックス] を使用して文書にコンテンツ コントロールを追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、コンテンツ コントロールを追加する場所にカーソルを置くか、または、テキストを置換するコンテンツ コントロールを選択します。

2. **[ツールボックス]** を開き、 **[Word コントロール]** タブをクリックします。

3. 次のいずれかの方法でコントロールを追加します。

    - **[ツールボックス]** のコンテンツ コントロールをダブルクリックします。

         or

    - **ツールボックス** 内のコンテンツ コントロールをクリックし、**Enter** キーを押します。

         or

    - **[ツールボックス]** からコンテンツ コントロールを文書にドラッグします。 コンテンツ コントロールが、マウス ポインターの場所ではなく、ドキュメント内の現在の選択の場所で追加されます。

> [!NOTE]
> <xref:Microsoft.Office.Tools.Word.GroupContentControl> [ツールボックス] **を使用して** を追加することはできません。 <xref:Microsoft.Office.Tools.Word.GroupContentControl> は Word で、または実行時にのみ追加できます。

> [!NOTE]
> Visual Studio では、チェック ボックス コンテンツ コントロールがツールボックスで提供されていません。 文書にチェック ボックス コンテンツ コントロールを追加するには、プログラムを使用して <xref:Microsoft.Office.Tools.Word.ContentControl> オブジェクトを作成する必要があります。 詳細については、「[コンテンツ コントロール](../vsto/content-controls.md)」を参照してください。

#### <a name="to-add-a-content-control-to-a-document-in-word"></a>Word で文書にコンテンツ コントロールを追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、コンテンツ コントロールを追加する場所にカーソルを置くか、または、テキストを置換するコンテンツ コントロールを選択します。

2. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳しくは、「[方法: [開発] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」をご覧ください。

3. **[コントロール]** グループで、追加するコンテンツ コントロールのアイコンをクリックします。

## <a name="add-content-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 実行時に、ドキュメント レベルのプロジェクトにコンテンツ コントロールを追加する
 プロジェクトで <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> クラスの `ThisDocument` プロパティのメソッドを使用して、実行時にプログラムによりドキュメントにコンテンツ コントロールを追加できます。 各メソッドには 3 つのオーバーロードがあります。それらを使用することにより、次のようにコンテンツ コントロールを追加できます。

- 現在の選択項目でコントロールを追加します。

- 指定された範囲にコントロールを追加します。

- 文書内のネイティブなコンテンツ コントロールに基づいたコントロールを追加します。

  動的に作成されたコンテンツ コントロールは、文書を閉じる際に文書に残りません。 ただし、ネイティブなコンテンツ コントロールは、文書内に残ります。 文書を次回開くときに、ネイティブのコンテンツ コントロールに基づくコンテンツ コントロールを再作成できます。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

> [!NOTE]
> Word 2010 プロジェクトで文書にチェック ボックス コンテンツ コントロールを追加するには、 <xref:Microsoft.Office.Tools.Word.ContentControl> オブジェクトを作成する必要があります。 詳細については、「[コンテンツ コントロール](../vsto/content-controls.md)」を参照してください。

### <a name="to-add-a-content-control-at-the-current-selection"></a>現在の選択項目でコンテンツ コントロールを追加するには

1. 名前が `Add`\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> などの追加するコンテンツ コントロールのクラス名) で、パラメーターが 1 個 (新しいコントロールの名前) の <xref:Microsoft.Office.Tools.Word.ControlCollection> メソッドを使用します。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `AddRichTextControlAtSelection` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs" id="Snippet700":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb" id="Snippet700":::

### <a name="to-add-a-content-control-at-a-specified-range"></a>指定された範囲にコンテンツ コントロールを追加するには

1. 名前が `Add`\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> などの追加するコンテンツ コントロールのクラス名) で、<xref:Microsoft.Office.Interop.Word.Range> をパラメーターとする <xref:Microsoft.Office.Tools.Word.ControlCollection> メソッドを使用します。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `AddRichTextControlAtRange` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs" id="Snippet701":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb" id="Snippet701":::

### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>ネイティブなコンテンツ コントロールに基づいたコンテンツ コントロールを追加するには

1. 名前が `Add`\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> などの追加するコンテンツ コントロールのクラス名) で、`Microsoft.Office.Interop.Word.ContentControl` をパラメーターとする <xref:Microsoft.Office.Tools.Word.ControlCollection> メソッドを使用します。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して、ドキュメント内にあるすべてのネイティブなリッチ テキスト コントロールについて新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を作成しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `CreateRichTextControlsFromNativeControls` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs" id="Snippet702":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb" id="Snippet702":::

## <a name="add-content-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a> VSTO アドイン プロジェクトで、実行時にコンテンツ コントロールを追加する
 コンテンツ フォーム コントロールは、実行時に VSTO アドインを使用して任意の開いているドキュメントに追加できます。 そのためには、開いている文書に基づいた <xref:Microsoft.Office.Tools.Word.Document> ホスト項目を生成し、このホスト項目の <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> プロパティのメソッドを使用します。 各メソッドには 3 つのオーバーロードがあります。それらを使用することにより、次のようにコンテンツ コントロールを追加できます。

- 現在の選択項目でコントロールを追加します。

- 指定された範囲にコントロールを追加します。

- 文書内のネイティブなコンテンツ コントロールに基づいたコントロールを追加します。

  動的に作成されたコンテンツ コントロールは、文書を閉じる際に文書に残りません。 ただし、ネイティブなコンテンツ コントロールは、文書内に残ります。 文書を次回開くときに、ネイティブのコンテンツ コントロールに基づくコンテンツ コントロールを再作成できます。 詳しくは、「[Office ドキュメントでのダイナミック コントロールの永続化](../vsto/persisting-dynamic-controls-in-office-documents.md)」をご覧ください。

  VSTO アドイン プロジェクトでのホスト項目の生成について詳しくは、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」をご覧ください。

> [!NOTE]
> 文書にチェック ボックス コンテンツ コントロールを追加するには、 <xref:Microsoft.Office.Tools.Word.ContentControl> オブジェクトを作成する必要があります。 詳細については、「[コンテンツ コントロール](../vsto/content-controls.md)」を参照してください。

### <a name="to-add-a-content-control-at-the-current-selection"></a>現在の選択項目でコンテンツ コントロールを追加するには

1. 名前が `Add`\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> などの追加するコンテンツ コントロールのクラス名) で、パラメーターが 1 個 (新しいコントロールの名前) の <xref:Microsoft.Office.Tools.Word.ControlCollection> メソッドを使用します。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用してアクティブな文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `AddRichTextControlAtSelection` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet1":::

### <a name="to-add-a-content-control-at-a-specified-range"></a>指定された範囲にコンテンツ コントロールを追加するには

1. 名前が `Add`\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> などの追加するコンテンツ コントロールのクラス名) で、<xref:Microsoft.Office.Interop.Word.Range> をパラメーターとする <xref:Microsoft.Office.Tools.Word.ControlCollection> メソッドを使用します。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用してアクティブな文書の先頭に新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `AddRichTextControlAtRange` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet2":::

#### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>ネイティブなコンテンツ コントロールに基づいたコンテンツ コントロールを追加するには

1. 名前が `Add`\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> などの追加するコンテンツ コントロールのクラス名) で、`Microsoft.Office.Interop.Word.ContentControl` をパラメーターとする <xref:Microsoft.Office.Tools.Word.ControlCollection> メソッドを使用します。

     次のコード例では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> メソッドを使用して、文書を開いた後に文書内にあるすべてのネイティブなリッチ テキスト コントロールについて、新しい <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を作成しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet3":::

     C# の場合、 `Application_DocumentOpen` イベント ハンドラーを <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> イベントに接続する必要もあります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet6":::

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
- [プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
