---
description: OEM のシンボルのデータ バイトを取得します。
title: IDiaSymbol::get_dataBytes | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_dataBytes method
ms.assetid: 5eb37179-20d8-44ae-a72a-405c1b0435c4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 09156b8d99daa5cbfd065110073c3c185c3ac0a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635163"
---
# <a name="idiasymbolget_databytes"></a>IDiaSymbol::get_dataBytes
OEM のシンボルのデータ バイトを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_dataBytes ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>パラメーター
 `cbData`

[入力] データを保持するバッファーのサイズ。

 `pcbData`

[出力] 書き込まれたバイト数を返します。または `data` パラメーターが `NULL` の場合は、使用可能なバイト数を返します。

 `data[]`
- [out,] データ バイトを格納するバッファー。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
