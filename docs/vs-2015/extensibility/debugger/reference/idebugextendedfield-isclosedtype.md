---
title: IDebugExtendedField::IsClosedType |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IsClosedType
- IDebugExtendedField::IsClosedType
ms.assetid: 9136fc57-74ff-4fe4-a6e2-b137cb9d5b08
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a1cf28e8391a1dd37949c042bd7d58d9c8b7da06
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58962943"
---
# <a name="idebugextendedfieldisclosedtype"></a>IDebugExtendedField::IsClosedType
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

フィールドがクローズ型を表すかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
