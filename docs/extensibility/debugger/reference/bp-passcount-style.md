---
description: ブレークポイントが発生する原因となる、ブレークポイントのパス カウントに関連付けられた条件を指定します。
title: BP_PASSCOUNT_STYLE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT_STYLE
helpviewer_keywords:
- BP_PASSCOUNT_STYLE structure
ms.assetid: 0a647047-e2d5-4724-a0b8-68108425ecad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39a0dba08aa74386c442a7732b6522d8ee27652c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094472"
---
# <a name="bp_passcount_style"></a>BP_PASSCOUNT_STYLE
ブレークポイントが発生する原因となる、ブレークポイントのパス カウントに関連付けられた条件を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
typedef DWORD BP_PASSCOUNT_STYLE;
```

```csharp
public enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
```

## <a name="fields"></a>フィールド
`BP_PASSCOUNT_NONE`\
ブレークポイントのパス カウントのスタイルを指定しません。

`BP_PASSCOUNT_EQUAL`\
ブレークポイントのパス カウントのスタイルを等しくなるように設定します。 ブレークポイントは、ブレークポイントがヒットした回数がパス カウントと等しいときに発生します。

`BP_PASSCOUNT_EQUAL_OR_GREATER`\
ブレークポイントのパス カウントのスタイルを、等しいかより大きくなるように設定します。 ブレークポイントがヒットした回数が、パス カウント以上になると、ブレークポイントが発生します。

`BP_PASSCOUNT_MOD`\
剰余パス カウントを指定します。 たとえば、パス カウントの型が `BP_PASSCOUNT_MOD` で、パス カウント値が 4 の場合、ヒット カウントが 4 の倍数になるたびにブレークポイントが発生します。

## <a name="remarks"></a>解説
次に [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) および [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体のメンバーになる、[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 構造体の `stylePassCount` メンバーに使用されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
