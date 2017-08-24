---
title: IDebugThread2::Suspend | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugThread2::Suspend
helpviewer_keywords:
- IDebugThread2::Suspend
ms.assetid: 1e20be85-aa12-48de-bb83-0bf0976e99ae
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: fa16bfc901bd4d6a7a36467886cbfae046a5f9b6
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugthread2suspend"></a>IDebugThread2::Suspend
Suspends a thread.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT Suspend (   
   DWORD *pdwSuspendCount  
);  
```  
  
```cs  
HRESULT Suspend (   
   out uint pdwSuspendCount  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pdwSuspendCount`  
 [out] Returns the suspend count after the suspend operation.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Each call to this method increments the suspend count above 0. This suspend count is displayed in the **Threads** debug window.  
  
 For each call to this method, there must be a later call to the [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) method.  
  
## <a name="see-also"></a>See Also  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
