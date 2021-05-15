---
title: '方法: プログラムによって Word 文書にテキストを挿入する'
description: Visual Studio を使用して、Microsoft Word 文書にテキストをプログラムによって挿入する方法について学習します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, inserting text in documents
- text [Office development in Visual Studio], inserting in documents
- ranges, replacing text in documents
- documents [Office development in Visual Studio], inserting text
- text [Office development in Visual Studio], replacing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f17828b4617f84cb104761918787b4bbb79f7afc
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827358"
---
# <a name="how-to-programmatically-insert-text-into-word-documents"></a>方法: プログラムによって Word 文書にテキストを挿入する
  Microsoft Office Word の文書にテキストを挿入するには、主に次の 3 つの方法があります。

- 範囲内にテキストを挿入する。

- 範囲内のテキストを新しいテキストに置換する。

- <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Selection> メソッドを使用して、カーソルの位置または選択範囲にテキストを挿入する。

> [!NOTE]
> テキストをコンテンツ コントロールやブックマークに挿入することもできます。 詳細については、「[コンテンツ コントロール](../vsto/content-controls.md)」および「[Bookmark コントロール](../vsto/bookmark-control.md)」をご覧ください。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="insert-text-in-a-range"></a>範囲内にテキストを挿入する
 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range> プロパティを使用して、文書にテキストを挿入します。

### <a name="to-insert-text-in-a-range"></a>範囲内にテキストを挿入するには

1. 文書の先頭に範囲を指定し、 **New Text** というテキストを挿入します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet51":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet51":::

     次のコード例は VSTO アドインで使用できます。 このコードでは作業中のドキュメントを使用します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet51":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet51":::

2. 1 文字から挿入したテキストの長さまで拡張された <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを選択します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet52":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet52":::

## <a name="replace-text-in-a-range"></a>範囲内のテキストを置換する
 指定した範囲にテキストが含まれている場合は、範囲内のすべてのテキストが挿入したテキストで置換されます。

### <a name="to-replace-text-in-a-range"></a>範囲内のテキストを置換するには

1. 文書の先頭の 12 文字から成る <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを作成します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet53":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet53":::

     次のコード例は VSTO アドインで使用できます。 このコードでは作業中のドキュメントを使用します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet53":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet53":::

2. これらの文字を **New Text** という文字列で置換します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet54":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet54":::

3. 範囲を選択します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet55":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet55":::

## <a name="insert-text-using-typetext"></a>TypeText を使用してテキストを挿入する
 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> メソッドは、選択範囲にテキストを挿入します。 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> の動作は、ユーザーのコンピューターで設定されているオプションによって異なります。 次のプロシージャのコードは、 <xref:Microsoft.Office.Interop.Word.Selection> オブジェクト変数を宣言し、 **Overtype** オプションがオンになっている場合はオフにします。 **Overtype** オプションが有効になっていると、カーソル位置の隣にあるテキストが上書きされます。

### <a name="to-insert-text-using-the-typetext-method"></a>TypeText メソッドを使用してテキストを挿入するには

1. まず、<xref:Microsoft.Office.Interop.Word.Selection> オブジェクト変数を宣言します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet57":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet57":::

2. **Overtype** オプションがオンの場合はオフにします。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet58":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet58":::

3. 現在の選択範囲が挿入ポイントであるかどうかを確認します。

    選択範囲が挿入位置である場合は、 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A>を使用して文を挿入し、 <xref:Microsoft.Office.Interop.Word.Selection.TypeParagraph%2A> メソッドを使用して段落記号を挿入します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet59":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet59":::

4. **ElseIf** ブロック内のコードで、選択範囲が通常の選択範囲であるかどうかを確認します。 通常の選択範囲である場合は、次の **If** ブロックで、 **ReplaceSelection** オプションがオンになっているかどうかを確認します。 オンである場合は、選択範囲の <xref:Microsoft.Office.Interop.Word.Selection.Collapse%2A> メソッドを使用して、選択範囲を選択されているテキスト ブロックの先頭の挿入ポイントに折りたたみます。 テキストと段落記号を挿入します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet60":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet60":::

5. 選択範囲が挿入ポイントでも選択テキストのブロックではない場合、 **Else** ブロックのコードは何も実行しません。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet61":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet61":::

   <xref:Microsoft.Office.Interop.Word.Selection> オブジェクトの <xref:Microsoft.Office.Interop.Word.Selection.TypeBackspace%2A> メソッドを使用することもできます。このメソッドは、キーボードの **Backspace** キーと同じ動作をします。 ただし、テキストの挿入および操作については、<xref:Microsoft.Office.Interop.Word.Range> オブジェクトの方がより細かく制御できます。

   完全なコード例を次に示します。 この例を使用するには、プロジェクトの `ThisDocument` クラスか `ThisAddIn` クラスからコードを実行します。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet56":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet56":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内のテキストに書式を設定する](../vsto/how-to-programmatically-format-text-in-documents.md)
- [方法: プログラムによって文書に複数の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによってドキュメント内の範囲を拡張する](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
