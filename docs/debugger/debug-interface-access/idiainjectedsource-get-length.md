---
description: コードのバイト数を取得します。
title: IDiaInjectedSource::get_length | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_length method
ms.assetid: 38b88b8b-c2e0-4b2d-8b8b-9ff373733e78
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3154f1a76c0f5b74c795884c62ecc61e049264a9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634415"
---
# <a name="idiainjectedsourceget_length"></a>IDiaInjectedSource::get_length
コードのバイト数を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_length ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] コードのバイト数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドによって返される値は、ソース コードの長さであり、[IDiaInjectedSource::get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md) メソッドによって返される値と同じです。

## <a name="see-also"></a>関連項目
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
- [IDiaInjectedSource::get_source](../../debugger/debug-interface-access/idiainjectedsource-get-source.md)
