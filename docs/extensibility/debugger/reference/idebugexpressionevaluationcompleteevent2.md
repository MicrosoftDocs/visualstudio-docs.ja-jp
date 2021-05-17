---
description: このインターフェイスは、非同期の式の評価が完了したときに、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugExpressionEvaluationCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluationCompleteEvent2
helpviewer_keywords:
- IDebugExpressionEvaluationCompleteEvent2
ms.assetid: d538fc19-55bf-4231-9595-eb01e84fd1d8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b30b61c0b7a9a9f3e06465a6b194c882213afb34
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092203"
---
# <a name="idebugexpressionevaluationcompleteevent2"></a>IDebugExpressionEvaluationCompleteEvent2
このインターフェイスは、非同期の式の評価が完了したときに、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugExpressionEvaluationCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) の呼び出しによって開始された式の評価の完了を報告するために、このインターフェイスを実装します。 このインターフェイスと同じオブジェクトに、[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、式の評価の完了を報告するために、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugExpressionEvaluationCompleteEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)|元の式を取得します。|
|[GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)|式の評価結果を取得します。|

## <a name="remarks"></a>解説
 DE は、評価が成功したかどうかにかかわらず、このイベントを送信する必要があります。

 評価が成功しなかった場合、`DEBUG_PROPINFO_VALUE` および `DEBUG_PROPINFO_ATTRIB` フラグは、[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) によって返される [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体では設定されません ([IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトは DE によって作成され、評価が失敗した場合は `IDebugExpressionEvaluationCompleteEvent2` イベントで返されます)。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
