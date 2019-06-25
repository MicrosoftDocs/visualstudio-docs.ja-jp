---
title: Idiaenumdebugstreams::next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Next method
ms.assetid: eb8eae5a-be27-45f4-a7bd-6e4ef0652385
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a1b7819c90804933795c220c4d47f288d29abfe1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838299"
---
# <a name="idiaenumdebugstreamsnext"></a>IDiaEnumDebugStreams::Next
指定された数の列挙体シーケンス内の debug ストリームを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next ( 
   ULONG                     celt,
   IDiaEnumDebugStreamData** rgelt,
   ULONG*                    pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 celt

[in]デバッグ ストリームを取得する列挙子の数。

 rgelt

[out]配列を返します[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)デバッグを表すオブジェクトをストリームを取得します。

 pceltFetched

[out]返されるデバッグ ストリームの数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返します`S_FALSE`以上のストリームがありませんがある場合。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)