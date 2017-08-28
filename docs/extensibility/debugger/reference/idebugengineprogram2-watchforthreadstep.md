---
title: IDebugEngineProgram2::WatchForThreadStep | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
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
ms.openlocfilehash: e87c6e5c38726c252a794ddb4342f4cc001861c4
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
Watches for execution (or stops watching for execution) to occur on the given thread.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT WatchForThreadStep(   
   IDebugProgram2* pOriginatingProgram,  
   DWORD           dwTid,  
   BOOL            fWatch,  
   DWORD           dwFrame  
);  
```  
  
```csharp  
int WatchForThreadStep(   
   IDebugProgram2 pOriginatingProgram,  
   uint           dwTid,  
   int            fWatch,  
   uint           dwFrame  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pOriginatingProgram`  
 [in] An [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) object representing the program being stepped.  
  
 `dwTid`  
 [in] Specifies the identifier of the thread to watch.  
  
 `fWatch`  
 [in] Non-zero (`TRUE`) means start watching for execution on the thread identified by `dwTid`; otherwise, zero (`FALSE`) means stop watching for execution on `dwTid`.  
  
 `dwFrame`  
 [in] Specifies a frame index that controls the step type. When this is value is zero (0), the step type is "step into" and the program should stop whenever the thread identified by `dwTid` executes. When `dwFrame` is non-zero, the step type is "step over" and the program should stop only if the thread identified by `dwTid` is running in a frame whose index is equal to or higher on the stack than `dwFrame`.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 When the session debug manager (SDM) steps a program, identified by the `pOriginatingProgram` parameter, it notifies all other attached programs by calling this method.  
  
 This method is applicable only to same-thread stepping.  
  
## <a name="see-also"></a>See Also  
 [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
