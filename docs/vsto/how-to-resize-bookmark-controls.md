---
title: '方法: Bookmark コントロールのサイズを変更します。'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- Bookmark control, resizing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 57b6d6a089570c52607cf73eeed4fc00978ab251
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924838"
---
# <a name="how-to-resize-bookmark-controls"></a>方法: Bookmark コントロールのサイズを変更します。
  <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールのサイズは、Microsoft Office Word ドキュメントに追加するときに設定します。 サイズは後から変更することもできます。  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 ブックマークのサイズは、次の 3 通りの方法で変更できます。  
  
- <xref:Microsoft.Office.Tools.Word.Bookmark> コントロール内でテキストを追加または削除する。  
  
   ブックマークのテキストを追加するたびに、ブックマークのサイズは自動的に、新しいテキスト分だけ大きくなります。 テキストを削除すると、ブックマークのサイズは自動的に小さくなります。  
  
- <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> コントロールの <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> および <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを変更する。  
  
   これは、数文字分だけサイズを変更する場合に役立ちます。  
  
- <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを作成し直す。  
  
   これは、ブックマークのサイズや場所に大幅な変更がある場合に便利です。  
  
  ドキュメント レベルのプロジェクトでは、デザイン時または実行時にプロジェクトの文書に <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを追加できます。 VSTO アドイン プロジェクトに追加することができます<xref:Microsoft.Office.Tools.Word.Bookmark>実行時に開いているドキュメントのコントロール。 詳細については、次を参照してください。[方法: Word 文書にコントロールをブックマークの追加](../vsto/how-to-add-bookmark-controls-to-word-documents.md)します。  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="change-the-start-and-end-properties"></a>Start および end プロパティを変更します。  
  
### <a name="to-resize-a-bookmark-in-a-document-level-project-at-design-time"></a>デザイン時にドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには  
  
1.  **[プロパティ]** ウィンドウでブックマークを選択します。  
  
2.  <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> プロパティの値を増減させます。  
  
3.  <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> プロパティの値を増減させます。  
  
### <a name="to-resize-a-bookmark-in-a-document-level-project-at-runtime"></a>実行時にドキュメント レベル プロジェクト内のブックマークのサイズを変更するには  
  
1.  変更、<xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A>と<xref:Microsoft.Office.Tools.Word.Bookmark.End%2A>のプロパティを<xref:Microsoft.Office.Tools.Word.Bookmark>時またはデザイン時に作成しました。  
  
     次のコード例では、 `SampleBookmark`という名前のブックマークの先頭に 5 文字を追加します。 このコードでは、ブックマークの前に 5 文字以上のテキストがあることを前提としています。  
  
     [!code-csharp[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#2)]
     [!code-vb[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#2)]  
  
     次のコード例では、同じブックマークの末尾に 5 文字を追加します。 このコードでは、ブックマークの後に 5 文字以上のテキストがあることを前提としています。  
  
     [!code-csharp[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#3)]
     [!code-vb[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#3)]  
  
### <a name="to-resize-a-bookmark-in-a-vsto-add-in-project-at-runtime"></a>実行時に VSTO アドイン プロジェクト内のブックマークのサイズを変更するには  
  
1.  変更、<xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A>と<xref:Microsoft.Office.Tools.Word.Bookmark.End%2A>のプロパティを<xref:Microsoft.Office.Tools.Word.Bookmark>実行時に作成しました。  
  
     次のコード例では、アクティブなドキュメントの最初の段落のテキストを含む <xref:Microsoft.Office.Tools.Word.Bookmark> を作成した後、 <xref:Microsoft.Office.Tools.Word.Bookmark>の先頭と末尾から 5 文字を削除します。  
  
     [!code-vb[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#16)]
     [!code-csharp[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#16)]  
  
## <a name="recreate-the-bookmark"></a>ブックマークを再作成します。  
 ドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには、既存のブックマークと同じ名前の新しいブックマークを別のサイズで作成します。  
  
### <a name="to-recreate-a-bookmark-in-a-document-level-project-at-design-time"></a>デザイン時にドキュメント レベルのプロジェクト内のブックマークを再作成するには  
  
1.  新しい <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールに含めるテキストを選択します。  
  
2.  **[挿入]** メニューで **[ブックマーク]** をクリックします。  
  
3.  **[ブックマーク]** ダイアログ ボックスで、サイズを変更するブックマークの名前を選択し、 **[追加]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [方法: Word 文書に Bookmark コントロールを追加](../vsto/how-to-add-bookmark-controls-to-word-documents.md)   
 [拡張オブジェクトを使用して Word を自動化します。](../vsto/automating-word-by-using-extended-objects.md)   
 [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)   
 [方法: NamedRange コントロールをサイズ変更](../vsto/how-to-resize-namedrange-controls.md)   
 [方法: ListObject コントロールをサイズ変更](../vsto/how-to-resize-listobject-controls.md)   
 [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  