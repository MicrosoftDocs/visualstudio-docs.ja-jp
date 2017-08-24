---
title: IDebugDefaultPort2::GetPortNotify | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugDefaultPort2::GetPortNotify
helpviewer_keywords:
- IDebugDefaultPort2::GetPortNotify
ms.assetid: 3ae715ee-9886-4694-a52b-59bb3b27467a
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: e3331ff25ff54d7be58e85979f366fff72b643a0
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugdefaultport2getportnotify"></a>IDebugDefaultPort2::GetPortNotify
This method gets an [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) interface for this port.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetPortNotify(  
   IDebugPortNotify2** ppPortNotify  
);  
```  
  
```cs  
int GetPortNotify(  
   out IDebugPortNotify2 ppPortNotify  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppPortNotify`  
 [out] An [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) object.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Normally, the `QueryInterface` method is called on the object implementing the [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) interface to obtain an [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) interface. However, there are circumstances in which the desired interface is implemented on a different object. This method hides those circumstances and returns the `IDebugPortNotify2` interface from the most appropriate object.  
  
## <a name="see-also"></a>See Also  
 [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)   
 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
