---
title: '方法: プログラムで新しいワークシートをブックに追加します。'
ms.date: 02/02/2017
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bc23a3d0dfc18a9271db80df2cb1a42677b8ed5e
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56643692"
---
# <a name="how-to-programmatically-add-new-worksheets-to-workbooks"></a>方法: プログラムで新しいワークシートをブックに追加します。
  プログラムによってワークシートを作成し、そのワークシートをブック内のワークシートのコレクションに追加できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、新しいワークシートをブックに追加するには

1.  <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> コレクションの <xref:Microsoft.Office.Interop.Excel.Sheets> メソッドを使用します。

     [!code-csharp[Trin_VstcoreExcelAutomation#15](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#15)]
     [!code-vb[Trin_VstcoreExcelAutomation#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#15)]

     新しいワークシートはネイティブの <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトであり、ホスト項目ではありません。 <xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目を追加するには、デザイン時にワークシートを追加する必要があります。

## <a name="to-add-a-new-worksheet-to-a-workbook-in-a-vsto-add-in"></a>VSTO アドインで、新しいワークシートをブックに追加するには

1.  <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> コレクションの <xref:Microsoft.Office.Interop.Excel.Sheets> メソッドを使用します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#11](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#11)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#11](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#11)]

     新しいワークシートはネイティブの <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトであり、ホスト項目ではありません。 ネイティブの <xref:Microsoft.Office.Tools.Excel.Worksheet> オブジェクトから <xref:Microsoft.Office.Interop.Excel.Worksheet> ホスト項目を生成することもできます。 詳細については、「 [VSTO アドインにおける実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ワークシートを操作します。](../vsto/working-with-worksheets.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [方法: プログラムによってブックからワークシートを削除します。](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: プログラムによってワークシートを選択します。](../vsto/how-to-programmatically-select-worksheets.md)
- [拡張オブジェクトを使用した Excel の自動化](../vsto/automating-excel-by-using-extended-objects.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
