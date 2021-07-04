---
title: 制御イベント | Microsoft Docs
description: IDebugEvent2 インターフェイスを使用して、プログラムの制御された実行中にイベントを送信する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 0fc63484-5fb6-4887-9ea4-1905b459ca9d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb7249ece3ab38ff6f378f3c48ce36a995677604
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905697"
---
# <a name="control-events"></a>制御イベント
プログラムの制御された実行中にイベントを送信する必要があります。 それらのすべてのイベントは、[IDebugEvent2](../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを使用して送信され、[IDebugEvent2::GetAttributes](../../extensibility/debugger/reference/idebugevent2-getattributes.md) メソッドの実装を必要とする属性を持っています。

## <a name="additional-methods"></a>他の方法
 一部のイベントでは、次のように追加のメソッドを実装する必要があります。

- デバッグ エンジン (DE) の初期化時に [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) インターフェイスを送信するには、[IDebugEngineCreateEvent2::GetEngine](../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md) メソッドを実装する必要があります。

- 実行制御では、[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md) および [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) インターフェイスなどの制御イベントを実装する必要があります。 **IDebugBreakEvent2** は、非同期の中断の場合にのみ必要となります。

- 関数にステップインするには、[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) インターフェイスとそのメソッドを実装する必要があります。

  ブレークポイントから派生するイベントでは、[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)、[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)、[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) の各インターフェイスと、[IDebugBreakpointBoundEvent2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) および [EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) メソッドを実装する必要があります。

  非同期の式の評価では、[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) インターフェイスとその [IDebugExpressionEvaluationCompleteEvent2::GetExpression](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md) および [GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) メソッドを実装する必要があります。

  同期イベントでは、[IDebugEngine2::ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) メソッドを実装する必要があります。

  エンジンで文字列形式の出力を書き込む場合は、[IDebugOutputStringEvent2::GetString](../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md) メソッドを実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
