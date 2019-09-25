---
title: '方法: コンテンツコントロールを使用してドキュメントの一部を保護する'
ms.date: 02/02/2017
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 129962209d8cfa541a34bc1575a73382cd63d7c4
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254665"
---
# <a name="how-to-protect-parts-of-documents-by-using-content-controls"></a>方法: コンテンツコントロールを使用してドキュメントの一部を保護する
  ドキュメントの一部を保護することにより、ユーザーがドキュメントのその部分を変更したり削除したりできないようにします。 コンテンツ コントロールを使用して Microsoft Office Word ドキュメントの一部を保護する方法は、いくつかあります。

- コンテンツ コントロールを保護することができます。

- コンテンツ コントロールに含まれていないドキュメントの一部を保護することができます。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="EditDeleteControl"></a>コンテンツコントロールを保護する
 デザイン時または実行時に文書レベルのプロジェクト内のコントロールのプロパティを設定することにより、ユーザーがコンテンツ コントロールを編集したり削除したりしないようにすることができます。

 VSTO アドイン プロジェクトを使用して、実行時にドキュメントに追加したコンテンツ コントロールを保護することもできます。 詳細については、「[方法 :Word 文書](../vsto/how-to-add-content-controls-to-word-documents.md)にコンテンツコントロールを追加します。

### <a name="to-protect-a-content-control-at-design-time"></a>デザイン時に、コンテンツ コントロールを保護するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、保護するコンテンツ コントロールを選択します。

2. **[プロパティ]** ウィンドウで、次のプロパティのいずれかまたは両方を設定します。

    - ユーザーがコントロールを編集できないようにするには、 **Lockcontents**を**True**に設定します。

    - ユーザーがコントロールを削除できないようにするには、 **Lockcontentcontrol**を**True**に設定します。

3. **[OK]** をクリックします。

### <a name="to-protect-a-content-control-at-run-time"></a>実行時に、コンテンツ コントロールを保護するには

1. ユーザーがコントロールを編集できないようにするには、コンテンツコントロールの`LockContentControl` プロパティをtrueに設定し、プロパティをtrueに設定して、ユーザーがコントロールを削除できないよう`LockContents`にします。

     次のコード例は、ドキュメント レベル プロジェクト内の 2 つの異なる <xref:Microsoft.Office.Tools.Word.RichTextContentControl> オブジェクトのプロパティ、<xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> と <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> の使用法を示しています。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `AddProtectedContentControls` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     [!code-csharp[Trin_ContentControlHowToProtect#2](../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlHowToProtect#2](../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb#2)]

     次のコード例は、VSTO アドイン プロジェクト内の 2 つの異なる <xref:Microsoft.Office.Tools.Word.RichTextContentControl> オブジェクトのプロパティ、<xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> と <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> の使用法を示しています。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `AddProtectedContentControls` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     [!code-vb[Trin_WordAddInDynamicControls#14](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#14)]
     [!code-csharp[Trin_WordAddInDynamicControls#14](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#14)]

## <a name="protect-a-part-of-a-document-that-is-not-in-a-content-control"></a>コンテンツコントロールに含まれていないドキュメントの一部を保護する
 ドキュメントのある領域を <xref:Microsoft.Office.Tools.Word.GroupContentControl> に配置することにより、ユーザーがその領域を変更できないようにすることができます。 これは、次のシナリオで役立ちます。

- コンテンツ コントロールが含まれていない領域を保護する場合。

- 既にコンテンツ コントロールが含まれている領域だが、保護対象のテキストまたはその他のアイテムが、コンテンツ コントロールに含まれていない場合。

> [!NOTE]
> 埋め込みコンテンツ コントロールを含む <xref:Microsoft.Office.Tools.Word.GroupContentControl> を作成する場合、埋め込みコンテンツ コントロールは自動的には保護されません。 ユーザーが埋め込みコンテンツコントロールを編集できないようにするには、コントロールの**Lockcontents**プロパティを使用します。

### <a name="to-protect-an-area-of-a-document-at-design-time"></a>デザイン時にドキュメントのある領域を保護するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされているドキュメントで、保護する領域を選択します。

2. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法 :リボン](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)に [開発者] タブを表示します。

3. **[コントロール]** グループの **[グループ]** ドロップダウンボタンをクリックし、 **[グループ]** をクリックします。

     保護された領域を含む <xref:Microsoft.Office.Tools.Word.GroupContentControl> が、プロジェクト内の `ThisDocument` クラスに自動的に生成されます。 グループ コントロールを表す枠線は、デザイン時に表示されますが、実行時に表示される枠線はありません。

### <a name="to-protect-an-area-of-a-document-at-run-time"></a>実行時にドキュメントの領域を保護するには

1. プログラムを使用して、保護する領域を選択し、<xref:Microsoft.Office.Tools.Word.ControlCollection.AddGroupContentControl%2A> メソッドを呼び出すことにより <xref:Microsoft.Office.Tools.Word.GroupContentControl> を作成します。

     ドキュメント レベル プロジェクトの次のコード例は、ドキュメント内の最初の段落にテキストを追加し、最初の段落を選択して <xref:Microsoft.Office.Tools.Word.GroupContentControl> をインスタンス化します。 このコードを実行するには、プロジェクトの `ThisDocument` クラスにコードを追加し、 `ProtectFirstParagraph` イベント ハンドラーから `ThisDocument_Startup` メソッドを呼び出します。

     [!code-csharp[Trin_ContentControlHowToProtect#1](../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlHowToProtect#1](../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb#1)]

     VSTO アドイン プロジェクトの次のコード例は、アクティブなドキュメント内の最初の段落にテキストを追加し、最初の段落を選択して <xref:Microsoft.Office.Tools.Word.GroupContentControl> をインスタンス化します。 このコードを実行するには、プロジェクトの `ThisAddIn` クラスにコードを追加し、 `ProtectFirstParagraph` イベント ハンドラーから `ThisAddIn_Startup` メソッドを呼び出します。

     [!code-vb[Trin_WordAddInDynamicControls#15](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#15)]
     [!code-csharp[Trin_WordAddInDynamicControls#15](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#15)]

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用した Word の自動化](../vsto/automating-word-by-using-extended-objects.md)
- [コンテンツコントロール](../vsto/content-controls.md)
- [方法: Word 文書にコンテンツコントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
