---
title: データ範囲をプログラムによって段階的にオートフィルする
description: Range オブジェクトの AutoFill メソッドを使用して、ワークシート内の特定の範囲に値を自動的に入力する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Autofill method [Excel]
- filling ranges automatically
- ranges, automatically filling
- workbooks, filling ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 615331181b9402e0d2062142ad266bdd41dca4eb
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824940"
---
# <a name="how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data"></a>方法: 段階的に変化するデータをプログラムによって範囲内に自動的に入力する
  <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトの <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> メソッドを使用すると、ワークシート内の特定の範囲に、値を自動的に入力することができます。 多くの場合、<xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> メソッドは、範囲内の値を段階的に増加または減少させるために使用されます。 この動作は、<xref:Microsoft.Office.Interop.Excel.XlAutoFillType> 列挙型からオプションの定数を提供することで指定できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> を使用する際には、次の 2 つの範囲を指定する必要があります。

- <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> メソッドを呼び出す範囲。このメソッドによって、入力の開始点が指定され、初期値が格納されます。

- 入力する範囲。これは、<xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> メソッドにパラメーターとして渡されます。 このターゲット範囲には、初期値を含めた範囲を指定する必要があります。

    > [!NOTE]
    > <xref:Microsoft.Office.Interop.Excel.Range> の代わりに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを渡すことはできません。 詳細については、「[ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet49":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet49":::

## <a name="compile-the-code"></a>コードのコンパイル
 入力する範囲の最初のセルには、初期値が格納される必要があります。

 この例では、次の 3 つの領域にデータを入力する必要があります。

- 列 B には、5 つの平日を格納します。 初期値として、セル B1 に「**Monday**」と入力します。

- 列 C には、5 つの月を格納します。 初期値として、セル C1 に「**January**」と入力します。

- 列 D には、行ごとに 2 ずつ増加する一連の数値を格納します。 初期値として、セル D1 に「**4**」、セル D2 に「**6**」と入力します。

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [方法: Excel の計算をプログラムで実行する](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
