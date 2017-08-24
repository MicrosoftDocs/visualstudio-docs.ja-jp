---
title: IDebugProgramNodeAttach2::OnAttach | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
caps.latest.revision: 3
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
ms.openlocfilehash: f6d113cdcd8e2eb958332e61a4da13e60505af00
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
Attaches to the associated program or defers the attach process to the [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) method.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT OnAttach(  
   [in] REFGUID guidProgramId  
);  
```  
  
```cs  
int OnAttach(  
   ref Guid guidProgramId  
};  
```  
  
#### <a name="parameters"></a>Parameters  
 `guidProgramId`  
 [in] `GUID` to assign to the associated program.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`. Returns `S_FALSE` if the [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) method should not be called. Otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 This method is called during the attach process, before the [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) method is called. The `OnAttach` method can perform the attach process itself (in which case, this method returns `S_FALSE`) or defer the attach process to the `IDebugEngine2::Attach` method (the `OnAttach` method returns `S_OK`). In either event, the `OnAttach` method can set the `GUID` of the program being debugged to the given `GUID`.  
  
## <a name="see-also"></a>See Also  
 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
