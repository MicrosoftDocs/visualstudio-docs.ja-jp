---
title: プログラムによって Excel の範囲内の日付値を格納および取得する
description: Visual Studio を使用して、Microsoft Excel の範囲内の日付値をプログラムによって格納および取得する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], retrieving date values from ranges
- ranges, retrieving data values
- dates, retrieving from Excel ranges
- Excel [Office development in Visual Studio], storing date values in ranges
- date values, storing in Excel ranges
- dates, storing in Excel ranges
- ranges, storing date values
- date values
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6e3115e00147a5dff850f6e0c051ffc3b6733218
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826240"
---
# <a name="how-to-programmatically-store-and-retrieve-date-values-in-excel-ranges"></a>方法: プログラムによって Excel の範囲内の日付値を格納および取得する
  <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブ Excel 範囲オブジェクトの値を格納および取得することができます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Visual Studio の Office 開発ツールを使用して、1/1/1900 以降の日付値を範囲に格納すると、その値は OLE オートメーション (OA) 形式で格納されます。 OLE オートメーション (OA) の日付の値を取得するには、<xref:System.DateTime.FromOADate%2A> メソッドを使用する必要があります。 1/1/1900 より前の日付は、文字列として格納されます。

> [!NOTE]
> 1900 年の最初の 2 か月については、Excel の日付と OLE オートメーションの日付は異なります。 また、 **[1904 年から計算する]** オプションがオンになっている場合にも違いがあります。 以下のコード例は、これらの違いには対処していません。

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する

- この例は、ドキュメント レベルのカスタマイズ用です。 このコードは、`ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

### <a name="to-store-a-date-value-in-a-named-range"></a>名前付き範囲に日付値を格納するには

1. <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをセル **A1** に作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet50":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet50":::

2. 今日の日付を `NamedRange1` の値として設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet51":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet51":::

### <a name="to-retrieve-a-date-value-from-a-named-range"></a>名前付き範囲から日付値を取得するには

1. `NamedRange1` から日付値を取得します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet52":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet52":::

## <a name="use-native-excel-ranges"></a>ネイティブ Excel 範囲を使用する

### <a name="to-store-a-date-value-in-a-native-excel-range-object"></a>ネイティブ Excel 範囲オブジェクトに日付値を格納するには

1. セル **A1** を表す <xref:Microsoft.Office.Interop.Excel.Range> を作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet25":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet25":::

2. 今日の日付を `rng` の値として設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet26":::

### <a name="to-retrieve-a-date-value-from-a-native-excel-range-object"></a>ネイティブ Excel 範囲オブジェクトから日付値を取得するには

1. `rng` から日付値を取得します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet27":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet27":::

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
