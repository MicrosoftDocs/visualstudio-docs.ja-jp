---
description: このインターフェイスは、バインドと評価の準備ができている解析済みの式を表します。
title: IDebugExpression2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2
helpviewer_keywords:
- IDebugExpression2 interface
ms.assetid: f5e4b124-1e30-47c8-a511-80084a02dba5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 934cef3dfd95b0aeadd588889dad020687d1cfd7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092333"
---
# <a name="idebugexpression2"></a>IDebugExpression2
このインターフェイスは、バインドと評価の準備ができている解析済みの式を表します。

## <a name="syntax"></a>構文

```
IDebugExpression2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) は、評価の準備ができている解析済みの式を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) の呼び出しで、このインターフェイスが返されます。 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) は、[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを返します。 これらのインターフェイスには、デバッグ中のプログラムが一時停止されていて、スタック フレームが使用可能な場合にのみアクセスできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugExpression2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|この式を非同期的に評価します。|
|[中止](../../../extensibility/debugger/reference/idebugexpression2-abort.md)|非同期の式の評価を終了します。|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|この式を同期的に評価します。|

## <a name="remarks"></a>解説
 プログラムが停止されると、セッション デバッグ マネージャー (SDM) は、[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) の呼び出しによって DE からスタック フレームを取得します。 次に、SDM は [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを取得します。 この後に [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) の呼び出しで、評価の準備ができている解析済みの式を表す `IDebugExpression2` インターフェイスを作成します。

 SDM は、式を実際に評価して値を生成するために、[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) を呼び出します。

 `IDebugExpressionContext2::ParseText` の実装では、DE は COM の `CoCreateInstance` 関数を使用して式エバリュエーターをインスタンス化し、[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) インターフェイスを取得します (`IDebugExpressionEvaluator` インターフェイスの「例」を参照)。 次に、DE は [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) を呼び出して、[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) インターフェイスを取得します。 このインターフェイスは、評価を実行するために `IDebugExpression2::EvaluateSync` および `IDebugExpression2::EvaluateAsync` の実装で使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)
