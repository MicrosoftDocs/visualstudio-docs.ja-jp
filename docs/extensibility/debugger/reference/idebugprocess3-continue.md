---
title: IDebugProcess3::Continue | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
caps.latest.revision: 7
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
ms.openlocfilehash: 4b084e75c89e39632c31080d5dfbfc13e9ed04be
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
Continues running this process from a stopped state. Any previous execution state (such as a step) is preserved, and the process starts executing again.  
  
> [!NOTE]
>  This method should be used instead of [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md).  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT Continue(  
   IDebugThread2* pThread  
);  
```  
  
```cs  
int Continue(  
   IDebugThread2 pThread  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pThread`  
 [in] An [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) object representing the thread to be continued.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns error code.  
  
## <a name="remarks"></a>Remarks  
 This method is called on this process regardless of how many processes are being debugged, or which process generated the stopping event. The implementation must retain the previous execution state (such as a step) and continue execution as though it had never stopped before completing its prior execution. That is, if a thread in this process was doing a step-over operation and was stopped because some other process stopped, and then `Continue` was called, the specified thread must complete the original step-over operation.  
  
 **Warning** Do not send a stopping event or an immediate (synchronous) event to [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) while handling this call; otherwise the debugger may hang.  
  
## <a name="see-also"></a>See Also  
 [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
