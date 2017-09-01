---
title: EXCEPTION_INFO | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- EXCEPTION_INFO
helpviewer_keywords:
- EXCEPTION_INFO structure
ms.assetid: d046957a-b97d-420b-b46b-c67cbaef709e
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
ms.openlocfilehash: fbc402041df0633038681eb64583e9a9b41fb28c
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="exceptioninfo"></a>EXCEPTION_INFO
Describes an exception or run-time error thrown by the program being debugged.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef struct tagEXCEPTION_INFO {   
   IDebugProgram2* pProgram;  
   BSTR            bstrProgramName;  
   BSTR            bstrExceptionName;  
   DWORD           dwCode;  
   EXCEPTION_STATE dwState;  
   GUID            guidType;  
} EXCEPTION_INFO;  
```  
  
```csharp  
public struct EXCEPTION_INFO {   
   public IDebugProgram2 pProgram;  
   public string         bstrProgramName;  
   public string         bstrExceptionName;  
   public uint           dwCode;  
   public uint           dwState;  
   public Guid           guidType;  
};  
```  
  
## <a name="members"></a>Members  
 pProgram  
 The [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) object that represents the program in which the exception occurred.  
  
 bstrProgramName  
 The name of the program in which the exception occurred.  
  
 bstrExceptionName  
 The name of the exception.  
  
 dwCode  
 The identification code for the exception or run-time error.  
  
 dwState  
 A value from the [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md) enumeration that defines the state of the exception.  
  
 guidType  
 The GUID language identifier, either `guidLang` or `guidEng`.  
  
## <a name="remarks"></a>Remarks  
 This structure is passed as a parameter to the [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) and the [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) methods. This structure is also passed to the [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) method to be filled in.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Structures and Unions](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)   
 [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)   
 [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)
