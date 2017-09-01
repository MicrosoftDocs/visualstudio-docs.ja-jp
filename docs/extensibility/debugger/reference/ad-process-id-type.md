---
title: AD_PROCESS_ID_TYPE | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
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
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 694582e69e19f155842e13e5f23314aa244d72b4
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="adprocessidtype"></a>AD_PROCESS_ID_TYPE
Specifies how to interpret a process ID in the [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) structure.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
typedef DWORD AD_PROCESS_ID_TYPE;  
```  
  
```csharp  
public enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
```  
  
## <a name="members"></a>Members  
 AD_PROCESS_ID_SYSTEM  
 Process ID is a system identifier. Use the `ProcessId.dwProcessId` field of the [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) structure.  
  
 AD_PROCESS_ID_GUID  
 Process ID is a GUID. Use the `ProcessId.guidProcessId` field of the `AD_PROCESS_ID` structure.  
  
## <a name="remarks"></a>Remarks  
 Used for the `ProcessIdType` member of the [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) structure to identify the type of process ID that is contained in the structure. Determines how to interpret the `ProcessId` union in the structure.  
  
## <a name="requirements"></a>Requirements  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>See Also  
 [Enumerations](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
