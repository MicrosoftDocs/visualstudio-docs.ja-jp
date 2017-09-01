---
title: IDebugBinder::ResolveRuntimeType | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugBinder::ResolveRuntimeType
helpviewer_keywords:
- IDebugBinder::ResolveRuntimeType method
ms.assetid: 6456ab3e-1c03-4f3c-91f9-16797ab7f5e7
caps.latest.revision: 12
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
ms.openlocfilehash: be2bbd889fa38645d8c3cd4438786a09819b71f1
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugbinderresolveruntimetype"></a>IDebugBinder::ResolveRuntimeType
This method determines the run-time type of an object.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT ResolveRuntimeType(   
   IDebugObject* pObject,  
   IDebugField** ppResolved  
);  
```  
  
```csharp  
int ResolveRuntimeType(  
   IDebugObject     pObject,   
   out IDebugField  ppResolved  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pObject`  
 [in] The [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) to be resolved.  
  
 `ppResolved`  
 [out] Returns the type of the object as an [IDebugField](../../../extensibility/debugger/reference/idebugfield.md).  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The run-time type of an object is not always known at compile time. For example, using polymorphism, an argument can be passed to a function as its base class, such as a button class. The actual argument might be a derived class, such as a radio button class.  
  
## <a name="see-also"></a>See Also  
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
