---
title: IDebugExpressionEvaluationCompleteEvent2::GetResult |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluationCompleteEvent2::GetResult
helpviewer_keywords:
- IDebugExpressionEvaluationCompleteEvent2::GetResult
ms.assetid: d9ad3e22-b6b2-421e-9a43-6bb8c70d12a9
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a7ceb20932a0d41486675a8bf1928831726856cb
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66200940"
---
# <a name="idebugexpressionevaluationcompleteevent2getresult"></a>IDebugExpressionEvaluationCompleteEvent2::GetResult
式の評価の結果を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetResult( 
   IDebugProperty2** ppResult
);
```

```csharp
int GetResult( 
   out IDebugProperty2 ppResult
);
```

## <a name="parameters"></a>パラメーター
`ppResult` [out]返します、 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)式の評価の結果を表すオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 返された[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトには、評価された式の値が含まれています。 この値は、配列など複雑な値である可能性がありますが、最終的な結果する必要がありますが、数値または文字列をユーザーに表示される値に注意してください。

## <a name="see-also"></a>関連項目
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)