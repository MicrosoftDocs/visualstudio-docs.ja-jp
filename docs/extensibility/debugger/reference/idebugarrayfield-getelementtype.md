---
description: 配列に含まれる要素の型を返します。
title: IDebugArrayField::GetElementType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetElementType
helpviewer_keywords:
- IDebugArrayField::GetElementType method
ms.assetid: c46bf625-0a48-4cbb-8f1f-286356f2c065
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a4c6e5eb14d3fa320cb8b86c20c6d336466c42cc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058964"
---
# <a name="idebugarrayfieldgetelementtype"></a>IDebugArrayField::GetElementType
配列に含まれる要素の型を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetElementType( 
   IDebugField** ppType
);
```

```csharp
int GetElementType(
   out IDebugField ppType
);
```

## <a name="parameters"></a>パラメーター
`ppType`\
[出力] 要素の型を表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md) オブジェクトでは、配列の全要素が同じ型であると想定されます。

## <a name="see-also"></a>関連項目
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
