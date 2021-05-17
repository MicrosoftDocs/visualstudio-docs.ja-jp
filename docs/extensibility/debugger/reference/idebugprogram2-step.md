---
description: ステップを実行します。
title: IDebugProgram2::Step | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Step
helpviewer_keywords:
- IDebugProgram2::Step
ms.assetid: e4c2ffce-9810-4088-8162-eac9ef04f2a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2470c62215c8c708056f7c123adc5eac3a5e389d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084494"
---
# <a name="idebugprogram2step"></a>IDebugProgram2::Step
ステップを実行します。

> [!NOTE]
> このメソッドは非推奨とされます。 代わりに [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md) メソッドを使用してください。

## <a name="syntax"></a>構文

```cpp
HRESULT Step( 
   IDebugThread2*  pThread,
   STEPKIND        sk,
   STEPUNIT        step
);
```

```csharp
int Step( 
   IDebugThread2  pThread,
   enum_STEPKIND  sk,
   enum_STEPUNIT  step
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
[入力] ステップ実行されるスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

`sk`\
[入力] ステップの種類を指定する [STEPKIND](../../../extensibility/debugger/reference/stepkind.md) 列挙型の値。

`step`\
[入力] ステップの単位 (ステートメントや命令など) を指定する [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md) 列挙型の値。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 スレッドの同期またはスレッド間の通信がある場合、プログラムの他のスレッドは、特定のスレッドのステップ実行時に実行されます。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。送信した場合、デバッガーが応答しなくなる可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
