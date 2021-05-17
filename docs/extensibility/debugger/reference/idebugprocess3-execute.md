---
description: このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべてクリアされ、プロセスの実行が再度開始されます。
title: IDebugProcess3::Execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e81efa2bec718899dba01181ccc691040cd4cf2b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081595"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべてクリアされ、プロセスの実行が再度開始されます。

> [!NOTE]
> このメソッドは、[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md) の代わりに使用する必要があります。

## <a name="syntax"></a>構文

```cpp
HRESULT Execute(
   IDebugThread2* pThread
);
```

```csharp
int Execute(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
[入力] 実行するスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 ユーザーが他のプロセスのスレッドで停止状態から実行を開始すると、このメソッドがこのプロセスで呼び出されます。 このメソッドは、ユーザーが IDE の **[デバッグ]** メニューから **[開始]** コマンドを選択したときにも呼び出されます。 このメソッドの実装は、プロセスの現在のスレッドで [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) メソッドを呼び出す場合と同じように簡単に行うことができます。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。送信した場合、デバッガーが応答しなくなる可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [再開](../../../extensibility/debugger/reference/idebugthread2-resume.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
