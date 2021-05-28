---
description: このメソッドでは、このオブジェクトに関連付けられている引数の型の一覧を取得します。
title: IDebugBinder3::GetTypeArguments | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetTypeArguments
helpviewer_keywords:
- IDebugBinder3::GetTypeArguments method
ms.assetid: fa0c37a7-327f-463e-9a9d-bb3f534584cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf360e85f4fdc2d641b00c6cd2252e58fa0d06cb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089005"
---
# <a name="idebugbinder3gettypearguments"></a>IDebugBinder3::GetTypeArguments
このメソッドでは、このオブジェクトに関連付けられている引数の型の一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetTypeArguments(
   UINT          skip,
   UINT          count,
   IDebugField** ppFields,
   UINT*         pFetched
);
```

```csharp
int GetTypeArguments(
   uint          skip,
   uint          count,
   IDebugField[] ppFields,
   out uint      pFetched
);
```

## <a name="parameters"></a>パラメーター
`skip`\
[入力] 引数の型を取得する前にスキップするフィールドの数。

`count`\
[入力] 返される引数フィールドの数 (`ppFields` 配列のサイズも指定します)。

`ppFields`\
[入力、出力] このメソッドの戻り時に入力されるフィールドの配列。

`pFetched`\
[出力] \(省略可能) 実際に返された引数の型フィールドの数。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 引数の型の数は、[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md) で事前に取得できます。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)
