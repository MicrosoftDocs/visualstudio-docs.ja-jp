---
title: Bind to an Activity&#39;s Property Dialog Box (Legacy) | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- System.Workflow.ComponentModel.Design.ActivityBindForm.UI
helpviewer_keywords:
- Bind to an Activity's Property dialog box
ms.assetid: 19ebb207-e0a9-4642-8f5f-a5e31395c683
caps.latest.revision: 5
author: ErikRe
ms.author: erikre
manager: erikre
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 21a413a3e2d17d77fd83d5109587a96f323a0511
ms.openlocfilehash: 728d4399735732037ff6b8b903367ddb4a54b0d8
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="bind-to-an-activity39s-property-dialog-box-legacy"></a>Bind to an Activity&#39;s Property Dialog Box (Legacy)
This topic describes how use the **Bind to an Activity's Property** dialog box in the legacy [!INCLUDE[wfd1](../workflow-designer/includes/wfd1_md.md)]. Use the legacy [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)] when you need to target either the [!INCLUDE[netfx35_long](../workflow-designer/includes/netfx35_long_md.md)] or the [!INCLUDE[vstecwinfx](../workflow-designer/includes/vstecwinfx_md.md)].  
  
 An instance type of dependency property can be bound to another activity's public property or event. For more information about activity binding, see [Using Dependency Properties](http://go.microsoft.com/fwlink?LinkID=65007).  
  
 You select a property to bind to using the **Bind to an Activity's Property** dialog box. You open this dialog box by clicking the ellipsis **[...]** at the end of the selected property's text box in the **Properties** window, or by clicking the blue exclamation mark icon that appears next to the property name in the property browser.  
  
 The following table describes the user interface (UI) elements of the **Bind to an Activity's Property** dialog box.  
  
|UI Element|Description|  
|----------------|-----------------|  
|**Bind to an existing member**|Select a member that you want to bind to in the tree view pane. The pane below the tree view displays a message that indicates if the member is a valid type to bind to or not. Click **OK** to bind to the selected valid member.|  
|**Bind to a new member**|Create a new member field or property to bind to. Enter a **New Member Name**. Choose whether you want to create a dependency property or a public field by selecting **Create Field** or **Create Property**. Click **OK** to create the new member.|  
  
## <a name="see-also"></a>See Also  
 [Using Activity Properties](http://go.microsoft.com/fwlink?LinkID=65013)   
 [Using Dependency Properties](http://go.microsoft.com/fwlink?LinkID=65007)   
 [Legacy Designer for Windows Workflow Foundation UI Help](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)
