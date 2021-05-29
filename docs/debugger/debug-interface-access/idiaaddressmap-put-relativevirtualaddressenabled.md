---
description: クライアントから、相対仮想アドレス (RVA) の計算と使用を有効または無効にできるようにします。
title: IDiaAddressMap::put_relativeVirtualAddressEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_relativeVirtualAddressEnabled method
ms.assetid: 767c078e-8ad7-4940-9e00-cae7704aadee
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7c3aab1379a39ee6abfd977350743e36c9792efb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634990"
---
# <a name="idiaaddressmapput_relativevirtualaddressenabled"></a>IDiaAddressMap::put_relativeVirtualAddressEnabled
クライアントから、相対仮想アドレス (RVA) の計算と使用を有効または無効にできるようにします。

## <a name="syntax"></a>構文

```C++
HRESULT put_relativeVirtualAddressEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>パラメーター
 NewVal

[入力] 有効にするには `TRUE` に、無効にするには `FALSE` に設定します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 DIA インターフェイスに記述されている、実行可能ファイルのイメージ ベースと相対的なデバッグ オブジェクトのアドレスは、相対仮想アドレスとして取得できます。

 RVA の使用は、セグメントが PDB ファイルから最初に読み込まれたときに有効になります。 RVA の使用の最新の状態を取得するには、[IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) メソッドを呼び出します。

 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) メソッドが正常に呼び出され、新しいイメージ ヘッダーが確立された後に RVA を有効にするには `put_relativeVirtualAddress` メソッドを呼び出す必要があります。

## <a name="see-also"></a>関連項目
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)
