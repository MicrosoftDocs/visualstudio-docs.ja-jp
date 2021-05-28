---
title: '方法: プログラムによって文書内の範囲を拡張する'
description: ドキュメント レベルまたはアプリケーション レベルで Microsoft Word 文書内の開始点と終了点の範囲をプログラムによって拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, extending
- documents [Office development in Visual Studio], extending ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7a539bbbc4ad8d73477e660ef9903ac51dce712f
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826526"
---
# <a name="how-to-programmatically-extend-ranges-in-documents"></a>方法: プログラムによって文書内の範囲を拡張する
  Microsoft Office Word ドキュメントで <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを定義した後、その始点と終点を <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> メソッドと <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> メソッドを使用して変更します。 <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> と <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> のメソッドは、同じ 2 つの引数 (*Unit* と *Count*) を取ります。 *Count* 引数は、移動する単位の数です。*Unit* 引数は、次の <xref:Microsoft.Office.Interop.Word.WdUnits> 値のいずれかです。

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdCharacter>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdWord>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdSentence>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdParagraph>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdSection>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdStory>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdCell>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdColumn>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdRow>

- <xref:Microsoft.Office.Interop.Word.WdUnits.wdTable>

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

  次の例では、7 文字の範囲を定義します。 その後、開始位置を元の開始位置から 7 文字後に移動します。 範囲の終了位置も開始位置より 7 文字後にあるため、結果はゼロ文字からなる範囲になります。 このコードは続いて、終了位置を現在の終了位置から 7 文字後に移動します。

## <a name="to-extend-a-range"></a>範囲を拡張するには

1. 文字の範囲を定義します。 詳細については、「[方法: プログラムによって文書内の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)」を参照してください。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet39":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet39":::

     次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet39":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet39":::

2. <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range> メソッドを使用して、範囲の開始位置を移動します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet40":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet40":::

3. <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range> メソッドを使用して、範囲の終了位置を移動します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet41":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet41":::

## <a name="document-level-customization-code"></a>ドキュメント レベルのカスタマイズ コード

### <a name="to-extend-a-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで範囲を拡張するには

1. 次の例は、ドキュメント レベルのカスタマイズのコード全体を示しています。 このコードを使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet38":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet38":::

## <a name="vsto-add-in-code"></a>VSTO アドイン コード

### <a name="to-extend-a-range-in-an-application-level-vsto-add-in"></a>アプリケーション レベルの VSTO アドインで範囲を拡張するには

1. 次の例は、VSTO アドインのコード全体を示しています。 このコードを使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet38":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet38":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word 文書の範囲をリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [方法: プログラムによって文書内の範囲または選択項目を折りたたむ](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: 範囲の開始および終了文字をプログラムで取得する](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [方法: 範囲を作成するときにプログラムによって段落記号を除外する](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
