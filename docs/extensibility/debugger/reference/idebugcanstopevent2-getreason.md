---
title: IDebugCanStopEvent2::GetReason | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: 1c010fdcce4059c1f3e4ba9c3a2682dc952d7c8a
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
Gets the reason why the debug engine (DE) wants to stop.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT GetReason(   
   CANSTOP_REASON* pcr  
);  
```  
  
```cs  
int GetReason(   
   out enum_CANSTOP_REASON pcr  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pcr`  
 [out] Returns a value from the [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md) enumeration that describes the reason for this event.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 This method is typically called before the [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) method so the caller can determine whether to pass non-zero (`TRUE`) to the `IDebugCanStopEvent2::CanStop` method.  
  
 The reason for stopping can be either `CANSTOP_ENTRYPOINT`, which means the DE has reached an entry point, or `CANSTOP_STEPIN`, which means the DE has stepped into a function.  
  
## <a name="see-also"></a>See Also  
 [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)   
 [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)   
 [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
