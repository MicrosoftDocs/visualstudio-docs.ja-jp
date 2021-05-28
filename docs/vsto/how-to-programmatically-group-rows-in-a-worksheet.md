---
title: '方法: ワークシート内の行をプログラムによってグループ化する'
description: Microsoft Excel で、NamedRange コントロールまたはネイティブ Excel 範囲オブジェクトを使用することにより、1 つ以上の行全体をプログラムによってグループ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, creating groups
- groups, creating in worksheets
- ranges, creating groups
- worksheets, clearing groups
- groups
- groups [Office development in Visual Studio], clearing in worksheets
- worksheets, ungrouping rows and columns
- rows [Office development in Visual Studio], ungrouping
- columns [Office development in Visual Studio], ungrouping
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: eaa0bbcc2c26a36e43e862cbe5a8f117c2a1fb26
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885418"
---
# <a name="how-to-programmatically-group-rows-in-a-worksheet"></a>方法: ワークシート内の行をプログラムによってグループ化する
  1 つ以上の行全体をグループ化できます。 ワークシートでグループを作成するには、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブ Excel 範囲オブジェクトを使用します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する
 デザイン時に <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをドキュメント レベルのプロジェクトに追加した場合は、そのコントロールを使用してプログラムでグループを作成できます。 次の例では、同じワークシートに `data2001`、`data2002`、`dataAll` という 3 つの <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールがあるものとします。 各名前付き範囲により、ワークシート内の行全体が参照されています。

### <a name="to-create-a-group-of-namedrange-controls-on-a-worksheet"></a>ワークシートで NamedRange コントロールのグループを作成するには

1. 各範囲の <xref:Microsoft.Office.Tools.Excel.NamedRange.Group%2A> メソッドを呼び出すことによって、3 つの名前付き範囲をグループ化します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     [!code-csharp[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#32)]
     [!code-vb[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#32)]

    > [!NOTE]
    > 行のグループ化を解除するには、<xref:Microsoft.Office.Tools.Excel.NamedRange.Ungroup%2A> メソッドを呼び出します。

## <a name="use-native-excel-ranges"></a>ネイティブ Excel 範囲を使用する
 このコードでは、`data2001`、`data2002`、`dataAll` という名前の 3 つの Excel 範囲が、ワークシートにあるものとします。

### <a name="to-create-a-group-of-excel-ranges-in-a-worksheet"></a>ワークシートで Excel 範囲のグループを作成するには

1. 各範囲の <xref:Microsoft.Office.Interop.Excel.Range.Group%2A> メソッドを呼び出すことによって、3 つの名前付き範囲をグループ化します。 次の例では、同じワークシートに `data2001`、`data2002`、`dataAll` という名前の 3 つの <xref:Microsoft.Office.Interop.Excel.Range> コントロールがあるものとします。 各名前付き範囲により、ワークシート内の行全体が参照されています。

     [!code-csharp[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#33)]
     [!code-vb[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#33)]

    > [!NOTE]
    > 行のグループ化を解除するには、<xref:Microsoft.Office.Interop.Excel.Range.Ungroup%2A> メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
