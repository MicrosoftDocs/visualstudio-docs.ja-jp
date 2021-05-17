---
description: このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべて保持され、プロセスの実行が再度開始されます。
title: IDebugProcess3::Continue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 11f2d5b652b950976834b8ba18f71a1dc0d1b34c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081582"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
このプロセスの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべて保持され、プロセスの実行が再度開始されます。

> [!NOTE]
> このメソッドは、[Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) の代わりに使用する必要があります。

## <a name="syntax"></a>構文

```cpp
HRESULT Continue(
   IDebugThread2* pThread
);
```

```csharp
int Continue(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
[入力] 続行するスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、デバッグされているプロセスの数や停止イベントを生成したプロセスに関係なく、このプロセスで呼び出されます。 実装では、前の実行状態 (ステップなど) が保持され、以前の実行を完了するまで停止していなかったかのように実行が継続される必要があります。 つまり、このプロセスのスレッドでステップオーバー操作を実行していて、他のプロセスが停止したために停止された場合、`Continue` が呼び出されると、指定されたスレッドで元のステップオーバー操作を完了する必要があります。

 **警告** この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。そうしないと、デバッガーが応答しなくなる可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
