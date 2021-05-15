---
title: '方法: プログラムを使用して新しいワークシートをブックに追加する'
description: プログラムを使用してワークシートを作成し、そのワークシートをブック内のワークシートのコレクションに追加する方法について学習します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, adding worksheets
- workbooks, creating worksheets
- worksheets, creating
- worksheets, adding to workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c093d61e38b3416fbef1e85dcf5af052c64db590
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827410"
---
# <a name="how-to-programmatically-add-new-worksheets-to-workbooks"></a>方法: プログラムを使用して新しいワークシートをブックに追加する
  プログラムによってワークシートを作成し、そのワークシートをブック内のワークシートのコレクションに追加できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、新しいワークシートをブックに追加するには

1. <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> コレクションの <xref:Microsoft.Office.Interop.Excel.Sheets> メソッドを使用します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet15":::

     新しいワークシートはネイティブの <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトであり、ホスト項目ではありません。 <xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目を追加するには、デザイン時にワークシートを追加する必要があります。

## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-vsto-add-in"></a>VSTO アドインで、新しいワークシートをブックに追加するには

1. <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> コレクションの <xref:Microsoft.Office.Interop.Excel.Sheets> メソッドを使用します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet11":::

     新しいワークシートはネイティブの <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトであり、ホスト項目ではありません。 ネイティブの <xref:Microsoft.Office.Tools.Excel.Worksheet> オブジェクトから <xref:Microsoft.Office.Interop.Excel.Worksheet> ホスト項目を生成することもできます。 詳細については、「 [Extending Word Documents and Excel Workbooks in VSTO Add-ins at Run Time](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [方法: プログラムによってブックからワークシートを削除する](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: プログラムによってワークシートを選択する](../vsto/how-to-programmatically-select-worksheets.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
