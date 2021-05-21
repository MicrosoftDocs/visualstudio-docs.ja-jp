---
description: 実行中、特定のポイントに到達後、プログラムでは実行を停止できるか判断する目的で使用されます。
title: CANSTOP_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CANSTOP_REASON
helpviewer_keywords:
- CANSTOP_REASON enumeration
ms.assetid: 6da944eb-36cd-4a8c-8d71-544c775cfcc1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39a22a0534a464e9899e666550b31ab24503c05d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096526"
---
# <a name="canstop_reason"></a>CANSTOP_REASON
実行中、特定のポイントに到達後、プログラムでは実行を停止できるか判断する目的で使用されます。

## <a name="syntax"></a>構文

```cpp
enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
typedef DWORD CANSTOP_REASON;
```

```csharp
public enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
```

## <a name="fields"></a>フィールド
`CANSTOP_ENTRYPOINT`\
指定のプログラムのエントリ ポイントを指定します。

`CANSTOP_STEPIN`\
関数のステップ インを指定します。

## <a name="remarks"></a>解説
プログラムのエントリ ポイントに到達後、あるいは関数またはメソッドのステップ イン後、停止しても問題ないか、セッション デバッグ マネージャー (SDM) に確認する目的で、[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) メソッドに引数として渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
