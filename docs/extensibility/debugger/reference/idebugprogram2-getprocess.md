---
title: IDebugProgram2::GetProcess | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
caps.latest.revision: 13
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
ms.openlocfilehash: 87f9a71027f072a6083ff556402ae31dc03be53f
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
Get the process that this program is running in.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetProcess(  
   IDebugProcess2** ppProcess  
);  
```  
  
```csharp  
int GetProcess(  
   out IDebugProcess2 ppProcess  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppProcess`  
 [out] Returns the [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) interface that represents the process.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Unless a debug engine (DE) implements the [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md) interface, the DE's implementation of this method should always return `E_NOTIMPL` because a DE cannot determine which process it is running in and therefore cannot satisfy an implementation of this method.  
  
 Implementing the `IDebugEngineLaunch2` interface means that the DE must know how to create a process; therefore, the DE's implementation of the [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) interface is able to know what process it is running in.  
  
## <a name="see-also"></a>See Also  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)   
 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
