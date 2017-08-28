---
title: IDebugFunctionObject::CreateStringObject | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugFunctionObject::CreateStringObject
helpviewer_keywords:
- IDebugFunctionObject::CreateStringObject method
ms.assetid: fd6070ab-07d4-4ea1-8d71-b16592d6f1a7
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
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 0bee94585adb586a008098d30018efd467c04f78
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugfunctionobjectcreatestringobject"></a>IDebugFunctionObject::CreateStringObject
Creates a string object.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT CreateStringObject(   
   LPCOLESTR      pcstrString,  
   IDebugObject** ppObject  
);  
```  
  
```csharp  
int CreateStringObject(  
   string      pcstrString,   
   out IDebugObject ppOjbect  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pcstrString`  
 [in] The string value for the string object.  
  
 `ppObject`  
 [out] Returns an [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) object that represents the newly created string object.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns S_OK; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Call this method to create an object that represents a string that is a parameter to the function which is represented by the [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) interface.  
  
## <a name="see-also"></a>See Also  
 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
