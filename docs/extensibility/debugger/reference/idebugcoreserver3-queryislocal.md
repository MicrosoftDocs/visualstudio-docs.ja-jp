---
title: IDebugCoreServer3::QueryIsLocal | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugCoreServer3::QueryIsLocal
helpviewer_keywords:
- IDebugCoreServer3::QueryIsLocal
ms.assetid: cca030de-f853-4ed7-b2fb-395f08a6b884
caps.latest.revision: 6
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
ms.openlocfilehash: d5cc1555f07f13dcce0de6d25ddf9399e9a3fdbc
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugcoreserver3queryislocal"></a>IDebugCoreServer3::QueryIsLocal
Determines if the server is local to the caller.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT QueryIsLocal(  
   void  
);  
```  
  
```cs  
int QueryIsLocal();  
```  
  
## <a name="return-value"></a>Return Value  
 Returns `S_OK` to indicate the server is local. Returns `S_FALSE` if the server is running from an instance of msvsmon.exe, which is typically used for remote debugging.  
  
## <a name="see-also"></a>See Also  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
