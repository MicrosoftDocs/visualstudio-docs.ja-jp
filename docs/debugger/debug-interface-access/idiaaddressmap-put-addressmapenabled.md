---
description: アドレス マップを使用してシンボルのアドレスを変換する必要があるかどうかを指定します。
title: IDiaAddressMap::put_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_addressMapEnabled method
ms.assetid: 0f205337-4e59-4383-8059-7b1d207d6dcd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 84878e83db15cfa5a9c68dccfec78536035cb70f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635087"
---
# <a name="idiaaddressmapput_addressmapenabled"></a>IDiaAddressMap::put_addressMapEnabled
アドレス マップを使用してシンボルのアドレスを変換する必要があるかどうかを指定します。

## <a name="syntax"></a>構文

```C++
HRESULT put_addressMapEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>パラメーター
 NewVal

[入力] シンボルの変換を有効にする場合は `TRUE` に設定し、無効にする場合は `FALSE` に設定します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 実行可能ファイルのポスト プロセッサにより、実行可能ファイルが更新されることがあります。 DIA には、新しいレイアウトへのシンボルの変換をサポートするメカニズムが含まれています。

 PDB ファイルが読み込まれると、そのファイルに保存されているアドレス マップが有効になります。 ただし、クライアント アプリケーションでは、[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) メソッドを呼び出して独自のアドレス マップを提供することが必要な場合があります。 `set_addressMap` メソッドが成功した場合、クライアント アプリケーションは `NewVal` パラメーターが `TRUE` に設定された `put_addressMapEnabled` メソッドを呼び出して、そのアドレス マップの使用を有効にする必要があります。

 有効になっているアドレス マップの現在の状態は、[IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md) メソッドを呼び出すことで取得できます。

## <a name="see-also"></a>関連項目
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)
