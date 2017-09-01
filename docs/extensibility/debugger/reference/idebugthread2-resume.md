---
title: IDebugThread2::Resume | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
caps.latest.revision: 10
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
ms.openlocfilehash: 20f4c7ecbcd724ad10c54eea2046407db443bd24
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
Resumes execution of a thread.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT Resume (   
   DWORD *pdwSuspendCount  
);  
```  
  
```csharp  
int Resume (   
   out uint pdwSuspendCount  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pdwSuspendCount`  
 [out] Returns the suspend count after the resume operation.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Each call to this method decrements the suspend count until it reaches 0 at which time, execution is actually resumed. This suspend count is displayed in the **Threads** debug window.  
  
 For each call to this method, there must be a previous call to the [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md) method. The suspend count determines how many times the `IDebugThread2::Suspend` method has been called so far.  
  
## <a name="see-also"></a>See Also  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md)
