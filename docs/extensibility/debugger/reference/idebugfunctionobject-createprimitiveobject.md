---
title: IDebugFunctionObject::CreatePrimitiveObject | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugFunctionObject::CreatePrimitiveObject
helpviewer_keywords:
- IDebugFunctionObject::CreatePrimitiveObject method
ms.assetid: 6e9dc8b6-b4e1-4abf-b6e0-e885910775bc
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
ms.openlocfilehash: fd6aedb49b17fa818ee03ca4a5fed5758fe8a9c3
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugfunctionobjectcreateprimitiveobject"></a>IDebugFunctionObject::CreatePrimitiveObject
Creates a primitive data object, such as a simple integer.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT CreatePrimitiveObject(   
   OBJECT_TYPE    ot,  
   IDebugObject** ppObject  
);  
```  
  
```csharp  
int CreatePrimitiveObject(  
   enum_OBJECT_TYPE ot,   
   out IDebugObject ppObject  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ot`  
 [in] A value from the [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) enumeration representing the type of primitive to create.  
  
 `ppObject`  
 [out] Returns an [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) representing the newly created object.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns S_OK; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Call this method to create an object that represents a primitive object that is a parameter to the function which is represented by the [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) interface. For example, if the expression string is "myString(5)", this method would be used to create an object representing the integer 5.  
  
## <a name="see-also"></a>See Also  
 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
