---
title: '方法: プログラムによってコード内でワークシートの範囲を参照する'
description: Visual Studio を使用して、Microsoft Excel ワークシート内の NamedRange コントロールまたはネイティブの Excel 範囲オブジェクトのコンテンツをプログラムで参照する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, referring to
- worksheets, referring to ranges
- referring to worksheet ranges
- Excel [Office development in Visual Studio], referring to worksheet ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6ea4e3da3c67d55aedea0d85a0a35b8ed2cf93b6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827085"
---
# <a name="how-to-programmatically-refer-to-worksheet-ranges-in-code"></a>方法: プログラムによってコード内でワークシートの範囲を参照する
  同様のプロセスを使用して、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブの Excel 範囲オブジェクトのコンテンツを参照します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する
 次の例では、ワークシートに <xref:Microsoft.Office.Tools.Excel.NamedRange> を追加し、その範囲内のセルにテキストを追加します。

### <a name="to-refer-to-a-namedrange-control"></a>NamedRange コントロールを参照するには

1. 文字列を <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールの <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> プロパティに割り当てます。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet46":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet46":::

## <a name="use-native-excel-ranges"></a>ネイティブの Excel 範囲を使用する
 次の例では、ワークシートにネイティブの Excel 範囲を追加し、その範囲内のセルにテキストを追加します。

### <a name="to-refer-to-a-native-range-object"></a>ネイティブ範囲オブジェクトを参照するには

1. 文字列を範囲の <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> プロパティに割り当てます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet47":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet47":::

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [方法: プログラムを使用してワークシートでスペル チェックを行う](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [方法: 増分するデータを範囲内にプログラムによって自動的に入力する](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [方法: プログラムによってワークシートの範囲内のテキストを検索する](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
