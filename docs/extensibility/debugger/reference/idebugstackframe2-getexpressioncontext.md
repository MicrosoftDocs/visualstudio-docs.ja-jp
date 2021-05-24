---
description: スタック フレームとスレッドの現在のコンテキスト内の式の評価に対する評価コンテキストを取得します。
title: IDebugStackFrame2::GetExpressionContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetExpressionContext
helpviewer_keywords:
- IDebugStackFrame2::GetExpressionContext
ms.assetid: a2604e6a-502d-473b-868f-b11ac64c7a35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4da07b438ca35417de025a0d9ec6c2dfa01f464d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053439"
---
# <a name="idebugstackframe2getexpressioncontext"></a>IDebugStackFrame2::GetExpressionContext
スタック フレームとスレッドの現在のコンテキスト内の式の評価に対する評価コンテキストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExpressionContext ( 
   IDebugExpressionContext2** ppExprCxt
);
```

```csharp
int GetExpressionContext ( 
   out IDebugExpressionContext2 ppExprCxt
);
```

## <a name="parameters"></a>パラメーター
`ppExprCxt`\
[out] 式の評価のコンテキストを表す [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 一般に、式の評価のコンテキストは、式の評価を実行するためのスコープと考えることができます。 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを呼び出して式を解析した後、結果の [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) メソッドを呼び出して、解析された式を評価します。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
