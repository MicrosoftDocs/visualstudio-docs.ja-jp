---
description: このメソッドでは、解析された式を評価し、必要に応じて結果を別のデータ型にキャストします。
title: IDebugParsedExpression::EvaluateSync | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 75f86506ea3cd29d09bf8c78a07eaabcf7a9a6f0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084637"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
このメソッドでは、解析された式を評価し、必要に応じて結果を別のデータ型にキャストします。

## <a name="syntax"></a>構文

```cpp
HRESULT EvaluateSync( 
   DWORD                 dwEvalFlags,
   DWORD                 dwTimeout,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   BSTR                  bstrResultType,
   IDebugProperty2**     ppResult
);
```

```csharp
int EvaluateSync(
   uint                 dwEvalFlags,
   uint                 dwTimeout,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   string               bstrResultType,
   out IDebugProperty2  ppResult
);
```

## <a name="parameters"></a>パラメーター
`dwEvalFlags`\
[入力] 式の評価方法を制御する [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 定数の組み合わせ。

`dwTimeout`\
[入力] このメソッドから戻る前に待機する最大時間 (ミリ秒単位) を指定します。 待機時間を指定しない場合は `INFINITE` を使用します。

`pSymbolProvider`\
[入力] [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイスとして表されたシンボル プロバイダー。

`pAddress`\
[入力] [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスとして表された、メソッド内の現在の実行位置。

`pBinder`\
[入力] [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) インターフェイスとして表されたバインダー。

`bstrResultType`\
[入力] 結果をキャストする型。 この引数には null 値を指定できます。

`ppResult`\
[出力] 評価の結果を表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 式の評価コンテキストは、`pAddress` によって指定されます。これにより、含まれているメソッドを判別し、言語のスコープ ルールを使用して、式のシンボルの値を判別できます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
