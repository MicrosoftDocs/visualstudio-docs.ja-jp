---
title: IDebugEventCallback2::Event |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2::Event
helpviewer_keywords:
- IDebugEventCallback2::Event
ms.assetid: e5a3345b-d460-4e40-8f5b-3111c56a2ed9
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a947f473fe7dc1fcf3e7b5b2b96d13edc3098218
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66201146"
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
[in][IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)は、このイベントを送信するデバッグ エンジン (DE) を表すオブジェクト。 このパラメーターの入力を DE が必要です。

`pProcess`\
[in][IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)イベントが発生するプロセスを表すオブジェクト。 このパラメーターは、セッション デバッグ マネージャー (SDM) によって入力されます。 常に、DE には、このパラメーターに null 値が渡されます。

`pProgram`\
[in][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)このイベントが発生するプログラムを表すオブジェクト。 ほとんどのイベントでは、このパラメーターは null 値ではありません。

`pThread`\
[in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)がこのイベントが発生したスレッドを表すオブジェクト。 イベントを停止するには、このパラメーターはスタック フレームがこのパラメーターから得られると、null 値をすることはできません。

`pEvent`\
[in][IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)デバッグ イベントを表すオブジェクト。

`riidEvent`\
[in]取得するには、どのイベント インターフェイスを識別する GUID、`pEvent`パラメーター。

`dwAttrib`\
[in]フラグの組み合わせ、[複数](../../../extensibility/debugger/reference/eventattributes.md)列挙体。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを呼び出すときに、`dwAttrib`パラメーターはから返される値と一致する必要があります、 [GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)渡されたメソッド、イベント オブジェクトに対して呼び出されると、`pEvent`パラメーター。

 すべてのデバッグ イベントがイベント自体が非同期かどうかに関係なく、非同期的に表示されます。 DE、このメソッドを呼び出すと、戻り値は示しませんイベントが処理されたかどうか、イベントを受信したかどうか。 実際、ほとんどの状況では、イベントが処理されていませんこのメソッドが戻るとき。

## <a name="see-also"></a>関連項目
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)