---
description: メモリ コンテキストと指定された配列内の各コンテキストとを比較フラグによって示される方法で比較し、一致する最初のコンテキストのインデックスを返します。
title: IDebugMemoryContext2::Compare | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Compare
helpviewer_keywords:
- IDebugMemoryContext2::Compare method
- Compare method
ms.assetid: c51b5128-848e-4d8e-b2e9-1161339763c3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 67acecafd677d5096e1bf975f85e21a5c6cbe133
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076772"
---
# <a name="idebugmemorycontext2compare"></a>IDebugMemoryContext2::Compare
メモリ コンテキストと指定された配列内の各コンテキストとを比較フラグによって示される方法で比較し、一致する最初のコンテキストのインデックスを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Compare( 
   CONTEXT_COMPARE        compare,
   IDebugMemoryContext2** rgpMemoryContextSet,
   DWORD                  dwMemoryContextSetLen,
   DWORD*                 pdwMemoryContext
);
```

```csharp
int Compare(
   enum_CONTEXT_COMPARE   compare,
   IDebugMemoryContext2[] rgpMemoryContextSet,
   uint                   dwMemoryContextSetLen,
   out uint               pdwMemoryContext
);
```

## <a name="parameters"></a>パラメーター
`compare`\
[入力] 比較の種類を決定する [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md) 列挙型の値。

`rgpMemoryContextSet`\
[入力] 比較する [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトへの参照の配列。

`dwMemoryContextSetLen`\
[入力] `rgpMemoryContextSet` 配列内のコンテキストの数。

`pdwMemoryContext`\
[出力] 比較を満たす最初のメモリ コンテキストのインデックスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 2 つのコンテキストを比較できない場合は、`E_COMPARE_CANNOT_COMPARE` を返します。

## <a name="remarks"></a>解説
 デバッグ エンジン (DE) では、すべての種類の比較をサポートする必要はありませんが、少なくとも `CONTEXT_EQUAL`、`CONTEXT_LESS_THAN`、`CONTEXT_GREATER_THAN`、および `CONTEXT_SAME_SCOPE` をサポートする必要があります。

## <a name="see-also"></a>関連項目
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)
