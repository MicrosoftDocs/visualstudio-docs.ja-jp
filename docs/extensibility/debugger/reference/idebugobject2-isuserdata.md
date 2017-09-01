---
title: IDebugObject2::IsUserData | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugObject2::IsUserData
helpviewer_keywords:
- IDebugObject2::IsUserData method
ms.assetid: 6ffa0d0e-f742-496d-acc7-db74c248bc45
caps.latest.revision: 7
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
ms.openlocfilehash: d11a71b08910425f1b3c399dfc665ae629f7316d
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugobject2isuserdata"></a>IDebugObject2::IsUserData
Determines whether the object represents user data.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT IsUserData(  
   BOOL* pfUser  
);  
```  
  
```csharp  
int IsUserData(  
   out int pfUser  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pfUser`  
 [out] Returns nonzero (`TRUE`) if the object represents user data; zero (`FALSE`) if it does not.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns S_OK; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 User data is any object that is part of a module designated as JustMyCode (a user-configurable option that marks a module as user code and therefore visible in a stack trace).  
  
## <a name="see-also"></a>See Also  
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
