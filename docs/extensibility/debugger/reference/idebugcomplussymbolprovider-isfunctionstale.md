---
description: 指定されたデバッグアドレスにある関数が古いものと見なされるかどうかを判断します。
title: 'IDebugComPlusSymbolProvider:: IsFunctionStale |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::IsFunctionStale
ms.assetid: dcffc090-4ed8-47b2-ba51-bce1a6b6428d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 93a6bd0eb2a6715587c2d845cf161dba8c756aa2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095499"
---
# <a name="idebugcomplussymbolproviderisfunctionstale"></a>IDebugComPlusSymbolProvider::IsFunctionStale
指定されたデバッグアドレスにある関数が古いものと見なされるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsFunctionStale(
    IDebugAddress* pAddress
);
```

```csharp
int IsFunctionStale(
    IDebugAddress pAddress
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
から [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスによって表されるデバッグアドレス。 このアドレスは METHOD_ADDRESS である必要があります。

## <a name="return-value"></a>戻り値
関数が古いと見なされた場合、はを返し `S_OK` ます。 関数が古くない場合、はを返し `S_FALSE` ます。

## <a name="example"></a>例
次の例は、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)インターフェイスを公開する **Cdebugシンボルプロバイダー** オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
HRESULT CDebugSymbolProvider::IsFunctionStale(
    IDebugAddress* pAddress
)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS address;
    CComPtr<CModule> pModule;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pAddress, IDebugAddress));

    METHOD_ENTRY( CDebugSymbolProvider::IsFunctionStale );

    IfFalseGo( pAddress, S_FALSE );
    IfFailGo( pAddress->GetAddress( &address ) );

    ASSERT(address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD);
    IfFalseGo( address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD, S_FALSE );

    IfFailGo( GetModule( address.GetModule(), &pModule) );

    if (!pModule->IsFunctionStale( address.addr.addr.addrMethod.tokMethod,
                                   address.addr.addr.addrMethod.dwVersion ))
    {

        // S_FALSE indicates the function is not stale

        hr = S_FALSE;
    }

Error:

    METHOD_EXIT( CDebugSymbolProvider::IsFunctionStale, hr );

    if (!SUCCEEDED(hr))
    {
        hr = S_FALSE;
    }

    return hr;
}
```

## <a name="see-also"></a>こちらもご覧ください
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
