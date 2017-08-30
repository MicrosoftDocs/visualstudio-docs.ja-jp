---
title: 'How to: Programmatically List All Worksheets in a Workbook | Microsoft Docs'
ms.custom: 
ms.date: 02/02/2017
ms.prod: visual-studio-dev14
ms.reviewer: 
ms.suite: 
ms.technology:
- office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing worksheets
- worksheets, listing
ms.assetid: 38b63d1d-6047-44e8-b089-c576c6179e4a
caps.latest.revision: 46
author: kempb
ms.author: kempb
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 03c0a0a04d2cbee58cee3441685a43e0bb327214
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="how-to-programmatically-list-all-worksheets-in-a-workbook"></a>How to: Programmatically List All Worksheets in a Workbook
  The <xref:Microsoft.Office.Interop.Excel.Workbook> class provides a <xref:Microsoft.Office.Interop.Excel.Worksheets> object. This object contains a collection of all the <xref:Microsoft.Office.Interop.Excel.Worksheet> objects in the workbook.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
### <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-document-level-customization"></a>To list all existing worksheets in a workbook in a document-level customization  
  
1.  Iterate through the <xref:Microsoft.Office.Interop.Excel.Worksheets> collection and send the name of each sheet to a cell offset from a <xref:Microsoft.Office.Tools.Excel.NamedRange> control.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#21)]  [!code-vb[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#21)]  
  
### <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-vsto-add-in"></a>To list all existing worksheets in a workbook in a VSTO Add-in  
  
1.  Iterate through the <xref:Microsoft.Office.Interop.Excel.Worksheets> collection and send the name of each sheet to a cell offset from a <xref:Microsoft.Office.Interop.Excel.Range> object.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#13)]  [!code-vb[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#13)]  
  
## <a name="see-also"></a>See Also  
 [Working with Worksheets](../vsto/working-with-worksheets.md)   
 [How to: Programmatically Add New Worksheets to Workbooks](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)   
 [How to: Programmatically Move Worksheets Within Workbooks](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)   
 [Global Access to Objects in Office Projects](../vsto/global-access-to-objects-in-office-projects.md)  
  
  
