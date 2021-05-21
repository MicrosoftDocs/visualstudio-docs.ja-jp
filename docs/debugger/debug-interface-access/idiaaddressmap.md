---
description: DIA SDK でデバッグ オブジェクトの仮想アドレスと相対仮想アドレスを計算する方法を制御します。
title: IDiaAddressMap | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap interface
ms.assetid: e6467529-508c-4328-85d7-89444ae4d1c1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 085ba4e75eab1dd67585b3926b71edd5dce88d72
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635083"
---
# <a name="idiaaddressmap"></a>IDiaAddressMap
DIA SDK でデバッグ オブジェクトの仮想アドレスと相対仮想アドレスを計算する方法を制御します。

## <a name="syntax"></a>構文

```
IDiaAddressMap : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDiaAddressMap` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)|特定のセッションに対してアドレス マップが確立されているかどうかを示します。|
|[IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)|アドレス マップを使用してシンボルのアドレスを変換する必要があるかどうかを指定します。|
|[IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)|相対仮想アドレスの計算と使用が有効になっているかどうかを示します。|
|[IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)|クライアントが相対仮想アドレスの計算を有効または無効にできるようにします。|
|[IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)|現在のイメージの配置を取得します。|
|[IDiaAddressMap::put_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md)|イメージの配置を設定します。|
|[IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)|イメージ ヘッダーを設定して、相対仮想アドレスの変換を有効にします。|
|[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)|イメージのレイアウトの変換をサポートするアドレス マップを提供します。|

## <a name="remarks"></a>解説
 このインターフェイスによる制御は、指定した 2 つのデータ セット (イメージ ヘッダーとアドレス マップ) にカプセル化されます。 ほとんどのクライアントは、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドを使用してイメージの適切なデバッグ情報を検索します。このメソッドでは、通常、必要なすべてのヘッダーとマップ データ自体を検出できます。 ただし、データの特殊な処理と検索を実装しているクライアントもあります。 このようなクライアントは、`IDiaAddressMap` インターフェイスのメソッドを使用して、DIA SDK に検索結果を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、DIA セッション オブジェクトから使用できます。 クライアントは、DIA セッション オブジェクト インターフェイス (通常は [IDiaSession](../../debugger/debug-interface-access/idiasession.md)) に対して `QueryInterface` メソッドを呼び出して、`IDiaAddressMap` インターフェイスを取得します。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
