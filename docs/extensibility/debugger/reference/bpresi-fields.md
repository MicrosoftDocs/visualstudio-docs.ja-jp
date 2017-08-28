---
title: BPRESI_FIELDS | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- BPRESI_FIELDS
helpviewer_keywords:
- BPRESI_FIELDS enumeration
ms.assetid: 99f17b1e-3e67-4f85-89d6-5c6cf45c8008
caps.latest.revision: 11
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
ms.openlocfilehash: 7bf02f2da4f11c5e0c702f331b9960d30f9b282f
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="bpresifields"></a>BPRESI_FIELDS
Specifies the information  to be retrieved about the successful resolution of a breakpoint.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
enum enum_BPRESI_FIELDS {   
   BPRESI_BPRESLOCATION = 0x0001,  
   BPRESI_PROGRAM       = 0x0002,  
   BPRESI_THREAD        = 0x0004,  
   BPRESI_ALLFIELDS     = 0xffffffff  
};  
typedef DWORD BPRESI_FIELDS;  
```  
  
```csharp  
public enum enum_BPRESI_FIELDS {   
   BPRESI_BPRESLOCATION = 0x0001,  
   BPRESI_PROGRAM       = 0x0002,  
   BPRESI_THREAD        = 0x0004,  
   BPRESI_ALLFIELDS     = 0xffffffff  
};  
```  
  
## <a name="members"></a>Members  
 BPRESI_BPRESLOCATION  
 Initialize/use the `bpResLocation` (breakpoint resolution location) field of the [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) structure.  
  
 BPRESI_PROGRAM  
 Initialize/use the `pProgram` field of the `BP_RESOLUTION_INFO` structure.  
  
 BPRESI_THREAD  
 Initialize/use the `pThread` field of the `BP_RESOLUTION_INFO` structure.  
  
 BPRESI_ALLFIELDS  
 Specifies all fields.  
  
## <a name="remarks"></a>Remarks  
 Passed to the [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md) method to indicate which fields of the [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) structure are to be initialized.  
  
 These flags are also used to indicate which fields of the `BP_RESOLUTION_INFO` structure are used and valid when that structure is returned.  
  
 These values may be combined with a bitwise `OR`.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Enumerations](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)   
 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
