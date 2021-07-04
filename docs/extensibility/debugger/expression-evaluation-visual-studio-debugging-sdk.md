---
title: 式の評価 (Visual Studio Debugging SDK) | Microsoft Docs
description: 中断モード時に、IDE ではプログラム変数を含む式が評価されます。 デバッグ エンジンで式が解析および評価される方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf213c30ef26490b44579d83c68b2640360584a7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904514"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>式の評価 (Visual Studio Debugging SDK)
中断モード時に、IDE では複数のプログラム変数を含む単純な式を評価する必要があります。 その評価を行うには、デバッグ エンジン (DE) によって、IDE のいずれかのウィンドウに入力された式を解析して評価する必要があります。

 式は、[IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して作成され、結果の [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスによって表されます。

 **IDebugExpression2** インターフェイスは DE によって実装され、IDE で式の評価結果を表示するために、[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを IDE に返す **EvalAsync** メソッドを呼び出します。 [IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) では、式の値を **[ウォッチ]** ウィンドウまたは **[ローカル]** ウィンドウに配置するために使用される構造体が返されます。

 デバッグ パッケージまたはセッション デバッグ マネージャー (SDM) によって、[IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) または [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) が呼び出され、評価の結果を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスが取得されます。 `IDebugProperty2` には、式の名前、型、および値を返すメソッドがあります。 この情報は、さまざまなデバッガー ウィンドウに表示されます。

## <a name="using-expression-evaluation"></a>式の評価の使用
 式の評価を使用するには、次の表に示すように、[IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドと [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスのすべてのメソッドを実装する必要があります。

|メソッド|説明|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|式を非同期で評価します。|
|[中止](../../extensibility/debugger/reference/idebugexpression2-abort.md)|非同期の式の評価を終了します。|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|式を同期して評価します。|

 同期および非同期評価には、[IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドを実装する必要があります。 非同期の式の評価には、[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) の実装が必要です。

## <a name="see-also"></a>関連項目
- [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
