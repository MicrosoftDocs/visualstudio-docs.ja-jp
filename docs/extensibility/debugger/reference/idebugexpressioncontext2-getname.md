---
title: IDebugExpressionContext2::GetName | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugExpressionContext2::GetName
helpviewer_keywords:
- IDebugExpressionContext2::GetName
ms.assetid: c2b70d22-17af-4986-a7e3-930910367216
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
ms.openlocfilehash: 05b3289597a4ea0073ce4e2b3f734b1d5283faf2
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugexpressioncontext2getname"></a>IDebugExpressionContext2::GetName
Retrieves the name of the evaluation context.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT GetName(   
   BSTR* pbstrName  
);  
```  
  
```cs  
int GetName(   
   out string pbstrName  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pbstrName`  
 [out] Returns the name of the evaluation context.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="remarks"></a>Remarks  
 The name is the description of this evaluation context. It is typically something that can be parsed by an expression evaluator that refers to this exact evaluation context. For example, in C++ the name is as follows:  
  
```  
"{ function-name, source-file-name, module-file-name }"  
```  
  
## <a name="see-also"></a>See Also  
 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
