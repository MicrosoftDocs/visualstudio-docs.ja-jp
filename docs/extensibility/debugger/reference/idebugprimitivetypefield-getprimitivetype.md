---
title: "IDebugPrimitiveTypeField::GetPrimitiveType |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GetPrimitiveType
- IDebugPrimitiveTypeField::GetPrimitiveType
ms.assetid: a186c922-bbfe-478c-a744-b21eb4672d8f
caps.latest.revision: "10"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3cba27320cd633c3f98ee01ec09cd2b8efbb3a45
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="idebugprimitivetypefieldgetprimitivetype"></a>IDebugPrimitiveTypeField::GetPrimitiveType
このフィールドに関連付けられているプリミティブ型を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetPrimitiveType (  
   DWORD* pdwType  
);  
```  
  
```csharp  
int GetPrimitiveType (  
   out uint pdwType  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwType`  
 [out]値から、 [CorElementType 列挙型](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration)プリミティブ型を表すです。  
  
## <a name="return-value"></a>戻り値  
 成功した場合を返します`S_OK`、それ以外を返します`S_FALSE`です。  
  
## <a name="see-also"></a>関連項目  
 [IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)