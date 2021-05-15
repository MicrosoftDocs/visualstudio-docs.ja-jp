---
description: バインドされたブレークポイントが存在することを明示し、それが有効になっているかどうかも明示します。
title: BP_STATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_STATE
helpviewer_keywords:
- BP_STATE enumeration
ms.assetid: 08aa6a3f-3e5f-4c83-8eca-7b7b5f8e208d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 886469727e9a20802f375faac12abbdd0d2b1ff2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089109"
---
# <a name="bp_state"></a>BP_STATE
バインドされたブレークポイントが存在することを明示し、それが有効になっているかどうかも明示します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
typedef DWORD BP_STATE;
```

```csharp
public enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>フィールド
`BPS_NONE`\
ブレークポイントが存在しないことを明示します。

`BPS_DELETED`\
ブレークポイントが削除されたことを明示します。

`BPS_DISABLED`\
ブレークポイントが無効になっていることを明示します。

`BPS_ENABLED`\
ブレークポイントが有効になっていることを明示します。

## <a name="remarks"></a>解説
[GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md) メソッドから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)
