---
title: IEnumDebugPorts2::Clone | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IEnumDebugPorts2::Clone
helpviewer_keywords:
- IEnumDebugPorts2::Clone
ms.assetid: d5ce77e8-bb99-409a-98fa-20fe5a0de25e
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: 218eb60df5f79dec5b08a97cdf701e5fcdb6759e
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="ienumdebugports2clone"></a>IEnumDebugPorts2::Clone
Returns a copy of the current enumeration as a separate object.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT Clone(  
   IEnumDebugPorts2** ppEnum  
);  
```  
  
```cs  
int Clone(  
   out IEnumDebugPorts2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppEnum`  
 [out] Returns a copy of this enumeration as a separate object.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The copy of the enumeration has the same state as the original at the time this method is called. However, the copy's and the original's states are separate and can be changed individually.  
  
## <a name="see-also"></a>See Also  
 [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
