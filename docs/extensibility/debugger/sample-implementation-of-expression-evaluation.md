---
title: 式の評価の実装のサンプル | Microsoft Docs
description: Visual Studio が ParseText を呼び出して、ウォッチ ウィンドウ式の IDebugExpression2 オブジェクトを作成する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: sample
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: de0e052fd42f1603889f7521a1e45e50b0f36eea
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902307"
---
# <a name="sample-implementation-of-expression-evaluation"></a>式の評価の実装のサンプル
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 **ウォッチ** ウィンドウ式の場合、Visual Studio は [parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出して、[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトを作成します。 `IDebugExpressionContext2::ParseText` により式エバリュエーター (EE) がインスタンス化され、 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) が呼び出されて [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトが取得されます。

 `IDebugExpressionEvaluator::Parse` により、次のタスクが実行されます。

1. [C++ のみ] 式を解析してエラーを探します。

2. `IDebugParsedExpression` インターフェイスを実行し、解析する式をクラスに格納するクラス (この例では `CParsedExpression` と呼ばれる) をインスタンス化します。

3. `CParsedExpression` オブジェクトから `IDebugParsedExpression` インターフェイスを返します。

> [!NOTE]
> 次に示す例と、MyCEE サンプルの例では、式エバリュエーターが評価から解析を分離していません。

## <a name="managed-code"></a>マネージド コード
 次のコードは、マネージド コードでの `IDebugExpressionEvaluator::Parse` の実装を示します。 このバージョンのメソッドは、解析用のコードも同時に評価されるため、[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) までは解析を行いません (「[ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)」を参照してください)。

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT Parse(
                string                 expression,
                uint                   parseFlags,
                uint                   radix,
            out string                 errorMessage,
            out uint                   errorPosition,
            out IDebugParsedExpression parsedExpression)
        {
            errorMessage = "";
            errorPosition = 0;

            parsedExpression =
                new CParsedExpression(parseFlags, radix, expression);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>アンマネージド コード
次のコードは、アンマネージド コードでの `IDebugExpressionEvaluator::Parse` の実装です。 このメソッドは、ヘルパー関数 `Parse` を呼び出して式を解析し、エラーをチェックしますが、結果の値は無視されます。 正式な評価は、評価時に式が解析される [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) まで行われません (「[ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)」を参照してください)。

```cpp
STDMETHODIMP CExpressionEvaluator::Parse(
        in    LPCOLESTR                 pszExpression,
        in    PARSEFLAGS                flags,
        in    UINT                      radix,
        out   BSTR                     *pbstrErrorMessages,
        inout UINT                     *perrorCount,
        out   IDebugParsedExpression  **ppparsedExpression
    )
{
    if (pbstrErrorMessages == NULL)
        return E_INVALIDARG;
    else
        *pbstrErrormessages = 0;

    if (pparsedExpression == NULL)
        return E_INVALIDARG;
    else
        *pparsedExpression = 0;

    if (perrorCount == NULL)
        return E_INVALIDARG;

    HRESULT hr;
    // Look for errors in the expression but ignore results
    hr = ::Parse( pszExpression, pbstrErrorMessages );
    if (hr != S_OK)
        return hr;

    CParsedExpression* pparsedExpr = new CParsedExpression( radix, flags, pszExpression );
    if (!pparsedExpr)
        return E_OUTOFMEMORY;

    hr = pparsedExpr->QueryInterface( IID_IDebugParsedExpression,
                                      reinterpret_cast<void**>(ppparsedExpression) );
    pparsedExpr->Release();

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [ウォッチ ウィンドウ式の評価](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)
