---
title: IDebugMethodField::EnumLocals | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
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
ms.openlocfilehash: 2b0a7f080e26a6c55fa9ba759ed93e6b1eb09156
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
Creates an enumerator for selected local variables of the method.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT EnumLocals(   
   IDebugAddress*     pAddress,  
   IEnumDebugFields** ppLocals  
);  
```  
  
```csharp  
int EnumLocals(  
   IDebugAddress        pAddress,   
   out IEnumDebugFields ppLocals  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pAddress`  
 [in] An [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) object representing the debug address that selects the context or scope from which to get the locals.  
  
 `ppLocals`  
 [out] Returns an [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) object representing a list of the locals; otherwise, returns a null value if there are no locals.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns S_OK or returns S_FALSE if there are no locals. Otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 Only the variables defined within the block that contains the given debug address are enumerated. If all locals including any compiler-generated locals are needed, call the [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md) method.  
  
 A method can contain multiple scoping contexts or blocks. For example, the following contrived method contains three scopes, the two inner blocks and the method body itself.  
  
```csharp  
public void func(int index)  
{  
    // Method body scope  
    int a = 0;  
    if (index == 1)  
    {  
        // Inner scope 1  
        int temp1 = a;  
    }  
    else  
    {  
        // Inner scope 2  
        int temp2 = a;  
    }  
}  
```  
  
 The [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) object represents the `func` method itself. Calling the `EnumLocals` method with an [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) set to the `Inner Scope 1` address returns an enumeration containing the `temp1` variable, for example.  
  
## <a name="see-also"></a>See Also  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)   
 [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
