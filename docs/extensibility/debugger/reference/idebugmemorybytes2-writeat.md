---
title: IDebugMemoryBytes2::WriteAt | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugMemoryBytes2::WriteAt
helpviewer_keywords:
- IDebugMemoryBytes2::WriteAt method
- WriteAt method
ms.assetid: 61cc3704-47fa-4d9b-aa62-bb4585ac8fb1
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: 4b6066de1c205e7df469c2c4f016e533ae9fd01a
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
Writes the specified number of bytes of memory, starting at the specified address.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT WriteAt(   
   IDebugMemoryContext2* pStartContext,  
   DWORD                 dwCount,  
   BYTE*                 rgbMemory  
);  
```  
  
```cs  
int WriteAt(  
   IDebugMemoryContext2 pStartContext,  
   uint                 dwCount,  
   byte[]               rgbMemory  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pStartContext`  
 [in] The [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) object that specifies where to start writing bytes.  
  
 `dwCount`  
 [in] The number of bytes to write.  
  
 `rgbMemory`  
 [in] The bytes to write. This array is assumed to be at least `dwCount` bytes in size.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns `S_FALSE` if not all bytes could be written or returns an error code (typically `E_FAIL`).  
  
## <a name="remarks"></a>Remarks  
 If the starting address is not within the memory window represented by this [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) object, no writing occurs and an error code of `E_FAIL` is returned — even if the amount to write overlaps into the memory space.  
  
## <a name="see-also"></a>See Also  
 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
