---
title: BP_RESOLUTION_DATA | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- BP_RESOLUTION_DATA
helpviewer_keywords:
- BP_RESOLUTION_DATA structure
ms.assetid: 9e0b9000-6a84-47b9-b07a-367a75764389
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
ms.openlocfilehash: f5be75214e9ab112cc3af17bd8bdcfae00083661
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="bpresolutiondata"></a>BP_RESOLUTION_DATA
Describes the result of binding a data breakpoint.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef struct _BP_RESOLUTION_DATA {   
   BSTR              bstrDataExpr;  
   BSTR              bstrFunc;  
   BSTR              bstrImage;  
   BP_RES_DATA_FLAGS dwFlags;  
} BP_RESOLUTION_DATA;  
```  
  
```csharp  
public struct BP_RESOLUTION_DATA {   
   public string bstrDataExpr;  
   public string bstrFunc;  
   public string bstrImage;  
   public uint   dwFlags;  
};  
```  
  
## <a name="members"></a>Members  
 `bstrDataExpr`  
 The data expression that has been bound.  
  
 `bstrFunc`  
 The name of the function the data breakpoint has bound in (if any).  
  
 `bstrImage`  
 The name of the module (MyModule.dll, for example) that the data breakpoint has bound in.  
  
 `dwFlags`  
 A value from the [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md) enumeration, describing how the data breakpoint is implemented.  
  
## <a name="remarks"></a>Remarks  
 This structure is a member of the [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) structure, which is in turn a member of the [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) structure returned by the [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md) method.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Structures and Unions](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)   
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)   
 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
