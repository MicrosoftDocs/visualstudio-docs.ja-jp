---
description: イメージのレイアウトの変換をサポートするアドレス マップを提供します。
title: IDiaAddressMap::set_addressMap | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_addressMap method
ms.assetid: 81e82073-089b-43d5-af39-49d7a4907c7a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b9b00147f4ea8b2313e49e86795c36ec33aae9f1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634989"
---
# <a name="idiaaddressmapset_addressmap"></a>IDiaAddressMap::set_addressMap
イメージのレイアウトの変換をサポートするアドレス マップを提供します。

## <a name="syntax"></a>構文

```C++
HRESULT set_addressMap ( 
   DWORD                     cbData,
   struct DiaAddressMapEntry data[],
   BOOL                      imagetoSymbols
);
```

#### <a name="parameters"></a>パラメーター
 `cbData`

[入力] `data` パラメーター内の要素の数。

 `data[]`

[入力] 変換マップを定義する [DiaAddressMapEntry 構造体](../../debugger/debug-interface-access/diaaddressmapentry.md)の配列。

 `imagetoSymbols`

[入力] `data` パラメーターで (デバッグ シンボルの記述に従って) 新しいイメージ レイアウトから元のレイアウトへのマップを定義する場合は `TRUE`。 `data` が元のレイアウトから取得された新しいイメージ レイアウトへのマップである場合は `FALSE`。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 通常、DIA はプログラム データベース (.pdb) ファイルからアドレス変換マップを取得します。 これらの値が見つからない場合は、[IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) メソッドが 2 回呼び出されます。1 回は `imagetoSymbols` パラメーターが `TRUE` に設定され、もう 1 回は `imagetoSymbols` パラメーターが `FALSE` に設定されます。 両方の変換マップが指定されていない限り、[IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md) メソッドを使用してアドレス マップの変換を有効にすることはできません。

## <a name="see-also"></a>こちらもご覧ください
- [DiaAddressMapEntry 構造体](../../debugger/debug-interface-access/diaaddressmapentry.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)
