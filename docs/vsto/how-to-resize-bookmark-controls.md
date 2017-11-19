---
title: "方法: Bookmark コントロールのサイズを変更する |Microsoft ドキュメント"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- Bookmark control, resizing
ms.assetid: 3de1c774-921a-4113-a54a-e3b8d4a65d53
caps.latest.revision: "45"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b461aec44b30f8934a6a2388d6fd4f4bc7d65210
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="how-to-resize-bookmark-controls"></a>方法 : Bookmark コントロールのサイズを変更する
  <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールのサイズは、Microsoft Office Word ドキュメントに追加するときに設定します。 サイズは後から変更することもできます。  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 ブックマークのサイズは、次の 3 通りの方法で変更できます。  
  
-   <xref:Microsoft.Office.Tools.Word.Bookmark> コントロール内でテキストを追加または削除する。  
  
     ブックマークのテキストを追加するたびに、ブックマークのサイズは自動的に、新しいテキスト分だけ大きくなります。 テキストを削除すると、ブックマークのサイズは自動的に小さくなります。  
  
-   <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> コントロールの <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> および <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを変更する。  
  
     これは、数文字分だけサイズを変更する場合に役立ちます。  
  
-   <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを作成し直す。  
  
     これは、ブックマークのサイズや場所に大幅な変更がある場合に便利です。  
  
 ドキュメント レベルのプロジェクトでは、デザイン時または実行時にプロジェクトの文書に <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを追加できます。 VSTO アドイン プロジェクトでは、実行時に、開いている任意の文書に <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを追加できます。 詳細については、「 [How to: Add Bookmark Controls to Word Documents](../vsto/how-to-add-bookmark-controls-to-word-documents.md)」を参照してください。  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="changing-the-start-and-end-properties"></a>Start および End プロパティの変更  
  
#### <a name="to-resize-a-bookmark-in-a-document-level-project-at-design-time"></a>デザイン時にドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには  
  
1.  **[プロパティ]** ウィンドウでブックマークを選択します。  
  
2.  <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> プロパティの値を増減させます。  
  
3.  <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> プロパティの値を増減させます。  
  
#### <a name="to-resize-a-bookmark-in-a-document-level-project-at-run-time"></a>実行時にドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには  
  
1.  実行時またはデザイン時に作成した <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> の <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> および <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを変更します。  
  
     次のコード例では、 `SampleBookmark`という名前のブックマークの先頭に 5 文字を追加します。 このコードでは、ブックマークの前に 5 文字以上のテキストがあることを前提としています。  
  
     [!code-csharp[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#2)]
     [!code-vb[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#2)]  
  
     次のコード例では、同じブックマークの末尾に 5 文字を追加します。 このコードでは、ブックマークの後に 5 文字以上のテキストがあることを前提としています。  
  
     [!code-csharp[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#3)]
     [!code-vb[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#3)]  
  
#### <a name="to-resize-a-bookmark-in-an-vsto-add-in-project-at-run-time"></a>実行時に VSTO アドイン プロジェクト内のブックマークのサイズを変更するには  
  
1.  実行時またはデザイン時に作成した <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> の <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> および <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを変更します。  
  
     次のコード例では、アクティブなドキュメントの最初の段落のテキストを含む <xref:Microsoft.Office.Tools.Word.Bookmark> を作成した後、 <xref:Microsoft.Office.Tools.Word.Bookmark>の先頭と末尾から 5 文字を削除します。  
  
     [!code-vb[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#16)]
     [!code-csharp[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#16)]  
  
## <a name="recreating-the-bookmark"></a>ブックマークの再作成  
 ドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには、既存のブックマークと同じ名前の新しいブックマークを別のサイズで作成します。  
  
#### <a name="to-recreate-a-bookmark-in-a-document-level-project-at-design-time"></a>デザイン時にドキュメント レベルのプロジェクト内のブックマークを再作成するには  
  
1.  新しい <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールに含めるテキストを選択します。  
  
2.  **[挿入]** メニューで **[ブックマーク]**をクリックします。  
  
3.  **[ブックマーク]** ダイアログ ボックスで、サイズを変更するブックマークの名前を選択し、 **[追加]**をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [How to: Add Bookmark Controls to Word Documents](../vsto/how-to-add-bookmark-controls-to-word-documents.md)   
 [拡張オブジェクトによる Word の自動化](../vsto/automating-word-by-using-extended-objects.md)   
 [Host Items and Host Controls Overview](../vsto/host-items-and-host-controls-overview.md)   
 [方法: NamedRange コントロールのサイズを変更します。](../vsto/how-to-resize-namedrange-controls.md)   
 [方法: ListObject コントロールのサイズを変更します。](../vsto/how-to-resize-listobject-controls.md)   
 [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  