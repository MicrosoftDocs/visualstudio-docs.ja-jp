---
title: IDebugFunctionObject2::Evaluate | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
caps.latest.revision: 8
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
ms.openlocfilehash: a00543427c753a6ff114d9b1188666980f7b17ab
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugfunctionobject2evaluate"></a>IDebugFunctionObject2::Evaluate
Calls the function and returns the resulting value as an object.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT Evaluate (  
   IDebugObject** ppParams,  
   DWORD          dwParams,  
   DWORD          dwEvalFlags,  
   DWORD          dwTimeout,  
   IDebugObject** ppResult  
);  
```  
  
```cs  
int Evaluate (  
   IDebugObject     ppParams,  
   uint             dwParams,  
   uint             dwEvalFlags,  
   uint             dwTimeout,  
   out IDebugObject ppResult  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppParams`  
 [in] An array of [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) objects that represents the input parameters. Each of these parameters was created by using one of the Create methods in this interface.  
  
 `dwParams`  
 [in] The number of parameters in the `ppParams` array.  
  
 `dwEvalFlags`  
 [in] A combination of flags from the [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) enumeration that specify how the evaluation is to be performed.  
  
 `dwTimeout`  
 [in] Specifies the maximum time, in milliseconds, to wait before returning from this method. Use **INFINITE** to wait indefinitely.  
  
 `ppResult`  
 [out] Returns an **IDebugObject** that represents the value of the function as an object.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="see-also"></a>See Also  
 [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
