---
title: IDebugModule3::IsUserCode | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugModule3::IsUserCode
helpviewer_keywords:
- IDebugModule3::IsUserCode
ms.assetid: 77022946-bb8b-4114-aa81-614df6e54b13
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
ms.openlocfilehash: 3f5bffdc71d82883799b94f2433e3eb7bdb37a7b
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugmodule3isusercode"></a>IDebugModule3::IsUserCode
Retrieves information on whether the module represents user code or not.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT IsUserCode(  
   BOOL* pfUser  
);  
```  
  
```csharp  
int IsUserCode(  
   out int pfUser  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pfUser`  
 [out] Nonzero (`TRUE`) if module represents user code, zero (`FALSE`) if it does not.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns error code.  
  
## <a name="see-also"></a>See Also  
 [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
