---
description: 保留中のブレークポイントとバインドされたブレークポイントのブレークポイント条件スタイルを指定します。
title: BP_COND_STYLE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 611df036ff876e10096013070cac097bc51a8986
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085417"
---
# <a name="bp_cond_style"></a>BP_COND_STYLE
保留中のブレークポイントとバインドされたブレークポイントのブレークポイント条件スタイルを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
typedef DWORD BP_COND_STYLE;
```

```csharp
public enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
```

## <a name="fields"></a>フィールド
`BP_COND_NONE`\
ブレークポイントの位置に達したときにブレークポイントを発生させます。 ブレークポイント条件は指定されていません。

`BP_COND_WHEN_TRUE`\
ブレークポイントに関連付けられている条件式が `true` と評価された場合にのみ、ブレークポイントを発生させます。

`BP_COND_WHEN_CHANGED`\
ブレークポイントに関連付けられている条件式の値が以前の評価から変化した場合にのみ、ブレークポイントを発生させます。

## <a name="remarks"></a>解説
[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 構造体の `styleCondition` メンバーに使用されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
