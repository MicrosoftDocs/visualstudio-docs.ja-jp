---
description: IDebugProgram2::Continue では、このプログラムの実行を停止状態から続行します。 前の実行状態 (ステップなど) がすべて保持され、プログラムの実行が再度開始されます。
title: IDebugProgram2::Continue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Continue
helpviewer_keywords:
- IDebugProgram2::Continue
ms.assetid: e5a6e02a-d21b-4a03-a034-e8de1f71ce2e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60f3cb4764a53d359e971020df8261d064c62e81
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076122"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
停止された状態からこのプログラムの実行を続行します。 前の実行状態 (ステップなど) がすべて保持され、プログラムの実行が再度開始されます。

> [!NOTE]
> このメソッドは非推奨とされます。 代わりに [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) メソッドを使用してください。

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
`pThread` [入力] スレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、デバッグされているプログラムの数や停止イベントを生成したプログラムに関係なく、このプログラムで呼び出されます。 実装では、前の実行状態 (ステップなど) が保持され、以前の実行を完了するまで停止していなかったかのように実行が継続される必要があります。 つまり、このプログラムのスレッドでステップオーバー操作を実行していて、他のプログラムが停止したために停止された場合、このメソッドが呼び出されると、プログラムで元のステップオーバー操作を完了する必要があります。

> [!WARNING]
> この呼び出しの処理中に、停止イベントまたは即時 (同期) イベントを [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に送信しないでください。送信した場合、デバッガーが応答しなくなる可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
