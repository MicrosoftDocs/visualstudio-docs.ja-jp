---
title: IDebugParsedExpression::EvaluateSync |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ea659b847149a6abb2c3a5ba7cc947a59c7ae41c
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56709643"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
このメソッドは、解析された式を評価し、必要に応じて別のデータ型に結果をキャストします。

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

#### <a name="parameters"></a>パラメーター
 `dwEvalFlags`

 [in]組み合わせた[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)式を評価する方法を制御する定数。

 `dwTimeout`

 [in]このメソッドから戻る前に待機するミリ秒単位で最大の時間を指定します。 使用`INFINITE`を無期限に待機します。

 `pSymbolProvider`

 [in]として表現される、シンボル プロバイダー、 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)インターフェイス。

 `pAddress`

 [in]表されるメソッド内の現在の実行場所、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイス。

 `pBinder`

 [in]表される、バインダー、 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)インターフェイス。

 `bstrResultType`

 [in]結果の型にキャストする必要があります。 この引数は、null 値を指定できます。

 `ppResult`

 [out]返します、 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)評価の結果を表すインターフェイスです。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 式の評価コンテキストがで指定された`pAddress`格納方法を決定できるように、式内のシンボルの値を決定するルールの言語のスコープを使用します。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)