---
title: CODE_PATH | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CODE_PATH
helpviewer_keywords:
- CODE_PATH structure
ms.assetid: 2d4b2890-4c9d-47e1-83c0-df9c6436427f
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: c3e9b04d1e88355d9846038c25f6db35a7fd8435
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="codepath"></a>CODE_PATH
Describes a method or function call.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
typedef struct tagCODE_PATH {   
   BSTR                bstrName;  
   IDebugCodeContext2* pCode;  
} CODE_PATH;  
```  
  
```cs  
public struct CODE_PATH {  
   public string            bstrName;  
   public IDebugCodeContext pCode;  
}  
```  
  
## <a name="members"></a>Members  
 bstrName  
 The name of the code path.  
  
 pCode  
 The [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) object that identifies where in the code to step into a function.  
  
## <a name="remarks"></a>Remarks  
 This structure is used to implement stepping into a function. [EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md) returns all the calls from the current location in the program being debugged. This structure represents one such call.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Structures and Unions](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)
