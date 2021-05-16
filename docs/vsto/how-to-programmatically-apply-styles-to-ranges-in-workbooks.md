---
title: '方法: プログラムによってブック内の範囲にスタイルを適用する'
description: ブック内の領域に名前付きスタイルを適用する方法について学習します。 Excel には、定義済みのスタイルがいくつか用意されています。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, styles
- styles, workbook ranges
- workbooks, styles
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b1ce30c9a0e21bd4b8860f7a4d17191c48cd2ad9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828307"
---
# <a name="how-to-programmatically-apply-styles-to-ranges-in-workbooks"></a>方法: プログラムによってブック内の範囲にスタイルを適用する
  ブック内の領域に名前付きスタイルを適用できます。 Excel には、定義済みのスタイルがいくつか用意されています。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 **[セルの書式設定]** ダイアログ ボックスには、セルの書式を設定するために使用できるすべてのオプションが表示されます。これらの各オプションはコードから使用できます。 Excel でこのダイアログ ボックスを表示するには、 **[書式]** メニューの **[セル]** をクリックします。

## <a name="to-apply-a-style-to-a-named-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで名前付き範囲にスタイルを適用するには

1. 新しいスタイルを作成し、その属性を設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet53":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet53":::

2. <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを作成し、テキストを割り当て、新しいスタイルを適用します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet54":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet54":::

## <a name="to-clear-a-style-from-a-named-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで名前付き範囲からスタイルをクリアするには

1. Normal スタイルを範囲に適用します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet55":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet55":::

## <a name="to-apply-a-style-to-a-named-range-in-a-vsto-add-in"></a>VSTO アドインで名前付き範囲にスタイルを適用するには

1. 新しいスタイルを作成し、その属性を設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet28":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet28":::

2. <xref:Microsoft.Office.Interop.Excel.Range> を作成し、テキストを割り当て、新しいスタイルを適用します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet29":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet29":::

## <a name="to-clear-a-style-from-a-named-range-in-a-vsto-add-in"></a>VSTO アドインで名前付き範囲からスタイルをクリアするには

1. Normal スタイルを範囲に適用します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet56":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet56":::

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
