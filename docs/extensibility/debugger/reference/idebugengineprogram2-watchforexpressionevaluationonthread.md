---
description: プログラムが停止している場合でも、指定されたスレッドでの式の評価の実行を許可します (または許可しません)。
title: IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
helpviewer_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
ms.assetid: 01d05e77-8cac-4d1b-b19f-25756767ed27
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 820babb655f04da40fdd44aae55f963539e5ffa8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093861"
---
# <a name="idebugengineprogram2watchforexpressionevaluationonthread"></a>IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
プログラムが停止している場合でも、指定されたスレッドでの式の評価の実行を許可します (または許可しません)。

## <a name="syntax"></a>構文

```cpp
HRESULT WatchForExpressionEvaluationOnThread( 
   IDebugProgram2*       pOriginatingProgram,
   DWORD                 dwTid,
   DWORD                 dwEvalFlags,
   IDebugEventCallback2* pExprCallback,
   BOOL                  fWatch
);
```

```csharp
int WatchForExpressionEvaluationOnThread( 
   IDebugProgram2       pOriginatingProgram,
   uint                  dwTid,
   uint                  dwEvalFlags,
   IDebugEventCallback2 pExprCallback,
   int                   fWatch
);
```

## <a name="parameters"></a>パラメーター
`pOriginatingProgram`\
[入力] 式を評価しているプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`dwTid`\
[入力] スレッドの識別子を指定します。

`dwEvalFlags`\
[入力] 評価の実行方法を指定する [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 列挙型のフラグの組み合わせ。

`pExprCallback`\
[入力] 式の評価中に発生するデバッグ イベントを送信するために使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`fWatch`\
[入力] ゼロ以外 (`TRUE`) の場合、`dwTid` で識別されるスレッドで式の評価を許可します。それ以外の場合、ゼロ (`FALSE`) はそのスレッドで式の評価を許可しません。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 セッション デバッグ マネージャー (SDM) は、`pOriginatingProgram` パラメーターで識別されるプログラムに式を評価するよう要求するときに、このメソッドを呼び出すことによって、アタッチされている他のすべてのプログラムに通知します。

 関数の評価や `IDispatch` プロパティの評価のためにて、1 つのプログラムでの式の評価により、コードが別のプログラムで実行される場合があります。 このため、このメソッドでは、このプログラムでスレッドが停止していても、式の評価を実行して完了することができます。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
