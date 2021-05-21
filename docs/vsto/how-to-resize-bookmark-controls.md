---
title: '方法: Bookmark コントロールのサイズを変更する'
description: Microsoft Word 文書に Bookmark コントロールを追加するとき、Visual Studio を使用し、Bookmark コントロールのサイズを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- Bookmark control, resizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b2b2bd963b2f0b4eb574630382930eb0805909be
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825785"
---
# <a name="how-to-resize-bookmark-controls"></a>方法: Bookmark コントロールのサイズを変更する
  <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールのサイズは、Microsoft Office Word ドキュメントに追加するときに設定します。 サイズは後から変更することもできます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 ブックマークのサイズは、次の 3 通りの方法で変更できます。

- <xref:Microsoft.Office.Tools.Word.Bookmark> コントロール内でテキストを追加または削除する。

   ブックマークのテキストを追加するたびに、ブックマークのサイズは自動的に、新しいテキスト分だけ大きくなります。 テキストを削除すると、ブックマークのサイズは自動的に小さくなります。

- <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> コントロールの <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> および <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを変更する。

   これは、数文字分だけサイズを変更する場合に役立ちます。

- <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを作成し直す。

   これは、ブックマークのサイズや場所に大幅な変更がある場合に便利です。

  ドキュメント レベルのプロジェクトでは、デザイン時または実行時にプロジェクトの文書に <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを追加できます。 VSTO アドイン プロジェクトでは、実行時に、開いている任意の文書に <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを追加できます。 詳細については、「[方法: Word 文書に Bookmark コントロールを追加する](../vsto/how-to-add-bookmark-controls-to-word-documents.md)」を参照してください。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="change-the-start-and-end-properties"></a>Start および End プロパティを変更する

### <a name="to-resize-a-bookmark-in-a-document-level-project-at-design-time"></a>デザイン時にドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには

1. **[プロパティ]** ウィンドウでブックマークを選択します。

2. <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> プロパティの値を増減させます。

3. <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> プロパティの値を増減させます。

### <a name="to-resize-a-bookmark-in-a-document-level-project-at-run-time"></a>実行時にドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには

1. 実行時またはデザイン時に作成した <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> の <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> および <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを変更します。

     次のコード例では、 `SampleBookmark`という名前のブックマークの先頭に 5 文字を追加します。 このコードでは、ブックマークの前に 5 文字以上のテキストがあることを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb" id="Snippet2":::

     次のコード例では、同じブックマークの末尾に 5 文字を追加します。 このコードでは、ブックマークの後に 5 文字以上のテキストがあることを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb" id="Snippet3":::

### <a name="to-resize-a-bookmark-in-a-vsto-add-in-project-at-run-time"></a>実行時に VSTO アドイン プロジェクト内のブックマークのサイズを変更するには

1. 実行時またはデザイン時に作成した <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> の <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> および <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを変更します。

     次のコード例では、アクティブなドキュメントの最初の段落のテキストを含む <xref:Microsoft.Office.Tools.Word.Bookmark> を作成した後、 <xref:Microsoft.Office.Tools.Word.Bookmark>の先頭と末尾から 5 文字を削除します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet16":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet16":::

## <a name="recreate-the-bookmark"></a>ブックマークを再作成する
 ドキュメント レベルのプロジェクト内のブックマークのサイズを変更するには、既存のブックマークと同じ名前の新しいブックマークを別のサイズで作成します。

### <a name="to-recreate-a-bookmark-in-a-document-level-project-at-design-time"></a>デザイン時にドキュメント レベルのプロジェクト内のブックマークを再作成するには

1. 新しい <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールに含めるテキストを選択します。

2. **[挿入]** メニューで **[ブックマーク]** をクリックします。

3. **[ブックマーク]** ダイアログ ボックスで、サイズを変更するブックマークの名前を選択し、 **[追加]** をクリックします。

## <a name="see-also"></a>関連項目
- [方法: Word 文書に Bookmark コントロールを追加する](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [方法: NamedRange コントロールのサイズを変更する](../vsto/how-to-resize-namedrange-controls.md)
- [方法: ListObject コントロールのサイズを変更する](../vsto/how-to-resize-listobject-controls.md)
- [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
