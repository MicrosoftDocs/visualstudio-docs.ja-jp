---
description: 2 つのメモリ コンテキストを比較するための条件を指定します。
title: CONTEXT_COMPARE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd74516c3f687f05b2d5fb33dc2b94455114bbc6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094446"
---
# <a name="context_compare"></a>CONTEXT_COMPARE
2 つのメモリ コンテキストを比較するための条件を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
typedef DWORD CONTEXT_COMPARE;
```

```csharp
public enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
```

## <a name="fields"></a>フィールド
`CONTEXT_EQUAL`\
リスト内でターゲットのメモリ コンテキストに等しい最初のメモリ コンテキストを検索します。

`CONTEXT_LESS_THAN`\
リスト内でターゲットのメモリ コンテキストより小さい最初のメモリ コンテキストを検索します。

`CONTEXT_GREATER_THAN`\
リスト内でターゲットのメモリ コンテキストより大きい最初のメモリ コンテキストを検索します。

`CONTEXT_LESS_THAN_OR_EQUAL`\
リスト内でターゲットのメモリ コンテキストより小さいか等しい最初のメモリ コンテキストを検索します。

`CONTEXT_GREATER_THAN_OR_EQUAL`\
リスト内でターゲットメモリ コンテキストより大きいか等しい最初のメモリ コンテキストを検索します。

`CONTEXT_SAME_SCOPE`\
リスト内でターゲットのメモリ コンテキストと同じスコープ内にある最初のメモリ コンテキストを検索します。

`CONTEXT_SAME_FUNCTION`\
リスト内で、ターゲットのメモリスコープと同じ関数内にある最初のメモリ コンテキストを検索します。

`CONTEXT_SAME_MODULE`\
リスト内でターゲットのメモリ コンテキストと同じモジュール内にある最初のメモリ コンテキストを検索します。

`CONTEXT_SAME_PROCESS`\
リスト内でターゲットのメモリ コンテキストと同じプロセス内にある最初のメモリ コンテキストを検索します。

## <a name="remarks"></a>解説
[Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md) メソッドに引数として渡されます。

これらの値は、指定された比較条件を満たす、リスト内の最初のメモリ コンテキストを検索するために使用されます。 メモリ コンテキストには、`IDebugMemoryContext2::Compare` メソッドを通じて、それ自体を比較するメモリ コンテキストのリストが与えられます。 比較演算子が `true` であるリスト内の最初のメモリ コンテキストが返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比較](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)
