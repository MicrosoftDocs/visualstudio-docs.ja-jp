---
title: IEnumDebugCodeContexts2::GetCount | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IEnumDebugCodeContexts2::GetCount
helpviewer_keywords:
- IEnumDebugCodeContexts2::GetCount
ms.assetid: 74c52fcf-688c-40df-9acd-29b3b84e6216
caps.latest.revision: 11
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
ms.openlocfilehash: 69723add7c2c400947bb5c1324371f343acd375a
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="ienumdebugcodecontexts2getcount"></a>IEnumDebugCodeContexts2::GetCount
Returns the number of elements in the enumeration.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetCount(  
   ULONG* pcelt  
);  
```  
  
```csharp  
int GetCount(  
   out uint pcelt  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pcelt`  
 [out] Returns the number of elements in the enumeration.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 This method is not part of the customary COM enumeration interface which specifies that only the `Next`, `Clone`, `Skip`, and `Reset` methods need to be implemented.  
  
## <a name="see-also"></a>See Also  
 [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)
