---
title: '方法: Excel の計算をプログラムで実行します。'
ms.date: 02/02/2017
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a81bcfc6c9f5db47c2140e68a7b609efc92bf8fe
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56610516"
---
# <a name="how-to-programmatically-run-excel-calculations"></a>方法: Excel の計算をプログラムで実行します。
  計算を実行する同様のプロセスを使用して、<xref:Microsoft.Office.Tools.Excel.NamedRange>コントロールまたはネイティブな Excel 範囲オブジェクト。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="run-calculations-in-a-namedrange-control"></a>NamedRange コントロール内の計算を実行します。
 次の例では、作成、<xref:Microsoft.Office.Tools.Excel.NamedRange>セル A1 にし、セルを計算します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

### <a name="to-run-calculations-in-a-namedrange-control"></a>NamedRange コントロール内の計算を実行するには

1.  名前付き範囲を作成します。

     [!code-csharp[Trin_VstcoreExcelAutomation#75](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#75)]
     [!code-vb[Trin_VstcoreExcelAutomation#75](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#75)]

2.  呼び出す、<xref:Microsoft.Office.Tools.Excel.NamedRange.Calculate%2A>指定された範囲のメソッド。

     [!code-csharp[Trin_VstcoreExcelAutomation#76](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#76)]
     [!code-vb[Trin_VstcoreExcelAutomation#76](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#76)]

## <a name="run-calculations-in-a-native-excel-range"></a>ネイティブな Excel 範囲で計算を実行します。

### <a name="to-run-calculations-in-a-native-excel-range"></a>ネイティブな Excel 範囲で計算を実行するには

1.  名前付き範囲を作成します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#30](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#30)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#30](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#30)]

2.  呼び出す、<xref:Microsoft.Office.Interop.Excel.Range.Calculate%2A>指定された範囲のメソッド。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#31](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#31)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#31](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#31)]

## <a name="see-also"></a>関連項目
- [範囲を操作します。](../vsto/working-with-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
