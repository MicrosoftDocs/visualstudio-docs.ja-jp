---
description: イメージ ヘッダーを設定して、相対仮想アドレス変換を有効にします。
title: IDiaAddressMap::set_imageHeaders | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_imageHeaders method
ms.assetid: a46b9d0e-43e6-433f-b2c7-aa203981e4e4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f5ae155c6491acf90c327b2503e6993a08c5f536
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635086"
---
# <a name="idiaaddressmapset_imageheaders"></a>IDiaAddressMap::set_imageHeaders
イメージ ヘッダーを設定して、相対仮想アドレス変換を有効にします。

## <a name="syntax"></a>構文

```C++
HRESULT set_imageHeaders ( 
   DWORD cbData,
   BYTE  data[],
   BOOL  originalHeaders
);
```

#### <a name="parameters"></a>パラメーター
 cbData

[入力] ヘッダー データのバイト数。 `n*sizeof(IMAGE_SECTION_HEADER)` である必要があります。`n` は、実行可能ファイル内のセクション ヘッダーの数です。

 data[]

[入力] イメージ ヘッダーとして使用される `IMAGE_SECTION_HEADER` 構造体の配列。

 originalHeaders

[入力] イメージ ヘッダーが新しいイメージからのものである場合は `FALSE` に設定し、アップグレード前の元のイメージを反映している場合は `TRUE` に設定します。 通常、これは、[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) メソッドの呼び出しと組み合わせて使用する場合にのみ、`TRUE` に設定されます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 `IMAGE_SECTION_HEADER` 構造体は Winnt.h で宣言され、実行可能ファイルのイメージ セクション ヘッダー形式を表します。

 相対仮想アドレスの計算は、`IMAGE_SECTION_HEADER` 値によって異なります。 通常、DIA は、プログラム データベース (.pdb) ファイルからこれらを取得します。 これらの値が見つからない場合、DIA は相対仮想アドレスを計算できず、[IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) メソッドは `FALSE` を返します。 その後、クライアントは欠落しているイメージ ヘッダーをイメージ自体から提供した後に、[IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md) メソッドを呼び出して、相対仮想アドレスの計算を有効にする必要があります。

## <a name="see-also"></a>関連項目
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)
