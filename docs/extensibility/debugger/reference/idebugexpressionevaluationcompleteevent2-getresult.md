---
description: 式の評価の結果を取得します。
title: 'IDebugExpressionEvaluationCompleteEvent2:: GetResult |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluationCompleteEvent2::GetResult
helpviewer_keywords:
- IDebugExpressionEvaluationCompleteEvent2::GetResult
ms.assetid: d9ad3e22-b6b2-421e-9a43-6bb8c70d12a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f1aaf150f3502490f7580866ac99a9fc16197dde
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092242"
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
`ppResult` 入出力式の評価結果を表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 返された [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトには、評価された式の値が含まれます。 この値は、配列などの複雑な値である可能性がありますが、最終的な結果はユーザーに表示される数値または文字列値である必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
