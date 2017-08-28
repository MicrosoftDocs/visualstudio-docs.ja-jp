---
title: Include Element | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- Include
helpviewer_keywords:
- Include element (VSCT XML schema)
- VSCT XML schema elements, Include
ms.assetid: c923dfe6-084a-4105-aec1-f0a3f8399c54
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
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
ms.translationtype: MT
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 92ac563092cae75cd32a5722a7f9f850545fcad9
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="include-element"></a>Include Element
The Include element specifies a file that can be located on the supplied include path for insertion into the current file.  All symbols and types defined will become part of the compiled result.  
  
## <a name="syntax"></a>Syntax  
  
```csharp  
<Include href="stdidcmd.h" />  
```  
  
## <a name="attributes-and-elements"></a>Attributes and Elements  
 The following sections describe attributes, child elements, and parent elements.  
  
### <a name="attributes"></a>Attributes  
  
|Attribute|Description|  
|---------------|-----------------|  
|href|Required. The path to the header file:<br /><br /> href="stdidcmd.h"|  
|Condition|Optional. See [Conditional Attributes](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Child Elements  
  
|Element|Description|  
|-------------|-----------------|  
|None.|None.|  
  
### <a name="parent-elements"></a>Parent Elements  
  
|Element|Description|  
|-------------|-----------------|  
|[CommandTable Element](../extensibility/commandtable-element.md)|Defines all of the elements that represent commands — that is, menu items, menus, toolbars, and combo boxes — that a VSPackage provides to the IDE.|  
  
## <a name="example"></a>Example  
  
```  
<Include href="PackagePlacements.vsct"/>  
```  
  
## <a name="see-also"></a>See Also  
 [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
