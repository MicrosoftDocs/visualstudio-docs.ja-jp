---
title: '方法: プログラムによって文書内の範囲を定義および選択する'
description: Range オブジェクトを使用して、Microsoft Word 文書内の範囲をプログラムによって定義および選択する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], selecting sentences
- documents [Office development in Visual Studio], ranges
- sentences, selecting in documents
- ranges, selecting in documents
- ranges, defining in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3a5dc0c7fb9f3e9a2b4a15447f81239db973c215
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825954"
---
# <a name="how-to-programmatically-define-and-select-ranges-in-documents"></a>方法: プログラムによって文書内の範囲を定義および選択する
  Microsoft Office Word 文書内に範囲を定義するには、<xref:Microsoft.Office.Interop.Word.Range> オブジェクトを使用します。 文書全体を選択するには、<xref:Microsoft.Office.Interop.Word.Range> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range.Select%2A> メソッドを使用する方法や、<xref:Microsoft.Office.Tools.Word.Document> クラス (ドキュメント レベルのカスタマイズの場合) または <xref:Microsoft.Office.Interop.Word.Document> クラス (VSTO アドインの場合) の Content プロパティを使用する方法など、いくつかの方法があります。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="define-a-range"></a>範囲を定義する
 次の使用例は、作業中の文書の最初の 7 文字 (非印刷文字を含む) で構成される新しい <xref:Microsoft.Office.Interop.Word.Range> オブジェクトの作成方法を示します。 次に、範囲内のテキストを選択します。

### <a name="to-define-a-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで範囲を定義するには

1. 文書に範囲を追加するには、<xref:Microsoft.Office.Tools.Word.Document> クラスの <xref:Microsoft.Office.Tools.Word.Document.Range%2A> メソッドに開始文字と終了文字を渡します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet18":::

### <a name="to-define-a-range-by-using-a-vsto-add-in"></a>VSTO アドインを使用して範囲を定義するには

1. 文書に範囲を追加するには、<xref:Microsoft.Office.Interop.Word.Document> クラスの <xref:Microsoft.Office.Interop.Word._Document.Range%2A> メソッドに開始文字と終了文字を渡します。 作業中の文書に範囲を追加するコード例を次に示します。 このコード例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet18":::

## <a name="select-a-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで範囲を選択するには
 次の例は、<xref:Microsoft.Office.Interop.Word.Range> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range.Select%2A> メソッドを使用して、または <xref:Microsoft.Office.Tools.Word.Document> クラスの <xref:Microsoft.Office.Tools.Word.Document.Content%2A> プロパティを使用して文書全体を選択する方法を示しています。

### <a name="to-select-the-entire-document-as-a-range-by-using-the-select-method"></a>Select メソッドを使用して文書全体を範囲として選択するには

1. 文書全体を含む <xref:Microsoft.Office.Interop.Word.Range> の <xref:Microsoft.Office.Interop.Word.Range.Select%2A> メソッドを使用します。 次のコード例を使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet19":::

### <a name="to-select-the-entire-document-as-a-range-by-using-the-content-property"></a>Content プロパティを使用して文書全体を範囲として選択するには

1. <xref:Microsoft.Office.Tools.Word.Document.Content%2A> プロパティを使用して、文書全体を含む範囲を定義します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet20":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet20":::

   また、他のオブジェクトのメソッドとプロパティを使用して範囲を定義することもできます。

### <a name="to-select-a-sentence-in-the-active-document"></a>作業中の文書の文を選択するには

1. <xref:Microsoft.Office.Interop.Word.Sentences> コレクション使用して範囲を設定します。 選択する文のインデックスを使用します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet21":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet21":::

   文を選択するもう 1 つの方法として、範囲の開始値と終了値を手動で設定する方法があります。

### <a name="to-select-a-sentence-by-manually-setting-the-start-and-end-values"></a>開始値と終了値を手動で設定して文を選択するには

1. 範囲変数を作成します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet23":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet23":::

2. 文書内に少なくとも 2 つの文があることを確認し、範囲の *Start* 引数と *End* 引数を設定した後、その範囲を選択します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet24":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet24":::

## <a name="select-a-range-by-using-a-vsto-add-in"></a>VSTO アドインを使用して範囲を選択する
 次の例は、<xref:Microsoft.Office.Interop.Word.Range> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range.Select%2A> メソッドを使用して、または <xref:Microsoft.Office.Interop.Word.Document> クラスの <xref:Microsoft.Office.Interop.Word._Document.Content%2A> プロパティを使用して文書全体を選択する方法を示しています。

### <a name="to-select-the-entire-document-as-a-range-by-using-the-select-method"></a>Select メソッドを使用して文書全体を範囲として選択するには

1. 文書全体を含む <xref:Microsoft.Office.Interop.Word.Range> の <xref:Microsoft.Office.Interop.Word.Range.Select%2A> メソッドを使用します。 次のコード例では、作業中の文書の内容を選択します。 このコード例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet19":::

### <a name="to-select-the-entire-document-as-a-range-by-using-the-content-property"></a>Content プロパティを使用して文書全体を範囲として選択するには

1. <xref:Microsoft.Office.Interop.Word._Document.Content%2A> プロパティを使用して、文書全体を含む範囲を定義します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet20":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet20":::

   また、他のオブジェクトのメソッドとプロパティを使用して範囲を定義することもできます。

### <a name="to-select-a-sentence-in-the-active-document"></a>作業中の文書の文を選択するには

1. <xref:Microsoft.Office.Interop.Word.Sentences> コレクション使用して範囲を設定します。 選択する文のインデックスを使用します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet21":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet21":::

   文を選択するもう 1 つの方法として、範囲の開始値と終了値を手動で設定する方法があります。

### <a name="to-select-a-sentence-by-manually-setting-the-start-and-end-values"></a>開始値と終了値を手動で設定して文を選択するには

1. 範囲変数を作成します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet23":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet23":::

2. 文書内に少なくとも 2 つの文があることを確認し、範囲の *Start* 引数と *End* 引数を設定した後、その範囲を選択します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet24":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet24":::

## <a name="see-also"></a>関連項目
- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)
- [方法: プログラムによって文書内の範囲を拡張する](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [方法: 範囲の開始および終了文字をプログラムで取得する](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [方法: プログラムによって文書内の範囲を拡張する](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [方法: プログラムによって Word 文書の範囲をリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [方法: プログラムによって文書内の範囲または選択範囲を縮小する](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [方法: 範囲を作成するときにプログラムによって段落記号を除外する](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
