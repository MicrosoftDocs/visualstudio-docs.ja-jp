---
title: IDebugComPlusSymbolProvider::GetArrayTypeFromAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetArrayTypeFromAddress
- IDebugComPlusSymbolProvider::GetArrayTypeFromAddress
ms.assetid: cc0c53f1-8c0f-49fa-8dbe-bc155e9ce0ef
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0878f4224d024e353c2c7ab798450a65e9677178
ms.sourcegitcommit: 7153e2fc717d32e0e9c8a9b8c406dc4053c9fd53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "56413346"
---
# <a name="idebugcomplussymbolprovidergetarraytypefromaddress"></a>IDebugComPlusSymbolProvider::GetArrayTypeFromAddress
については、デバッグ アドレスが指定されて、指定した配列の型を取得します。

## <a name="syntax"></a>構文

```
[C++]
HRESULT GetArrayTypeFromAddress(
    IDebugAddress* pAddress,
    BYTE*          pSig,
    DWORD          dwSigLength,
    IDebugField**  ppField
);
```

```
[C#]
int GetArrayTypeFromAddress(
    IDebugAddress   pAddress,
    int[]           pSig,
    uint            dwSigLength,
    out IDebugField ppField
);
```

#### <a name="parameters"></a>パラメーター
`pAddress`  
[in]によって表されるデバッグ アドレス、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイス。

`pSig`  
[in]確認する配列。

`dwSigLength`  
[in]長のバイト単位、`pSig`配列。

`ppField`  
[out]によって表される配列の型を返します、 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)インターフェイス。

## <a name="return-value"></a>戻り値
成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="example"></a>例
次の例では、このメソッドを実装する方法を示しています、 **CDebugSymbolProvider**を公開するオブジェクト、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)インターフェイス。

```cpp
HRESULT CDebugSymbolProvider::GetArrayTypeFromAddress(
    IDebugAddress *pAddress,
    BYTE *pSig,
    DWORD dwSigLength,
    IDebugField **ppField)
{
    HRESULT hr = E_FAIL;
    CDEBUG_ADDRESS da;
    CDebugGenericParamScope* pGenScope = NULL;

    METHOD_ENTRY( CDebugDynamicFieldSymbol::GetArrayTypeFromAddress );

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidWritePtr(ppField, IDebugField*));

    IfFailGo( pAddress->GetAddress(&da) );

    if ( S_OK == hr )
    {
        IfNullGo( pGenScope = new CDebugGenericParamScope(da.GetModule(), da.tokClass, da.GetMethod()), E_OUTOFMEMORY );

        IfFailGo( this->CreateType((const COR_SIGNATURE*)(pSig), dwSigLength, da.GetModule(), mdMethodDefNil, pGenScope, ppField) );
    }

Error:

    METHOD_EXIT( CDebugDynamicFieldSymbol::GetArrayTypeFromAddress, hr );
    RELEASE( pGenScope );
    return hr;
}
```

## <a name="see-also"></a>関連項目
[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
