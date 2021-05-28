---
description: 特定のセッションに対してアドレス マップが確立されているかどうかを示します。
title: IDiaAddressMap::get_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_addressMapEnabled method
ms.assetid: 6183dc5e-befa-4e5a-ae5a-f4aa24f3ed9e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6a55ff89e97d1898ec2ced2b62f7cdfa5a0df817
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634514"
---
# <a name="idiaaddressmapget_addressmapenabled"></a>IDiaAddressMap::get_addressMapEnabled
特定のセッションに対してアドレス マップが確立されているかどうかを示します。

## <a name="syntax"></a>構文

```C++
HRESULT get_addressMapEnabled ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 pRetVal

[出力] アドレス マッピングが有効になっている場合は `TRUE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 実行可能ファイルのポスト プロセッサにより、実行可能ファイルが更新されることがあります。 DIA には、新しいレイアウトへのシンボルの変換をサポートするメカニズムが含まれています。

 クライアント アプリケーションでは、[IDiaSession](../../debugger/debug-interface-access/idiasession.md) インターフェイスから [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md) インターフェイスを取得し、[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) メソッドを呼び出し、その後で [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md) メソッドを呼び出すことによって、特定のセッションのアドレス マップを設定できます。 `get_addressMapEnabled` メソッドからは、`put_addressMapEnabled` メソッドの呼び出しの結果が返されます。

## <a name="see-also"></a>関連項目
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)
