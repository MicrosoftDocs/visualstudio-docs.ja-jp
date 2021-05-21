---
description: このシンボルによって表されるオブジェクトによって使用されるメモリのビット数またはバイト数を取得します。
title: IDiaSymbol::get_length | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_length method
ms.assetid: cc62f028-d195-4fbf-93bc-10b08bef52d2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a7b3a7a88c688f8ff68f2c1280390f10110c3a9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635257"
---
# <a name="idiasymbolget_length"></a>IDiaSymbol::get_length
このシンボルによって表されるオブジェクトによって使用されるメモリのビット数またはバイト数を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_length ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] このシンボルによって表されるオブジェクトによって使用されるメモリのビット数またはバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 シンボルの [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md) が `LocIsBitField` の場合、このメソッドによって返される長さはビット単位になります。それ以外の場合、他のすべての場所の種類の長さはバイト単位になります。

## <a name="example"></a>例

```C++
IDiaSymbol* pSymbol;
ULONGLONG   length;
pSymbol->get_length( &length );
```

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
