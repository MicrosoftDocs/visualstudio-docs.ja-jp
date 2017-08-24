---
title: FIELD_INFO_FIELDS | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
caps.latest.revision: 14
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: 45b40af3c81efe2c3e9851e59069e8e229674930
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="fieldinfofields"></a>FIELD_INFO_FIELDS
Specifies what information to retrieve about an [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) object.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
enum enum_FIELD_INFO_FIELDS {   
   FIF_FULLNAME  = 0x0001,  
   FIF_NAME      = 0x0002,  
   FIF_TYPE      = 0x0004,  
   FIF_MODIFIERS = 0x0008,  
   FIF_ALL       = 0xffffffff,  
   FIF_NONE      = 0x0000  
};  
typedef DWORD FIELD_INFO_FIELDS;  
```  
  
```cs  
public enum enum_FIELD_INFO_FIELDS {  
   FIF_FULLNAME  = 0x0001,  
   FIF_NAME      = 0x0002,  
   FIF_TYPE      = 0x0004,  
   FIF_MODIFIERS = 0x0008,  
   FIF_ALL       = 0xffffffff,  
   FIF_NONE      = 0x0000  
};  
```  
  
## <a name="members"></a>Members  
 FIF_FULLNAME  
 Initialize/use the `bstrFullName` field in the [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) structure.  
  
 FIF_NAME  
 Initialize/use the `bstrName` field in the `FIELD_INFO` structure.  
  
 FIF_TYPE  
 Initialize/use the `bstrType` field in the `FIELD_INFO` structure.  
  
 FIF_MODIFIERS  
 Initialize/use the `bstrModifiers` field in the `FIELD_INFO` structure.  
  
## <a name="remarks"></a>Remarks  
 These values are also passed as an argument to the [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) method to specify which fields of the [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) structure are to be initialized.  
  
 These values are also used in the `dwFields` member of the `FIELD_INFO` structure to indicate which fields are used and valid.  
  
 These flags may be combined with a bitwise `OR`.  
  
## <a name="requirements"></a>Requirements  
 Header: sh.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Enumerations](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
