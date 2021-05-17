---
description: 2 つのドキュメント コンテキストを比較するための条件を指定します。
title: DOCCONTEXT_COMPARE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6eeee3e31c898660930b676df716fe25769bbb8b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096006"
---
# <a name="doccontext_compare"></a>DOCCONTEXT_COMPARE
2 つのドキュメント コンテキストを比較するための条件を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
typedef DWORD DOCCONTEXT_COMPARE;
```

```csharp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
```

## <a name="fields"></a>フィールド
`DOCCONTEXT_EQUAL`\
リスト内でターゲット ドキュメント コンテキストと等しい最初のドキュメント コンテキストを検索します。

`DOCCONTEXT_LESS_THAN`\
リスト内でターゲット ドキュメント コンテキストより小さい最初のドキュメント コンテキストを検索します。

`DOCCONTEXT_GREATER_THAN`\
リスト内でターゲット ドキュメント コンテキストより大きい最初のドキュメント コンテキストを検索します。

`DOCCONTEXT_SAME_DOCUMENT`\
リスト内で、ターゲット ドキュメント コンテキストと同じドキュメント内にある最初のドキュメント コンテキストを検索します。

## <a name="remarks"></a>解説
[Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md) メソッドに引数として渡されます。

これらの値は、リスト内の最初のドキュメント コンテキストを検索するための比較条件を指定するために使用されます。 ドキュメント コンテキストには、`IDebugDocumentContext2::Compare` メソッドを通じて、それ自体を比較するドキュメント コンテキストのリストが与えられ ます。 比較演算子が `true` であるリスト内の最初のドキュメント コンテキストが返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比較](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)
