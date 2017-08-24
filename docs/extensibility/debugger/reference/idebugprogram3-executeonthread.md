---
title: IDebugProgram3::ExecuteOnThread | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
caps.latest.revision: 6
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
ms.openlocfilehash: 2266e39c3a2791b8acf31300af8da2eb49dee727
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
Executes the debugger program. The thread is returned to give the debugger information on which thread the user is viewing when executing the program.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT ExecuteOnThread(  
   [in] IDebugThread2* pThread)  
```  
  
```cs  
int ExecuteOnThread(  
   IDebugThread2 pThread  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pThread`  
 [in] An [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) object.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 There are three different ways that a debugger can resume execution after stopping:  
  
-   Execute: Cancel any previous step, and run until the next breakpoint and so on.  
  
-   Step: Cancel any old step, and run until the new step completes.  
  
-   Continue: Run again, and leave any old step active.  
  
 The thread passed to `ExecuteOnThread` is useful when deciding which step to cancel. If you do not know the thread, running execute cancels all steps. With knowledge of the thread, you only need to cancel the step on the active thread.  
  
## <a name="see-also"></a>See Also  
 [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)   
 [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)
