---
description: ジェネリック フィールドに関連付けられている型パラメーターの数を取得します。
title: IDebugGenericFieldDefinition::TypeParamCount | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TypeParamCount
- IDebugGenericFieldDefinition::TypeParamCount
ms.assetid: d41dd5ea-aa25-4bf3-bcfd-e0bf451ead49
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9a50f258fe3febdf7c1dd680ea6b731e756abf7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063397"
---
# <a name="idebuggenericfielddefinitiontypeparamcount"></a>IDebugGenericFieldDefinition::TypeParamCount
ジェネリック フィールドに関連付けられている型パラメーターの数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT TypeParamCount(
   ULONG32* pcParams
);
```

```csharp
int TypeParamCount(
   ref uint pcParams
);
```

## <a name="parameters"></a>パラメーター
`pcParams`\
[入力、出力] 型パラメーターの数。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 List\<T> の場合、このメソッドは 1 を返します。List\<T1,T2> の場合、このメソッドは 2 を返します。 型パラメーターがない場合、このメソッドは 0 を返します。

## <a name="see-also"></a>関連項目
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)
