---
title: IDebugEngine2::SetMetric | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugEngine2:::SetMetric
helpviewer_keywords:
- IDebugEngine2:::SetMetric
ms.assetid: dcda4972-c32e-4693-a0e1-25d5c58b9782
caps.latest.revision: 15
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
ms.openlocfilehash: b7e1090e5e345ca969294efea6a002ff84052351
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugengine2setmetric"></a>IDebugEngine2::SetMetric
This method sets a registry value known as a metric.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT SetMetric(  
   LPCOLESTR pszMetric,  
   VARIANT   varValue  
);  
```  
  
```cs  
int SetMetric(  
   string pszMetric,  
   object varValue  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pszMetric`  
 [in] The metric name.  
  
 `varValue`  
 [in] Specifies the metric value.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 A metric is a registry value used to change a debug engine's behavior or to advertise supported functionality. This method can forward the call to the appropriate form of the [SDK Helpers for Debugging](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) function, `SetMetric`.  
  
## <a name="see-also"></a>See Also  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [SDK Helpers for Debugging](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
