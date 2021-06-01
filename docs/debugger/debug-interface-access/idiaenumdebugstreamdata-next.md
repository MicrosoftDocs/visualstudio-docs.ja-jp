---
description: 列挙シーケンス内の指定された数のレコードを取得します。
title: IDiaEnumDebugStreamData::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Next method
ms.assetid: 114171dd-38fd-4bd7-a702-8ff887ffc99b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e854a4bbcd7c1429ef14a90f705f80afc92e75bc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635080"
---
# <a name="idiaenumdebugstreamdatanext"></a>IDiaEnumDebugStreamData::Next
列挙シーケンス内の指定された数のレコードを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next ( 
   ULONG  celt,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[],
   ULONG* pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 celt

[入力] 取得するレコードの数。

 cbData

[入力] データ バッファーのサイズ (バイト単位)。

 pcbData

[出力] 返されるバイト数を返します。 `data` が NULL の場合、`pcbData` には、要求されたすべてのレコードに使用できるデータの合計バイト数が格納されます。

 data[]

[出力] デバッグ ストリーム レコード データが格納されるバッファー。

 pceltFetched

[入力、出力] `data` 内のレコードの数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 レコードがそれ以上ない場合は `S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)
