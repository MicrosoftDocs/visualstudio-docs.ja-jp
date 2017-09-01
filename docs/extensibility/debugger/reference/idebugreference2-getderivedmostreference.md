---
title: IDebugReference2::GetDerivedMostReference | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
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
ms.openlocfilehash: 9c52e0deb9303790a10091bf645646546aef546d
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
Gets the derived-most reference of a reference. Reserved for future use.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetDerivedMostReference(   
   IDebugReference2** ppDerivedMost  
);  
```  
  
```csharp  
int GetDerivedMostReference(   
   out IDebugReference2 ppDerivedMost  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppDerivedMost`  
 [out] Returns an [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) object that represents the derived-most property.  
  
## <a name="return-value"></a>Return Value  
 Always returns `E_NOTIMPL`.  
  
## <a name="remarks"></a>Remarks  
 For example, if this property describes an object that implements `ClassRoot` but which is actually an instantiation of `ClassDerived` that is derived from `ClassRoot`, then this method returns an [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) object representing a reference to the `ClassDerived` object.  
  
## <a name="see-also"></a>See Also  
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
