---
title: '方法: プログラムによってワークシートを印刷する'
description: Visual Studio を使用して、Microsoft Excel ブック内の任意のワークシートをプログラムで印刷する方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- worksheets, printing
- print preview, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 129493f726967776aa669eb92f6e912ed9c1b11b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827150"
---
# <a name="how-to-programmatically-print-worksheets"></a>方法: プログラムによってワークシートを印刷する

ブック内のワークシートはすべて印刷できます。

[!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="print-a-worksheet-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズでワークシートを印刷する

### <a name="to-print-a-worksheet"></a>ワークシートを印刷するには

1. `Sheet1` の `PrintOut` メソッドを呼び出します。印刷部数は 2 部で、印刷前に文書をプレビューします。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet22":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet22":::

   <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> メソッドを使用すると、指定されたオブジェクトを **[印刷プレビュー]** ウィンドウに表示できます。 次のコードでは、`Sheet1` という名前の <xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目があることを前提としています。

### <a name="to-preview-a-page-before-printing"></a>印刷する前にページをプレビューするには

1. ワークシートの <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet23":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet23":::

## <a name="print-a-worksheet-in-a-vsto-add-in"></a>VSTO アドインでワークシートを印刷する

### <a name="to-print-a-worksheet"></a>ワークシートを印刷するには

1. 作業中のワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintOut%2A> メソッドを呼び出します。印刷部数は 2 部で、印刷前に文書をプレビューします。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet14":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet14":::

   <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> メソッドを使用すると、指定されたオブジェクトを **[印刷プレビュー]** ウィンドウに表示できます。

### <a name="to-preview-a-page-before-printing"></a>印刷する前にページをプレビューするには

1. 作業中のワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet15":::

## <a name="see-also"></a>関連項目

- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムを使用してワークシートでスペル チェックを行う](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [ワークシート ホスト項目](../vsto/worksheet-host-item.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
