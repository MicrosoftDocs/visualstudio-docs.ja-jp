---
title: 'How to: Programmatically Use Word Dialog Boxes in Hidden Mode | Microsoft Docs'
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
- hidden dialog boxes
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, hidden mode in Word
ms.assetid: a5619325-8b54-41f1-becb-3f6eae7e4a6b
caps.latest.revision: 48
author: kempb
ms.author: kempb
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 527b6c37d87f7a04d93e96692f6d40d4e25e8f39
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="how-to-programmatically-use-word-dialog-boxes-in-hidden-mode"></a>How to: Programmatically Use Word Dialog Boxes in Hidden Mode
  You can perform complex operations with one method call by invoking the built-in dialog boxes in Microsoft Office Word without displaying them to the user. You can do this by using the <xref:Microsoft.Office.Interop.Word.Dialog.Execute%2A> method of the <xref:Microsoft.Office.Interop.Word.Dialog> object without calling the <xref:Microsoft.Office.Interop.Word.Dialog.Display%2A> method.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="examples"></a>Examples  
 The following code examples demonstrate how to use the **Page Setup** dialog box in hidden mode to set multiple page setup properties with no user input. The examples use a <xref:Microsoft.Office.Interop.Word.Dialog> object to configure a custom page size. The specific settings for page setup, such as the top margin, bottom margin, and so on, are available as late-bound properties of the <xref:Microsoft.Office.Interop.Word.Dialog> object. These properties are dynamically created by Word at run time.  
  
 The following example demonstrates how to perform this task in Visual Basic projects where **Option Strict** is off and in Visual C# projects that target the [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]. In these projects, you can use late binding features in the Visual Basic and Visual C# compilers. To use this example, run it from the `ThisDocument` or `ThisAddIn` class in your project.  
  
 [!code-vb[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#123)] [!code-csharp[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#123)]  
  
 The following example demonstrates how to perform this task in Visual Basic projects where **Option Strict** is on. In these projects, you must use reflection to access the late-bound properties. To use this example, run it from the `ThisDocument` or `ThisAddIn` class in your project.  
  
 [!code-vb[Trin_VstcoreWordAutomation#104](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#104)]  
  
## <a name="see-also"></a>See Also  
 [How to: Programmatically Use Built-In Dialog Boxes in Word](../vsto/how-to-programmatically-use-built-in-dialog-boxes-in-word.md)   
 [Word Object Model Overview](../vsto/word-object-model-overview.md)   
 [Late Binding in Office Solutions](../vsto/late-binding-in-office-solutions.md)   
 [Reflection (C#)](/dotnet/csharp/programming-guide/concepts/reflection)  
 [Reflection (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)  
  
  
