---
title: IDebugPortRequest2::GetPortName | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugPortRequest2::GetPortName
helpviewer_keywords:
- IDebugPortRequest2::GetPortName
ms.assetid: 53e2a3a4-bb34-4a02-a983-6bd84ea70587
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: 54d218b4a706cdbfe918ebf3e50197e9131ea537
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugportrequest2getportname"></a>IDebugPortRequest2::GetPortName
Gets the name of the port.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT GetPortName(   
   BSTR* pbstrPortName  
);  
```  
  
```cs  
int GetPortName(   
   out string pbstrPortName  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pbstrPortName`  
 [out] Returns the name of the port.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) interface is usually passed from a debug package (the client) to a port supplier (the server) to obtain a connection to a port. Both the debug package and the port supplier are aware of the possible choices for the port. If a simple string can describe the port, then the `IDebugPortRequest2::GetPortName` method has enough information to make the connection. Otherwise, additional interfaces can be provided by the client, which can be obtained by the server using `IDebugPortRequest2::QueryInterface`.  
  
## <a name="see-also"></a>See Also  
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
