---
description: デバッグ イベントの通知を送信します。
title: IDebugEventCallback2::Event | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2::Event
helpviewer_keywords:
- IDebugEventCallback2::Event
ms.assetid: e5a3345b-d460-4e40-8f5b-3111c56a2ed9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0fec6984ffc30c3c368193079fdabc1752f63a65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065802"
---
# <a name="idebugeventcallback2event"></a>IDebugEventCallback2::Event
デバッグ イベントの通知を送信します。

## <a name="syntax"></a>構文

```cpp
HRESULT Event( 
   IDebugEngine2*  pEngine,
   IDebugProcess2* pProcess,
   IDebugProgram2* pProgram,
   IDebugThread2*  pThread,
   IDebugEvent2*   pEvent,
   REFIID          riidEvent,
   DWORD           dwAttrib
);
```

```csharp
int Event( 
   IDebugEngine2  pEngine,
   IDebugProcess2 pProcess,
   IDebugProgram2 pProgram,
   IDebugThread2  pThread,
   IDebugEvent2   pEvent,
   ref Guid       riidEvent,
   uint           dwAttrib
);
```

## <a name="parameters"></a>パラメーター
`pEngine`\
[入力] このイベントを送信しているデバッグ エンジン (DE) を表す [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) オブジェクト。 このパラメーターを入力するには、DE が必要です。

`pProcess`\
[入力] イベントが発生するプロセスを表す [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) オブジェクト。 このパラメーターは、セッション デバッグ マネージャー (SDM) によって入力されます。 DE は、常にこのパラメーターに null 値を渡します。

`pProgram`\
[入力] このイベントが発生するプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。 ほとんどのイベントについて、このパラメーターは null 値ではありません。

`pThread`\
[入力] このイベントが発生するスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。 停止イベントについては、このパラメーターからスタック フレームが取得されるため、このパラメーターを null 値にすることはできません。

`pEvent`\
[入力] デバッグ イベントを表す [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) オブジェクト。

`riidEvent`\
[入力] `pEvent` パラメーターから取得するイベント インターフェイスを識別する GUID。

`dwAttrib`\
[入力] [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md) 列挙型のフラグの組み合わせ。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドを呼び出す場合、`dwAttrib` パラメーターは、`pEvent` パラメーターで渡されたイベント オブジェクトに対して [GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md) メソッドを呼び出したときの戻り値に一致する必要があります。

 イベント自体が非同期であるかどうかに関係なく、すべてのデバッグ イベントは非同期で POST されます。 DE でこのメソッドを呼び出すと、戻り値はイベントが処理されたかどうかは示さず、イベントが受信されたかどうかのみを示します。 実際、ほとんどの状況下で、このメソッドから制御が戻った時点ではイベントは処理されていません。

## <a name="see-also"></a>関連項目
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
