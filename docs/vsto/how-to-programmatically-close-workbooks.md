---
title: '方法: プログラムによってブックを閉じる'
description: プログラムで作業中のブックを閉じたり、ブックを指定して閉じたりする方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, closing
- Excel [Office development in Visual Studio], closing workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d09cbff06b1bb7048316629b7b958ee299029ec8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825265"
---
# <a name="how-to-programmatically-close-workbooks"></a>方法: プログラムによってブックを閉じる
  作業中のブックを閉じたり、ブックを指定して閉じたりすることができます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="close-the-active-workbook"></a>作業中のブックを閉じる
 作業中のブックを閉じる手順には、ドキュメント レベルのカスタマイズでの手順と VSTO アドインでの手順の 2 つがあります。

### <a name="to-close-the-active-workbook-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで作業中のブックを閉じるには

1. <xref:Microsoft.Office.Tools.Excel.Workbook.Close%2A> メソッドを呼び出して、カスタマイズに関連付けられているブックを閉じます。 次のコード例を使用するには、Excel のドキュメント レベルのプロジェクトの `Sheet1` クラスから実行します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet3":::

### <a name="to-close-the-active-workbook-in-a-vsto-add-in"></a>VSTO アドインで作業中のブックを閉じるには

1. <xref:Microsoft.Office.Interop.Excel._Workbook.Close%2A> メソッドを呼び出して、作業中のブックを閉じます。 次のコード例を使用するには、Excel 用 VSTO アドイン プロジェクトの `ThisAddIn` クラスから実行します。

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet1":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet1":::

## <a name="close-a-workbook-that-you-specify-by-name"></a>名前を指定してブックを閉じる
 名前を指定してブックを閉じる方法は、VSTO アドインとドキュメント レベルのカスタマイズで同じです。

### <a name="to-close-a-workbook-that-you-specify-by-name"></a>名前を指定してブックを閉じるには

1. <xref:Microsoft.Office.Interop.Excel.Workbooks> コレクションの引数にブック名を指定します。 次のコード例では、Excel で **NewWorkbook** というブックが開いていることを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet2":::

## <a name="see-also"></a>関連項目
- [ブックを操作する](../vsto/working-with-workbooks.md)
- [方法: プログラムによってブックを保存する](../vsto/how-to-programmatically-save-workbooks.md)
- [方法: プログラムによってブックを開く](../vsto/how-to-programmatically-open-workbooks.md)
- [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
