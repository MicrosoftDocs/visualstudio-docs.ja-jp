---
description: このメソッドにより、アドレス列挙体から次の要素セットが返されます。
title: IEnumDebugAddresses::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Next
helpviewer_keywords:
- IEnumDebugAddresses::Next method
ms.assetid: 941e4be7-858d-433a-9259-18d0d017be9e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 570fbcb49e4e96fce558c5981eb590ae33e0f0a6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083181"
---
# <a name="ienumdebugaddressesnext"></a>IEnumDebugAddresses::Next
このメソッドにより、列挙体から次の要素セットが返されます。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG           celt,
   IDebugAddress** rgelt,
   ULONG*          pceltFetched
);
```

```csharp
int Next(
   uint            celt,
   IDebugAddress[] rgelt,
   ref uint        pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in] 取得する要素の数。 `rgelt` 配列の最大サイズも指定します。

`rgelt`\
[in, out] 入力される [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 要素の配列。

`pceltFetched`\
[out] `rgelt` で実際に返された要素の数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返すことができた要素の数が要求された数よりも少なかった場合は、`S_FALSE` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
