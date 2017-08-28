---
title: IDebugDefaultPort2::QueryIsLocal | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugDefaultPort2::QueryIsLocal
helpviewer_keywords:
- IDebugDefaultPort2::QueryIsLocal
ms.assetid: 1a42e774-c6ed-419a-a0e3-cab5778652ca
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
ms.openlocfilehash: 169a4975770ea0704ebaf59d9fa5b621f30bd014
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="idebugdefaultport2queryislocal"></a>IDebugDefaultPort2::QueryIsLocal
This method determines whether this port is on the local machine.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT QueryIsLocal(  
   void  
);  
```  
  
```csharp  
int QueryIsLocal();  
```  
  
## <a name="return-value"></a>Return Value  
 Returns `S_OK` if this port is local (on the same machine as the caller) or `S_FALSE` if the port is on another machine.  
  
## <a name="see-also"></a>See Also  
 [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
