---
title: DISASSEMBLY_STREAM_SCOPE | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- DISASSEMBLY_STREAM_SCOPE
helpviewer_keywords:
- DISASSEMBLY_STREAM_SCOPE enumeration
ms.assetid: 43e2b364-cbbe-4755-a7e6-a03f3054c965
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
ms.openlocfilehash: 5383c2dfce7e6d50df6926cdcdfc0caf22754d65
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="disassemblystreamscope"></a>DISASSEMBLY_STREAM_SCOPE
Specifies the scope of the disassembly stream.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
enum enum_DISASSEMBLY_STREAM_SCOPE {   
   DSS_HUGE     = 0x10000000,  
   DSS_FUNCTION = 0x0001,  
   DSS_MODULE   = (DSS_HUGE) | 0x0002,  
   DSS_ALL      = (DSS_HUGE) | 0x0003  
};  
typedef DWORD DISASSEMBLY_STREAM_SCOPE;  
```  
  
```csharp  
public enum enum_DISASSEMBLY_STREAM_SCOPE {   
   DSS_HUGE     = 0x10000000,  
   DSS_FUNCTION = 0x0001,  
   DSS_MODULE   = (DSS_HUGE) | 0x0002,  
   DSS_ALL      = (DSS_HUGE) | 0x0003  
};  
```  
  
## <a name="members"></a>Members  
 DSS_HUGE  
 Specifies that disassembling the code context would generate more output than a client would typically want to retrieve in a single call.  
  
 DSS_FUNCTION  
 Specifies that the function contained by the code context should be disassembled. Specifies that the disassembly stream represents a function, when returned by the [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md) method.  
  
 DSS_MODULE  
 When returned by the `IDebugDisassemblyStream2::GetScope` method, specifies that the disassembly stream represents a module.  
  
 DSS_ALL  
 Specifies disassembly for the entire address space.  
  
## <a name="remarks"></a>Remarks  
 Passed as an argument to the [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md) method and returned by the [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md) method.  
  
 These values may be combined with a bitwise `OR`.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Enumerations](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)   
 [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)
