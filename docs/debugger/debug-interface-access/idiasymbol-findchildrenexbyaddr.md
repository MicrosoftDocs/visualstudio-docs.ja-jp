---
description: 指定されたアドレスにあるシンボルの有効な子を取得します。
title: IDiaSymbol::findChildrenExByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenExByAddr
ms.assetid: c1e7885d-2d15-4529-9ac2-32dd22efe31c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 254ab98e8b1f1ec88fc946221bb2e15e2af76ffd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635178"
---
# <a name="idiasymbolfindchildrenexbyaddr"></a>IDiaSymbol::findChildrenExByAddr
指定されたアドレスにあるシンボルの有効な子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findChildrenExByAddr ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   DWORD             address,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `symtag`

[入力] [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)で定義されている、取得する子のシンボル タグを指定します。 すべての子を取得するには、`SymTagNull` に設定します。

 `name`

[入力] 取得する子の名前を指定します。 すべての子を取得するには、`NULL` に設定します。

 `compareFlags`

[入力] 名前の照合に適用する比較オプションを指定します。 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)に関する記事の列挙型の値は、単独で使用することも、組み合わせて使用することもできます。

 `address`

[入力] シンボルのアドレス。

 `ppResult`

[出力] 取得された子シンボルのリストを含む [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 シンボルの子が少なくとも 1 つ見つかった場合は `S_OK` を返し、子が見つからなかった場合は `S_FALSE` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 返されるローカル シンボルには、有効範囲情報が含まれます。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)
