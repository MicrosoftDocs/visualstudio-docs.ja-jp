---
description: LocationType Enumeration) が LocIsEnregistered` に設定されているとき、場所のレジスタ指定子を取得します。
title: IDiaSymbol::get_registerId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3f6845c83b46fb524221933eb859742ebe7a95e6
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635239"
---
# <a name="idiasymbolget_registerid"></a>IDiaSymbol::get_registerId
[LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md) が `LocIsEnregistered` に設定されているとき、場所のレジスタ指定子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_registerId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] 場所のレジスタ指定子を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 シンボルがレジスタに対して相対となる場合、つまり、シンボルの [LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md) が `LocIsRegRel` に設定されている場合、`get_registerId` メソッドを使用し、続けて [IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md) を呼び出し、シンボルが置かれているレジスタからオフセットを取得します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
