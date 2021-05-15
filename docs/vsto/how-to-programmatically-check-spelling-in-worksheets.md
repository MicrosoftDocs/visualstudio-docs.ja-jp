---
title: '方法: プログラムを使用してワークシートでスペル チェックを行う'
description: Microsoft Excel ワークシート内の単語のスペルをプログラムでチェックする方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- spellchecking
- spelling checker, worksheets
- worksheets, checking spelling
- spelling, checking in worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1bf35e225def686ae2424a89b7e5d6b77207ccee
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826058"
---
# <a name="how-to-programmatically-check-spelling-in-worksheets"></a>方法: プログラムを使用してワークシートでスペル チェックを行う
  ワークシート内の単語のスペルをプログラムでチェックすることができます。 ワークシート内の単語のスペルが正しくないと、 **[スペル チェック]** ダイアログ ボックスが自動的に表示されます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-check-spelling-in-a-worksheet-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズでワークシート内のスペルをチェックするには

1. ワークシートの <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet45":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet45":::

## <a name="to-check-spelling-in-a-worksheet-in-a-vsto-add-in"></a>VSTO アドインでワークシート内のスペルをチェックするには

1. 作業中のワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.CheckSpelling%2A> メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet22":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet22":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: Excel の計算をプログラムで実行する](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
