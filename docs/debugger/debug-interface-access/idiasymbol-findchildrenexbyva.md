---
description: 指定の仮想アドレスで有効なシンボルの子を取得します。
title: IDiaSymbol::findChildrenExByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenExByVA
ms.assetid: 29080009-36e4-4697-acd7-50f2e3e1bf1b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ff9ed80ebd63baa8733fc3bab7d3d74ed3d4cc99
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635176"
---
# <a name="idiasymbolfindchildrenexbyva"></a>IDiaSymbol::findChildrenExByVA
指定の仮想アドレスで有効なシンボルの子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findChildrenExByVA ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   DWORD             address,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `symtag`

[入力] [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)に関するページでの定義に基づき、取得する子のシンボル タグを指定します。 すべての子を取得するには、`SymTagNull` に設定します。

 `name`

[入力] 取得する子の名前を指定します。 すべての子を取得するには、`NULL` に設定します。

 `compareFlags`

[入力] 名前の照合に適用する比較オプションを指定します。 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)に関するページの列挙型の値は、単独で使用することも、組み合わせて使用することもできます。

 `address`

[入力] 仮想アドレスを指定します。

 `ppResult`

[出力] 取得された子シンボルの一覧を含む [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 シンボルの子が少なくとも 1 つ見つかった場合は `S_OK` を返し、子が見つからなかった場合は `S_FALSE` を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>解説
 返されるローカル シンボルには、有効範囲の情報が含まれます。

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
