---
title: '方法: コンテンツ コントロールを使用して文書の一部を保護する'
description: Visual Studio を使用して、コンテンツ コントロールを使用して Microsoft Word 文書の一部を保護する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- partial document protection [Office development in Visual Studio]
- content controls [Office development in Visual Studio], protecting documents
- Word [Office development in Visual Studio], partial document protection
- document protection [Office development in Visual Studio]
- Word [Office development in Visual Studio], restricted permissions
- GroupContentControl
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cc333871d4f371530db84a0c4f07ab891db2a937
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825473"
---
# <a name="how-to-protect-parts-of-documents-by-using-content-controls"></a>方法: コンテンツ コントロールを使用して文書の一部を保護する
  ドキュメントの一部を保護することにより、ユーザーがドキュメントのその部分を変更したり削除したりできないようにします。 コンテンツ コントロールを使用して Microsoft Office Word ドキュメントの一部を保護する方法は、いくつかあります。

- コンテンツ コントロールを保護することができます。

- コンテンツ コントロールに含まれていないドキュメントの一部を保護することができます。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="protect-a-content-control"></a><a name="EditDeleteControl"></a> コンテンツ コントロールを保護する
 デザイン時または実行時に文書レベルのプロジェクト内のコントロールのプロパティを設定することにより、ユーザーがコンテンツ コントロールを編集したり削除したりしないようにすることができます。

 VSTO アドイン プロジェクトを使用して、実行時にドキュメントに追加したコンテンツ コントロールを保護することもできます。 詳細については、「[方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)」を参照してください。

### <a name="to-protect-a-content-control-at-design-time"></a>デザイン時に、コンテンツ コントロールを保護するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、保護するコンテンツ コントロールを選択します。

2. **[プロパティ]** ウィンドウで、次のプロパティのいずれか、または両方を設定します。

    - ユーザーがコントロールを編集できないようにするには、**LockContents** を **True** に設定します。

    - ユーザーがコントロールを削除できないようにするには、**LockContentControl** を **True** に設定します。

3. **[OK]** をクリックします。

### <a name="to-protect-a-content-control-at-run-time"></a>実行時に、コンテンツ コントロールを保護するには

1. ユーザーがコントロールを編集できないようにするには、コンテンツ コントロールの `LockContents` プロパティを **true** に設定し、ユーザーがコントロールを削除できないようにするには、`LockContentControl` プロパティを **true** に設定します。

     次のコード例は、ドキュメント レベル プロジェクト内の 2 つの異なる <xref:Microsoft.Office.Tools.Word.RichTextContentControl> オブジェクトのプロパティ、<xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> と <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> の使用法を示しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `AddProtectedContentControls` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb" id="Snippet2":::

     次のコード例は、VSTO アドイン プロジェクト内の 2 つの異なる <xref:Microsoft.Office.Tools.Word.RichTextContentControl> オブジェクトのプロパティ、<xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> と <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> の使用法を示しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `AddProtectedContentControls` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet14":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet14":::

## <a name="protect-a-part-of-a-document-that-is-not-in-a-content-control"></a>コンテンツ コントロールに含まれていないドキュメントの一部を保護する
 ドキュメントのある領域を <xref:Microsoft.Office.Tools.Word.GroupContentControl> に配置することにより、ユーザーがその領域を変更できないようにすることができます。 これは、次のシナリオで役立ちます。

- コンテンツ コントロールが含まれていない領域を保護する場合。

- 既にコンテンツ コントロールが含まれている領域だが、保護対象のテキストまたはその他のアイテムが、コンテンツ コントロールに含まれていない場合。

> [!NOTE]
> 埋め込みコンテンツ コントロールを含む <xref:Microsoft.Office.Tools.Word.GroupContentControl> を作成する場合、埋め込みコンテンツ コントロールは自動的には保護されません。 ユーザーが埋め込みコンテンツ コントロールを編集できないようにするには、コントロールの **LockContents** プロパティを使用します。

### <a name="to-protect-an-area-of-a-document-at-design-time"></a>デザイン時にドキュメントのある領域を保護するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、保護する領域を選択します。

2. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

3. **[コントロール]** グループで **[グループ]** ドロップダウン ボタンをクリックし、 **[グループ]** をクリックします。

     保護された領域を含む <xref:Microsoft.Office.Tools.Word.GroupContentControl> が、プロジェクト内の `ThisDocument` クラスに自動的に生成されます。 グループ コントロールを表す枠線は、デザイン時に表示されますが、実行時に表示される枠線はありません。

### <a name="to-protect-an-area-of-a-document-at-run-time"></a>実行時にドキュメントの領域を保護するには

1. プログラムを使用して、保護する領域を選択し、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddGroupContentControl%2A> メソッドを呼び出すことにより <xref:Microsoft.Office.Tools.Word.GroupContentControl> を作成します。

     ドキュメント レベル プロジェクトの次のコード例は、ドキュメント内の最初の段落にテキストを追加し、最初の段落を選択して <xref:Microsoft.Office.Tools.Word.GroupContentControl> をインスタンス化します。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `ProtectFirstParagraph` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb" id="Snippet1":::

     VSTO アドイン プロジェクトの次のコード例は、アクティブなドキュメント内の最初の段落にテキストを追加し、最初の段落を選択して <xref:Microsoft.Office.Tools.Word.GroupContentControl> をインスタンス化します。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `ProtectFirstParagraph` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet15":::

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [コンテンツ コントロール](../vsto/content-controls.md)
- [方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
