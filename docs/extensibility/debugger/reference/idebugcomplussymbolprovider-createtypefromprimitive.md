---
title: IDebugComPlusSymbolProvider::CreateTypeFromPrimitive |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::CreateTypeFromPrimitive
- CreateTypeFromPrimitive
ms.assetid: 37213cc2-a038-42ea-9b28-3ae40d4cfe69
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c20ba30a7212c89048d18fab3b20c57260ec5185
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338883"
---
# <a name="idebugcomplussymbolprovidercreatetypefromprimitive"></a>IDebugComPlusSymbolProvider::CreateTypeFromPrimitive
指定したプリミティブ型から型を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateTypeFromPrimitive(
    DWORD          dwPrimType,
    IDebugAddress* pAddress,
    IDebugField**  ppType
);
```

```csharp
int CreateTypeFromPrimitive(
    uint          dwPrimType,
    IDebugAddress pAddress,
    IDebugField   ppType
);
```

## <a name="parameters"></a>パラメーター
`dwPrimType`\
[in]値を[CorElementType 列挙型](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration)プリミティブ型を表します。

`pAddress`\
[in]によって表されるアドレス オブジェクトを[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイス。

`ppType`\
[in]返します、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)型を記述するオブジェクト。

## <a name="return-value"></a>戻り値
成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="example"></a>例
次の例では、このメソッドを実装する方法を示しています、 **CDebugSymbolProvider**を公開するオブジェクト、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)インターフェイス。

```cpp
HRESULT CDebugSymbolProvider::CreateTypeFromPrimitive(
    DWORD dwPrimType,
    IDebugAddress* pAddress,
    IDebugField** ppType)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS addr;
    const COR_SIGNATURE* pTypeInfo = (const COR_SIGNATURE*) & dwPrimType;
    CDebugGenericParamScope* pGenScope = NULL;

    //
    // This function will only work for primitive types
    //

    METHOD_ENTRY( CDebugSymbolProvider::CreateTypeFromPrimitive );

    IfFailGo( pAddress->GetAddress( &addr ) );

    IfNullGo( pGenScope = new CDebugGenericParamScope(addr.GetModule(), addr.tokClass, addr.GetMethod()), E_OUTOFMEMORY );

    IfFailGo( CreateType( pTypeInfo,
                          1,
                          addr.GetModule(),
                          addr.GetMethod(),
                          pGenScope,
                          ppType ) );

    METHOD_EXIT( CDebugSymbolProvider::CreateTypeFromPrimitive, hr );

Error:

    RELEASE( pGenScope );
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
