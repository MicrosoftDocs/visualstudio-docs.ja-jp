---
description: このメソッドでは、指定された数の IDebugObject 要素をスキップします。
title: IEnumDebugObjects::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects::Skip
helpviewer_keywords:
- IEnumDebugObjects::Skip method
ms.assetid: 957cead8-0a9c-4403-b190-b9fbadc49d42
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 381be32c6c13b995096374ea75b9603768bf1344
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052854"
---
# <a name="ienumdebugobjectsskip"></a>IEnumDebugObjects::Skip
このメソッドでは、指定された数の要素をスキップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Skip(
   [in] ULONG celt
);
```

```csharp
int Skip(
   [In] uint celt
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
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
