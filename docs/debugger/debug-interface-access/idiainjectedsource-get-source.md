---
description: ソース コードのバイト数を取得します。
title: IDiaInjectedSource::get_source | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_source method
ms.assetid: 3c0b5386-321f-4f8f-85cc-e2ee7b4cc3d2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 248fc00320f94b297a9b0697742dff6e3fbd2004
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634413"
---
# <a name="idiainjectedsourceget_source"></a>IDiaInjectedSource::get_source
ソース コードのバイト数を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_source ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>パラメーター
 `cbData`

[入力] データ バッファーのサイズを表すバイト数。

 `pcbData`

[出力] 返されたバイト数を表すバイト数を返します。 `data` が `NULL` の場合、`pcbData` は利用可能な合計データ バイト数です。

 `data[]`

[出力] コピー元のバイトが格納されるバッファー。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
