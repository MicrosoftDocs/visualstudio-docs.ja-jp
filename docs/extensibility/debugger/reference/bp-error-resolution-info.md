---
title: BP_ERROR_RESOLUTION_INFO | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- BP_ERROR_RESOLUTION_INFO
helpviewer_keywords:
- BP_ERROR_RESOLUTION_INFO structure
ms.assetid: a6b83242-5728-4716-80f3-840c96d59c6c
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
ms.openlocfilehash: 3f15c5d5176f12345f41dde7b0ac5fe729bd1202
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="bperrorresolutioninfo"></a>BP_ERROR_RESOLUTION_INFO
Describes the resolution of an error breakpoint, including location, program, and thread.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef struct _BP_ERROR_RESOLUTION_INFO {   
   BPERESI_FIELDS         dwFields;  
   BP_RESOLUTION_LOCATION bpResLocation;  
   IDebugProgram2*        pProgram;  
   IDebugThread2*         pThread;  
   BSTR                   bstrMessage;  
   BP_ERROR_TYPE          dwType;  
} BP_ERROR_RESOLUTION_INFO;  
```  
  
```csharp  
public struct BP_ERROR_RESOLUTION_INFO {   
   public uint                   dwFields;  
   public BP_RESOLUTION_LOCATION bpResLocation;  
   public IDebugProgram2         pProgram;  
   public IDebugThread2          pThread;  
   public string                 bstrMessage;  
   public uint                   dwType;  
};  
```  
  
## <a name="members"></a>Members  
 `dwFields`  
 A combination of values from the [BPERESI_FIELDS](../../../extensibility/debugger/reference/bperesi-fields.md) enumeration specifying which fields of this structure are filled out.  
  
 `bpResLocation`  
 The [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) union, which specifies the breakpoint resolution location.  
  
 `pProgram`  
 The [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) object that represents the application in which the breakpoint error occurred.  
  
 `pThread`  
 The [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) object that represents the thread on which the application that generated the breakpoint error is running.  
  
 `bstrMessage`  
 A string containing any warning or error message resulting from this error resolution.  
  
 `dwType`  
 A value from the [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md) enumeration that specifies the breakpoint error type.  
  
## <a name="remarks"></a>Remarks  
 This structure is returned from the [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) method.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Structures and Unions](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)   
 [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)   
 [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)
