---
title: IDebugParsedExpression::EvaluateSync | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: b3a0fb72daf623636e3aeb50f8c0681c8b98a7e4
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
This method evaluates the parsed expression and optionally casts the result to another data type.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT EvaluateSync(   
   DWORD                 dwEvalFlags,  
   DWORD                 dwTimeout,  
   IDebugSymbolProvider* pSymbolProvider,  
   IDebugAddress*        pAddress,  
   IDebugBinder*         pBinder,  
   BSTR                  bstrResultType,  
   IDebugProperty2**     ppResult  
);  
```  
  
```cs  
int EvaluateSync(  
   uint                 dwEvalFlags,   
   uint                 dwTimeout,   
   IDebugSymbolProvider pSymbolProvider,   
   IDebugAddress        pAddress,   
   IDebugBinder         pBinder,   
   string               bstrResultType,   
   out IDebugProperty2  ppResult  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `dwEvalFlags`  
 [in] A combination of [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) constants that control how the expression is to be evaluated.  
  
 `dwTimeout`  
 [in] Specifies the maximum time, in milliseconds, to wait before returning from this method. Use `INFINITE` to wait indefinitely.  
  
 `pSymbolProvider`  
 [in] The symbol provider, expressed as an [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) interface.  
  
 `pAddress`  
 [in] The current execution location within a method, expressed as an [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) interface.  
  
 `pBinder`  
 [in] The binder, expressed as an [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) interface.  
  
 `bstrResultType`  
 [in] The type the result should be cast to. This argument can be a null value.  
  
 `ppResult`  
 [out] Returns the [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) interface that represents the results of evaluation.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The expression evaluation context is given by `pAddress`, which makes it possible to determine the containing method and then use language scoping rules to determine the value of the symbols in the expression.  
  
## <a name="see-also"></a>See Also  
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
