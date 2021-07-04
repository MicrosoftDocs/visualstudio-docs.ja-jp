---
title: GetMethodProperty の実装 | Microsoft Docs
description: デバッグ エンジンの GetDebugProperty を使用して、Visual Studio によりスタック フレームの現在のメソッドに関する情報が取得されるしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- GetMethodProperty method
- IDebugExpressionEvaluator2 property
ms.assetid: 6305874f-a2c4-4432-834c-07530ea84bff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6ab7b0ba5e51ba8ea47b473934e825b82dec320c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903295"
---
# <a name="implement-getmethodproperty"></a>GetMethodProperty の実装
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

Visual Studio から、デバッグ エンジンの (DE) [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) が呼び出されます。これにより [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) が呼び出され、スタック フレームの現在のメソッドに関する情報が取得されます。

この `IDebugExpressionEvaluator::GetMethodProperty` の実装では、次のタスクが実行されます。

1. [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) が呼び出され、[IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) オブジェクトが渡されます。 シンボル プロバイダー (SP) から、指定されたアドレスを含むメソッドを表す [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) が返されます。

2. `IDebugContainerField` から [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) が取得されます。

3. [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを実装し、SP から返された `IDebugMethodField` オブジェクトを格納するクラス (この例では `CFieldProperty` と呼ばれます) をインスタンス化します。

4. `CFieldProperty` オブジェクトから `IDebugProperty2` インターフェイスを返します。

## <a name="managed-code"></a>マネージド コード
この例は、マネージド コードでの `IDebugExpressionEvaluator::GetMethodProperty` の実装を示しています。

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        public HRESULT GetMethodProperty(
                IDebugSymbolProvider symbolProvider,
                IDebugAddress        address,
                IDebugBinder         binder,
                int                  includeHiddenLocals,
            out IDebugProperty2      property)
        {
            IDebugContainerField containerField = null;
            IDebugMethodField methodField       = null;
            property = null;

            // Get the containing method field.
            symbolProvider.GetContainerField(address, out containerField);
            methodField = (IDebugMethodField) containerField;

            // Return the property of method field.
            property = new CFieldProperty(symbolProvider, address, binder, methodField);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>アンマネージド コード
この例は、アンマネージド コードでの `IDebugExpressionEvaluator::GetMethodProperty` の実装を示しています。

```
[CPP]
STDMETHODIMP CExpressionEvaluator::GetMethodProperty(
        in IDebugSymbolProvider *pprovider,
        in IDebugAddress        *paddress,
        in IDebugBinder         *pbinder,
        in BOOL                  includeHiddenLocals,
        out IDebugProperty2    **ppproperty
    )
{
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    IDebugContainerField* pcontainer = NULL;

    hr = pprovider->GetContainerField(paddress, &pcontainer);
    if (FAILED(hr))
        return hr;

    IDebugMethodField*    pmethod    = NULL;
    hr = pcontainer->QueryInterface( IID_IDebugMethodField,
            reinterpret_cast<void**>(&pmethod));
    pcontainer->Release();
    if (FAILED(hr))
        return hr;

    CFieldProperty* pfieldProperty = new CFieldProperty( pprovider,
                                                         paddress,
                                                         pbinder,
                                                         pmethod );
    pmethod->Release();
    if (!pfieldProperty)
        return E_OUTOFMEMORY;

    hr = pfieldProperty->Init();
    if (FAILED(hr))
    {
        pfieldProperty->Release();
        return hr;
    }

    hr = pfieldProperty->QueryInterface( IID_IDebugProperty2,
            reinterpret_cast<void**>(ppproperty));
    pfieldProperty->Release();

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [ローカルの実装のサンプル](../../extensibility/debugger/sample-implementation-of-locals.md)
