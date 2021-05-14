---
description: バインドされたブレークポイントの列挙型の要素を指定した数スキップします。
title: IEnumDebugBoundBreakpoints2::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2::Skip
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2::Skip
ms.assetid: 95659709-6d7c-44ca-b598-629eb688429f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c9af4f8568a2f743aa62280db1f8ce9015e9f694
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061681"
---
# <a name="ienumdebugboundbreakpoints2skip"></a>IEnumDebugBoundBreakpoints2::Skip
指定した数の要素をスキップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[入力] スキップする要素の数。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 `celt` が残りの要素の数より大きい場合は `S_FALSE` を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 `celt` が、残りの要素の数よりも大きい場合、列挙型は終わりに設定され、`S_FALSE` が返されます。

## <a name="see-also"></a>関連項目
- [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)
