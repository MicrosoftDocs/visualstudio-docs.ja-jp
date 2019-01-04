---
title: IDebugExtendedField::IsClosedType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IsClosedType
- IDebugExtendedField::IsClosedType
ms.assetid: 9136fc57-74ff-4fe4-a6e2-b137cb9d5b08
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ae7d6010bcc7c80f6b61c04242e5f335e3a3f013
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53850675"
---
# <a name="idebugextendedfieldisclosedtype"></a>IDebugExtendedField::IsClosedType
フィールドがクローズ型を表すかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsClosedType(  
   void  
);  
```  
  
```csharp  
int IsClosedType();  
```  
  
## <a name="return-value"></a>戻り値  
 フィールドがクローズ型の場合は、返す`S_OK`。 それ以外を返します`S_FALSE`します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)