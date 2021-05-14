---
description: 指定された値を現在のコンテキストに追加し、新しいコンテキストを返します。
title: IDebugMemoryContext2::Add | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Add
helpviewer_keywords:
- IDebugMemoryContext2::Add method
- Add method
ms.assetid: 3c47e646-ce9e-4dd3-8f1a-6dbd3827d407
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 48847a65a1c5b6f514a96e702b9d8e666ad09630
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076798"
---
# <a name="idebugmemorycontext2add"></a>IDebugMemoryContext2::Add
指定された値を現在のコンテキストに追加し、新しいコンテキストを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Add( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Add(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>パラメーター
`dwCount`\
[in] 現在のコンテキストに追加する値。

`ppMemCxt`\
[out] 新しい [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 メモリ コンテキストはアドレスであるため、アドレスに値を追加すると、新しいコンテキスト インターフェイスを必要とする新しいアドレスが生成されます。

 このメソッドにより、結果のアドレスがこのコンテキストに関連付けられたメモリ領域外にある場合でも、常に新しいコンテキストを生成する必要があります。 唯一の例外は、新しいコンテキストにメモリを割り当てることができない場合、または `ppMemCxt` が null 値 (エラー) である場合です。

## <a name="see-also"></a>関連項目
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
