---
description: 条件付きのブレークポイントが発生する回数と条件を表します。
title: BP_PASSCOUNT | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT
helpviewer_keywords:
- BP_PASSCOUNT structure
ms.assetid: 791ac175-b897-4c70-873e-240da7e0ac89
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: afb94436897224bc9c6896a601447e9d9a1c8b6f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096734"
---
# <a name="bp_passcount"></a>BP_PASSCOUNT
条件付きのブレークポイントが発生する回数と条件を表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_PASSCOUNT {
    DWORD              dwPassCount;
    BP_PASSCOUNT_STYLE stylePassCount;
} BP_PASSCOUNT;
```

```csharp
public struct BP_PASSCOUNT {
    public uint dwPassCount;
    public uint stylePassCount;
};
```

## <a name="members"></a>メンバー
`dwPassCount`\
この回数だけブレークポイントを通過した後、ブレークポイントを発生させます。

`stylePassCount`\
[BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md) 列挙型からの、ブレークポイント通過カウントのスタイルを指定する値。

## <a name="remarks"></a>解説
この構造体は、[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造体に属します。

この構造体は、[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md) メソッドと [SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md) メソッドにもパラメーターとして渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)
- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)
