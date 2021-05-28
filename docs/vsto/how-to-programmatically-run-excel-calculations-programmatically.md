---
title: '方法: Excel の計算をプログラムで実行する'
description: Visual Studio を使用して、Microsoft Excel ブック内の計算をプログラムで実行する方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, running calculations
- calculations, running in Excel
- Excel [Office development in Visual Studio], running calculations programmatically
- workbooks, running calculations
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9fdc9cbc1966ac0fd862b795d66c7004f5089499
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823965"
---
# <a name="how-to-programmatically-run-excel-calculations"></a>方法: Excel の計算をプログラムで実行する
  <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールとネイティブの Excel 範囲オブジェクトでは、同様のプロセスを使って計算を実行できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="run-calculations-in-a-namedrange-control"></a>NamedRange コントロールで計算を実行する
 次の例では、セル A1 に <xref:Microsoft.Office.Tools.Excel.NamedRange> を作成した後、そのセルを計算します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

### <a name="to-run-calculations-in-a-namedrange-control"></a>NamedRange コントロールで計算を実行するには

1. 名前付き範囲を作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet75":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet75":::

2. 指定された範囲の <xref:Microsoft.Office.Tools.Excel.NamedRange.Calculate%2A> メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet76":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet76":::

## <a name="run-calculations-in-a-native-excel-range"></a>ネイティブの Excel 範囲で計算を実行する

### <a name="to-run-calculations-in-a-native-excel-range"></a>ネイティブの Excel 範囲で計算を実行するには

1. 名前付き範囲を作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet30":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet30":::

2. 指定された範囲の <xref:Microsoft.Office.Interop.Excel.Range.Calculate%2A> メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet31":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet31":::

## <a name="see-also"></a>こちらもご覧ください
- [範囲の操作](../vsto/working-with-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
