---
title: ウォッチ式の評価 | Microsoft Docs
description: Visual Studio によって、ウォッチ式の値を表示する準備ができたときに、EvaluateSync がどのように使用されるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 21a173a8c041bbaf12cb67bf90e1c4407ac5e4a7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097059"
---
# <a name="evaluate-a-watch-expression"></a>ウォッチ式の評価
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

Visual Studio でウォッチ式の値を表示する準備が整うと、[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) が呼び出され、次に、[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) が呼び出されます。 このプロセスでは、式の値と型を含む [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトが生成されます。

`IDebugParsedExpression::EvaluateSync` のこの実装では、式が解析され、同時に評価されます。 この実装では、次のタスクが実行されます。

1. 式を解析して評価し、値とその型を保持するジェネリック オブジェクトを生成します。 C# では、これは `object` として表され、C++ では `VARIANT` として表されます。

2. `IDebugProperty2` インターフェイスを実行し、返される値をクラスに格納するクラス (この例では `CValueProperty` と呼ばれている) をインスタンス化します。

3. `CValueProperty` オブジェクトから `IDebugProperty2` インターフェイスを返します。

## <a name="managed-code"></a>マネージド コード
これは、マネージド コードでの `IDebugParsedExpression::EvaluateSync` の実装です。 ヘルパー メソッド `Tokenize` では、式が解析ツリーに解析されます。 ヘルパー関数 `EvalToken` では、トークンが値に変換されます。 ヘルパー関数 `FindTerm` では、解析ツリーが再帰的に走査され、各ノードに対して `EvalToken` が呼び出され、値が表され、式で任意の演算 (加算や減算) が適用されます。

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT EvaluateSync(
            uint evalFlags,
            uint timeout,
            IDebugSymbolProvider provider,
            IDebugAddress address,
            IDebugBinder binder,
            string resultType,
            out IDebugProperty2 result)
        {
            HRESULT retval = COM.S_OK;
            this.evalFlags = evalFlags;
            this.timeout = timeout;
            this.provider = provider;
            this.address = address;
            this.binder = binder;
            this.resultType = resultType;

            try
            {
                IDebugField field = null;
                // Tokenize, then parse.
                tokens = Tokenize(expression);
                result = new CValueProperty(
                        expression,
                        (int) FindTerm(EvalToken(tokens[0], out field),1),
                        field,
                        binder);
            }
            catch (ParseException)
            {
                result = new CValueProperty(expression, "Huh?");
                retval = COM.E_INVALIDARG;
            }
            return retval;
        }
    }
}
```

## <a name="unmanaged-code"></a>アンマネージド コード
これは、アンマネージド コードでの `IDebugParsedExpression::EvaluateSync` の実装です。 ヘルパー関数 `Evaluate` では、式が解析され、評価されて、結果の値を保持する `VARIANT` が返されます。 ヘルパー関数 `VariantValueToProperty` では、`VARIANT` が `CValueProperty` オブジェクトにバンドルされます。

```cpp
STDMETHODIMP CParsedExpression::EvaluateSync(
    in  DWORD                 evalFlags,
    in  DWORD                 dwTimeout,
    in  IDebugSymbolProvider* pprovider,
    in  IDebugAddress*        paddress,
    in  IDebugBinder*         pbinder,
    in  BSTR                  bstrResultType,
    out IDebugProperty2**     ppproperty )
{
    // dwTimeout parameter is ignored in this implementation.
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (paddress == NULL)
        return E_INVALIDARG;

    if (pbinder == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    VARIANT value;
    BSTR    bstrErrorMessage = NULL;
    hr = ::Evaluate( pprovider,
                     paddress,
                     pbinder,
                     m_expr,
                     &bstrErrorMessage,
                     &value );
    if (hr != S_OK)
    {
        if (bstrErrorMessage == NULL)
            return hr;

        //we can display better messages ourselves.
        HRESULT hrLocal = S_OK;
        VARIANT varType;
        VARIANT varErrorMessage;

        VariantInit( &varType );
        VariantInit( &varErrorMessage );
        varErrorMessage.vt      = VT_BSTR;
        varErrorMessage.bstrVal = bstrErrorMessage;

        CValueProperty* valueProperty = new CValueProperty();
        if (valueProperty != NULL)
        {
            hrLocal = valueProperty->Init(m_expr, varType, varErrorMessage);
            if (SUCCEEDED(hrLocal))
            {
                hrLocal = valueProperty->QueryInterface( IID_IDebugProperty2,
                        reinterpret_cast<void**>(ppproperty) );
            }
        }

        VariantClear(&varType);
        VariantClear(&varErrorMessage); //frees BSTR
        if (!valueProperty)
            return hr;
        valueProperty->Release();
        if (FAILED(hrLocal))
            return hr;
    }
    else
    {
        if (bstrErrorMessage != NULL)
            SysFreeString(bstrErrorMessage);

        hr = VariantValueToProperty( pprovider,
                                     paddress,
                                     pbinder,
                                     m_radix,
                                     m_expr,
                                     value,
                                     ppproperty );
        VariantClear(&value);
        if (FAILED(hr))
            return hr;
    }

    return S_OK;
}
```

## <a name="see-also"></a>関連項目
- [ウォッチ ウィンドウ式の評価](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [式の評価の実装のサンプル](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)
