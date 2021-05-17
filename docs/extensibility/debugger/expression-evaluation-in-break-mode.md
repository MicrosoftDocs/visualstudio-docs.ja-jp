---
title: 中断モードでの式の評価 | Microsoft Docs
description: デバッガーが中断モードであり、式の評価を実行する必要がある場合に発生するプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 932bebecf4eea73cfae579bbea58e024b4388ffb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067869"
---
# <a name="expression-evaluation-in-break-mode"></a>中断モードでの式の評価
次のセクションでは、デバッガーが中断モードであり、式の評価を実行する必要がある場合に発生するプロセスについて説明します。

## <a name="expression-evaluation-process"></a>式の評価のプロセス
 式の評価に関係する基本的な手順は次のとおりです。

1. セッション デバッグ マネージャー (SDM) で [IDebugStackFrame2::GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、式コンテキスト インターフェイス [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) を取得します。

2. 次に SDM は、解析する文字列を指定して [IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) を呼び出します。

3. ParseText が S_OK を返さない場合、エラーの理由が返されます。

     -それ以外の場合-

     ParseText が S_OK を返す場合、SDM は [IDebugExpression2::EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) のいずれかを呼び出して、解析された式から最終的な値を取得できます。

    - `IDebugExpression2::EvaluateSync` を使用する場合、指定されたコールバック インターフェイスは、評価の進行中のプロセスを伝達します。 最終的な値は、[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスで返されます。

    - `IDebugExpression2::EvaluateAsync` を使用する場合、指定されたコールバック インターフェイスは、評価の進行中のプロセスを伝達します。 評価が完了すると、EvaluateAsync はコールバックを通じて [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) インターフェイスを送信します。 このイベント インターフェイスの [GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) を使用した結果が、最終的な値です。

## <a name="see-also"></a>関連項目
- [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
