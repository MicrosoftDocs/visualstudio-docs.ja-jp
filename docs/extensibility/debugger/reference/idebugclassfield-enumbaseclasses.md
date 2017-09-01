---
title: IDebugClassField::EnumBaseClasses | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugClassField::EnumBaseClasses
helpviewer_keywords:
- IDebugClassField::EnumBaseClasses method
ms.assetid: 78749674-ef75-46d3-a1f4-ff33afd90e32
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
ms.openlocfilehash: 21e2de0ff49be7b1ef25d2b9d5be81ef0aafc6dd
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugclassfieldenumbaseclasses"></a>IDebugClassField::EnumBaseClasses
Creates an enumerator for the base classes of this class.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT EnumBaseClasses(   
   IEnumDebugFields** ppEnum  
);  
```  
  
```csharp  
int EnumBaseClasses(  
   out IEnumDebugFields ppEnum  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppEnum`  
 [out] Returns an [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) object representing the list of base classes. Returns a null value if there are no base classes.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns S_OK, returns S_SH_NO_BASE_CLASSES if there are no base classes (and the `ppEnum` parameter is set to a null value); otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The base classes in the enumerator object are specified in order of the most immediate (or most derived) base class to the most remote base class. For example, given the C++ classes:  
  
```  
class Root { }  
class Level1 : Root { }  
class Level2 : Level1 { }  
class MyClass : Level2 { }  
```  
  
 The enumeration would return the base classes in the order `Level2`, `Level1`, `Root`.  
  
## <a name="see-also"></a>See Also  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
