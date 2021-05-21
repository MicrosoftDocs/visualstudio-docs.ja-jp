---
description: このメソッドでは、アドレス列挙体内の指定された数の要素をスキップします。
title: IEnumDebugAddresses::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Skip
helpviewer_keywords:
- IEnumDebugAddresses::Skip method
ms.assetid: ed9a8e71-30ef-414b-9da5-c9a2a251b84e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 082cba541b1074e75e44384cd8ac9e4879cc29c3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083155"
---
# <a name="ienumdebugaddressesskip"></a>IEnumDebugAddresses::Skip
このメソッドでは、指定された数の要素をスキップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Skip(
   [in] ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in] スキップする要素の数。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 `celt` が残りの要素の数より大きい場合は、`S_FALSE` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 `celt` に残りの要素の数よりも大きい値を指定した場合、この列挙体は末尾に設定され、`S_FALSE` が返されます。

## <a name="see-also"></a>関連項目
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
