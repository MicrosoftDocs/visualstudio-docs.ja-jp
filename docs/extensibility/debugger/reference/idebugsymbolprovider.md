---
description: このインターフェイスは、シンボルと型を提供し、それらをフィールドとして返すシンボル プロバイダーを表します。
title: IDebugSymbolProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider
helpviewer_keywords:
- IDebugSymbolProvider interface
ms.assetid: df5f095f-1dee-46f9-84cf-92417c71d5fb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bda1ec3c65e2f3fdc811b6bde636e78f5a787f32
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053166"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
このインターフェイスは、シンボルと型を提供し、それらをフィールドとして返すシンボル プロバイダーを表します。

## <a name="syntax"></a>構文

```
IDebugSymbolProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
シンボル プロバイダーでは、このインターフェイスを実装して、シンボルと型の情報を式エバリュエーターに提供する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、COM の `CoCreateInstance` 関数を使用する (アンマネージド シンボル プロバイダーの場合) か、適切なマネージド コード アセンブリを読み込んで、そのアセンブリ内の情報に基づいてシンボル プロバイダーをインスタンス化します。 デバッグ エンジンでは、式エバリュエーターと連携して動作するようにシンボル プロバイダーをインスタンス化します。 このインターフェイスをインスタンス化する 1 つの方法については、「例」を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDebugSymbolProvider` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|`Initialize`|非推奨。 使用しないでください。|
|`Uninitialize`|使用は推奨されていません。 使用しないでください。|
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|デバッグ アドレスが格納されているフィールドを取得します。|
|`GetField`|非推奨。 使用しないでください。|
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|ドキュメントの位置をデバッグ アドレスの配列にマップします。|
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|ドキュメント コンテキストをデバッグ アドレスの配列にマップします。|
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|デバッグ アドレスをドキュメント コンテキストにマップします。|
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|デバッグ アドレスのコードをコンパイルするために使用される言語を取得します。|
|`GetGlobalContainer`|非推奨。 使用しないでください。|
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|完全修飾メソッド名を表すフィールドを取得します。|
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|完全修飾クラス名を表すクラス フィールド型を取得します。|
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|デバッグ アドレスに関連付けられた名前空間の列挙子を作成します。|
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|シンボル名をシンボルの種類にマップします。|
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|メソッド内の指定されたデバッグ アドレスの後に続くデバッグ アドレスを取得します。|

## <a name="remarks"></a>解説
このインターフェイスでは、ドキュメントの位置をデバッグ アドレスに (およびその逆に) にマップします。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例
この例では、GUID (デバッグ エンジンでこの値が認識されている必要があります) を指定して、シンボル プロバイダーをインスタンス化する方法を示します。

```cpp
// A debug engine uses its own symbol provider and would know the GUID
// of that provider.
IDebugSymbolProvider *GetSymbolProvider(GUID *pSymbolProviderGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugSymbolProvider *pProvider = NULL;
    if (pSymbolProviderGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetSPMetric(*pSymbolProviderGuid,
                      storetypeFile,
                      metricCLSID,
                      &clsidProvider,
                      strRegistrationRoot);
        if (IsEqualGUID(clsidProvider,GUID_NULL)) {
            // No file type provider, try metadata provider.
            ::GetSPMetric(*pSymbolProviderGuid,
                          ::storetypeMetadata,
                          metricCLSID,
                          &clsidProvider,
                          strRegistrationRoot);
        }
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugSymbolProvider> spSymbolProvider;
            spSymbolProvider.CoCreateInstance(clsidProvider);
            if (spSymbolProvider != NULL) {
                pProvider = spSymbolProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
