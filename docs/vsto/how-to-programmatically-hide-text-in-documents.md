---
title: '方法: プログラムによって文書内のテキストを非表示にする'
description: 特定範囲のテキストに対応するフォントの [非表示] プロパティを設定して、Microsoft Word 文書内のテキストを非表示にする方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], hiding text
- text [Office development in Visual Studio], hiding in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 04ea6b56519656782a3e408892235fa177eef755
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826487"
---
# <a name="how-to-programmatically-hide-text-in-documents"></a>方法: プログラムによって文書内のテキストを非表示にする
  特定範囲のテキストに対応する <xref:Microsoft.Office.Interop.Word._Font.Hidden%2A> の <xref:Microsoft.Office.Interop.Word.Range.Font%2A> プロパティを設定して、文書内のテキストを非表示にできます。

 たとえば、文書をプリンターに送信する前に、<xref:Microsoft.Office.Tools.Word.Bookmark> (ドキュメント レベルのカスタマイズ) または <xref:Microsoft.Office.Interop.Word.Bookmark> (VSTO アドイン) 内のテキストを一時的に非表示にできます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-hide-text-in-a-bookmark-control-while-printing-the-document"></a>文書の印刷時に Bookmark コントロール内のテキストを非表示にするには

1. 指定した範囲内にあるテキストをすべて非表示にするプロシージャを作成します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet105":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet105":::

2. 指定した範囲内にあるテキストをすべて再表示するプロシージャを作成します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet106":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet106":::

3. `HideText` メソッドにブックマークの範囲を渡し、文書を印刷して、 `UnhideText` メソッドに同じ範囲を渡します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet107":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet107":::

     次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。 この例を使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet107":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet107":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例では、`bookmark1` という名前の <xref:Microsoft.Office.Tools.Word.Bookmark> コントロール (ドキュメント レベルのカスタマイズの場合) または <xref:Microsoft.Office.Interop.Word.Bookmark> コントロール (VSTO アドインの場合) が文書に含まれていることを前提にしています。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書を印刷する](../vsto/how-to-programmatically-print-documents.md)
- [方法: プログラムによって文書に複数の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって Word 文書の範囲をリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [方法: プログラムによってブックマークのテキストを更新する](../vsto/how-to-programmatically-update-bookmark-text.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
