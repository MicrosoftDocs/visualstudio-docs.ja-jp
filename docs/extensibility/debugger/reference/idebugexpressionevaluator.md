---
description: このインターフェイスは、式エバリュエーターを表します。
title: IDebugExpressionEvaluator | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator
helpviewer_keywords:
- IDebugExpressionEvaluator interface
ms.assetid: 0636d8c3-625a-49fa-94b6-516f22b7e1bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dd14e85d279bd724dcfdf2cd9b71028ac5a4fd87
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092073"
---
# <a name="idebugexpressionevaluator"></a>IDebugExpressionEvaluator
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

このインターフェイスは、式エバリュエーターを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionEvaluator : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
式エバリュエーターは、このインターフェイスを実装する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、エバリュエーターのクラス ID (CLSID) を使用して、`CoCreateInstance` メソッドを介して式エバリュエーターをインスタンス化します。 「例」を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDebugExpressionEvaluator` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)|式の文字列を解析された式に変換します。|
|[GetMethodProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)|メソッドのローカル変数、引数、およびその他のプロパティを取得します。|
|[GetMethodLocationProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodlocationproperty.md)|メソッドの位置とオフセットをメモリ アドレスに変換します。|
|[SetLocale](../../../extensibility/debugger/reference/idebugexpressionevaluator-setlocale.md)|出力可能な結果を作成するために使用する言語を決定します。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugexpressionevaluator-setregistryroot.md)|レジストリ ルートを設定します。 サイドバイサイドのデバッグに使用されます。|

## <a name="remarks"></a>解説
一般的な状況では、デバッグ エンジン (DE) は [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) の呼び出しの結果として式エバリュエーター (EE) をインスタンス化します。 DE は使用する EE の言語とベンダーを認識しているため、DE は、EE の CLSID をレジストリから取得します (この取得には、[デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)関数、`GetEEMetric` が役立ちます)。

EE がインスタンス化された後、DE は [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) を呼び出して式を解析し、[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトに格納します。 後で、[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) の呼び出しで、式が評価されます。

## <a name="requirements"></a>必要条件
ヘッダー: ee.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例
この例では、シンボル プロバイダーとソース コード内のアドレスを指定して、式エバリュエーターをインスタンス化する方法を示します。 この例では、[デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) ライブラリ、dbgmetric.lib の関数である `GetEEMetric` を使用します。

```cpp
IDebugExpressionEvaluator GetExpressionEvaluator(IDebugSymbolProvider pSymbolProvider,
                                                 IDebugAddress *pSourceAddress)
{
    // This is typically defined globally but is specified here just
    // for this example.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";

    IDebugExpressionEvaluator *pEE = NULL;
    if (pSymbolProvider != NULL && pSourceAddress != NULL) {
        HRESULT hr         = S_OK;
        GUID  languageGuid = { 0 };
        GUID  vendorGuid   = { 0 };

        hr = pSymbolProvider->GetLanguage(pSourceAddress,
                                          &languageGuid,
                                          &vendorGuid);
        if (SUCCEEDED(hr)) {
            CLSID clsidEE = { 0 };
            CComPtr<IDebugExpressionEvaluator> spExpressionEvaluator;
            // Get the expression evaluator's CLSID from the registry.
            ::GetEEMetric(languageGuid,
                          vendorGuid,
                          metricCLSID,
                          &clsidEE,
                          strRegistrationRoot);
            if (!IsEqualGUID(clsidEE,GUID_NULL)) {
                // Instantiate the expression evaluator.
                spExpressionEvaluator.CoCreateInstance(clsidEE);
            }
            if (spExpressionEvaluator != NULL) {
                pEE = spExpressionEvaluator.Detach();
            }
        }
    }
    return pEE;
}
```

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [デバッグ用 SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
