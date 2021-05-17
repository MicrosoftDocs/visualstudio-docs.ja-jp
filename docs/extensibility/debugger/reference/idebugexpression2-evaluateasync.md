---
description: このメソッドは、式を非同期的に評価します。
title: IDebugExpression2::EvaluateAsync | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateAsync
helpviewer_keywords:
- IDebugExpression2::EvaluateAsync
ms.assetid: 848fe6cb-0759-42f2-890b-d2b551c527d6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bea7a5a05dc5277e693d033452f0b4e7342ea946
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092424"
---
# <a name="idebugexpression2evaluateasync"></a>IDebugExpression2::EvaluateAsync
このメソッドは、式を非同期的に評価します。

## <a name="syntax"></a>構文

```cpp
HRESULT EvaluateAsync (
    EVALFLAGS             dwFlags,
    IDebugEventCallback2* pExprCallback
);
```

```csharp
int EvaluateAsync(
    enum_EVALFLAGS       dwFlags,
    IDebugEventCallback2 pExprCallback
);
```

## <a name="parameters"></a>パラメーター
`dwFlags`\
[入力] 式の評価を制御する [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 列挙型のフラグの組み合わせ。

`pExprCallback`\
[入力] このパラメーターは常に null 値です。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 一般的なエラー コードは次のとおりです。

|エラー|説明|
|-----------|-----------------|
|E_EVALUATE_BUSY_WITH_EVALUATION|現在、別の式が評価中であり、式の同時評価はサポートされていません。|

## <a name="remarks"></a>解説
このメソッドは、式の評価を開始した直後に返される必要があります。 式が正常に評価された場合は、[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md) または [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) によって指定される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) イベント コールバックに [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) を送信する必要があります。

## <a name="example"></a>例
次の例は、[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスを実装する単純な `CExpression` オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
HRESULT CExpression::EvaluateAsync(EVALFLAGS dwFlags,
                                   IDebugEventCallback2* pExprCallback)
{
    // Set the aborted state to FALSE
    // in case the user tries to redo the evaluation after aborting.
    m_bAborted = FALSE;
    // Post the WM_EVAL_EXPR message in the message queue of the current thread.
    // This starts the expression evaluation on a background thread.
    PostThreadMessage(GetCurrentThreadId(), WM_EVAL_EXPR, 0, (LPARAM) this);
    return S_OK;
}
```

## <a name="see-also"></a>関連項目
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
