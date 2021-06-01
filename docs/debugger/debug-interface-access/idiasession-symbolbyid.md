---
description: シンボルを一意の識別子ごとに取得します。
title: IDiaSession::symbolById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symbolById method
ms.assetid: 062e4b5a-9c4d-4703-88da-ec13102c2b66
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 979825cd3e62c97334d55676b3bf32bf874f8445
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634297"
---
# <a name="idiasessionsymbolbyid"></a>IDiaSession::symbolById
シンボルを一意の識別子ごとに取得します。

## <a name="syntax"></a>構文

```C++
HRESULT symbolById (
    DWORD        id,
    IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>パラメーター
`id`

[入力] 一意の識別子。

`ppSymbol`

[出力] 取得されたシンボルを表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
指定された識別子は、すべてのシンボルを一意にするために DIA SDK によって内部的に使用される一意の値です。

たとえば、このメソッドを使用すると、別のシンボルの種類を表すシンボルを取得できます (例を参照)。

## <a name="example"></a>例
この例では、別のシンボルの種類を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) を取得しています。 セッションの `symbolById` メソッドの使用方法を次の例に示します。 より簡単な方法は、[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md) メソッドを呼び出して、種類のシンボルを直接取得することです。

```C++
IDiaSymbol *GetSymbolType(IDiaSymbol *pSymbol, IDiaSession *pSession)
{
    IDiaSymbol *pTypeSymbol = NULL;
    if (pSymbol != NULL && pSession != NULL)
    {
        DWORD symbolTypeId;
        pSymbol->get_typeId(&symbolTypeId);
        pSession->symbolById(symbolTypeId, &pTypeSymbol);
    }
    return(pTypeSymbol);
}
```

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
