---
description: イベント属性を指定します。
title: EVENTATTRIBUTES | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 922c60c0bb36c58b88c2422580eeda0db1c02d42
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059484"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
イベント属性を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
typedef DWORD EVENTATTRIBUTES;
```

```csharp
public enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
```

## <a name="fields"></a>フィールド
`EVENT_ASYNCHRONOUS`\
イベントが非同期であり、イベントへの応答を必要としないことを示します。

`EVENT_SYNCHRONOUS`\
イベントが同期であることを示します。[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) を通じて応答します。

`EVENT_STOPPING`\
これが停止イベントであることを示します。 は、`EVENT_ASYNCHRONOUS` または `EVENT_SYNCHRONOUS` のいずれかと組み合わせる必要があります。

`EVENT_ASYNC_STOP`\
非同期の停止イベントを示します。 現在、このようなイベントはありません。 このフラグは単なるプレースホルダーです。

`EVENT_SYNC_STOP`\
同期停止イベント (`EVENT_SYNCHRONOUS` と `EVENT_STOPPING` の組み合わせ) を示します。 この値は、デバッグ エンジン (DE) によって停止イベントが送信されるときに使用されます。 応答は、[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)、または [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) を呼び出すことによって行われます。

`EVENT_IMMEDIATE`\
すぐに、IDE に同期的に送信されるイベントを示します。 このフラグは `EVENT_ASYNCHRONOUS`、`EVENT_SYNCHRONOUS`、`EVENT_SYNC_STOP` などの他のフラグと組み合わせて、イベントの種類と、応答機構 (存在する場合) がわかっていることを示します。

`EVENT_EXPRESSION_EVALUATION`\
イベントは、式の評価の結果です。

## <a name="remarks"></a>解説
これらの値は、[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) メソッドの `dwAttrib` パラメーターで渡されます。

これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
