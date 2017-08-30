---
title: 'How to: Programmatically Print Visio Documents | Microsoft Docs'
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
- Visio [Office development in Visual Studio], printing Visio documents
- documents [Office development in Visual Studio], printing Visio documents
ms.assetid: 606a2678-5eb8-40b2-a50a-305cecb1b3d4
caps.latest.revision: 17
author: kempb
ms.author: kempb
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: a4bea4d1de77755044087bbcc6eca1ab6aee2dbc
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="how-to-programmatically-print-visio-documents"></a>How to: Programmatically Print Visio Documents
  You can print a complete Microsoft Office Visio document or only a specific page.  
  
 For details about the print methods, see the VBA reference documentation for the [Microsoft.Office.Interop.Visio.Document.Print](https://msdn.microsoft.com/library/office/ff767996.aspx) method and [Microsoft.Office.Interop.Visio.Page.Print](https://msdn.microsoft.com/library/office/ff765064.aspx) method.  
  
## <a name="printing-a-visio-document"></a>Printing a Visio Document  
  
#### <a name="to-print-a-complete-document"></a>To print a complete document  
  
-   Call the Microsoft.Office.Interop.Visio.Document.Print method of the Microsoft.Office.Interop.Visio.Document object that you want to print.  
  
     The following code example prints the active document. To use this example, run the code from the `ThisAddIn` class in your project.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#8](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#8)]  [!code-vb[Trin_VstcoreVisioAutomationAddIn#8](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#8)]  
  
## <a name="printing-a-page-of-a-visio-document"></a>Printing a Page of a Visio Document  
  
#### <a name="to-print-a-page-of-a-document"></a>To print a page of a document  
  
-   Call the Microsoft.Office.Interop.Visio.Pages.Print method of the Microsoft.Office.Interop.Visio.Pages object that you want to print.  
  
     The following code example prints the first page of the active document. To use this example, run the code from the `ThisAddIn` class in your project.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#9](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#9)]  [!code-vb[Trin_VstcoreVisioAutomationAddIn#9](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#9)]  
  
## <a name="see-also"></a>See Also  
 [Visio Solutions](../vsto/visio-solutions.md)   
 [Visio Object Model Overview](../vsto/visio-object-model-overview.md)   
 [How to: Programmatically Create New Visio Documents](../vsto/how-to-programmatically-create-new-visio-documents.md)   
 [How to: Programmatically Open Visio Documents](../vsto/how-to-programmatically-open-visio-documents.md)   
 [How to: Programmatically Close Visio Documents](../vsto/how-to-programmatically-close-visio-documents.md)   
 [How to: Programmatically Save Visio Documents](../vsto/how-to-programmatically-save-visio-documents.md)  
  
  
