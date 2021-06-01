---
description: ブレークポイントのバインドが解除された理由を示します。
title: BP_UNBOUND_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13f723c6395b8b271d6f097d811c5a31569c5853
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067700"
---
# <a name="bp_unbound_reason"></a>BP_UNBOUND_REASON
ブレークポイントのバインドが解除された理由を示します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
typedef DWORD BP_UNBOUND_REASON;
```

```csharp
public enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
```

## <a name="fields"></a>フィールド
`BPUR_UNKNOWN`\
理由は不明です。

`BPUR_CODE_UNLOADED`\
このブレークポイントを含むコードがアンロードされました。

`BPUR_BREAKPOINT_REBIND`\
このブレークポイントは別の場所に再バインドされました。 これは、編集および続行操作の後、ブレークポイントが移動したときや、パスが有効でなくなったファイルにブレークポイントがバインドされているときに発生する可能性があります。

`BPUR_ BREAKPOINT_ERROR`\
このブレークポイントは、バインドされた後、エラーと判定されました。 これは、条件が有効でなくなったマネージド ブレークポイントに発生します。

## <a name="remarks"></a>解説
[GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md) メソッドから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)
