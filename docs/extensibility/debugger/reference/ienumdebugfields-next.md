---
description: このメソッドは、フィールド列挙型から次の要素セットを返します。
title: IEnumDebugFields::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Next
helpviewer_keywords:
- IEnumDebugFields::Next method
ms.assetid: 22c177a2-af81-4234-812b-f9b47be245a2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6b1705c1f07ce17df0d09c8b3036c639b6fe829a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073470"
---
# <a name="ienumdebugfieldsnext"></a>IEnumDebugFields::Next
このメソッドは、列挙型から次の要素セットを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG         celt,
   IDebugField** rgelt,
   ULONG*        pceltFetched
);
```

```csharp
int Next(
   uint          celt,
   IDebugField[] rgelt,
   ref uint      pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[入力] 取得する要素の数。 `rgelt` 配列の最大サイズも指定します。

`rgelt`\
[入力、出力] 入力された [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 要素の配列。

`pceltFetched`\
[出力] `rgelt` に実際に返された要素の数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返すことができた要素の数が要求された数よりも少なかった場合は `S_FALSE`、それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
