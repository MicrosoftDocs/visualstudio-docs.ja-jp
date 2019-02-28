---
title: Idiaenumsegments::next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Next method
ms.assetid: 53f61874-d821-47ab-a1f5-27e982804a6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f9b0f0d06ae5303277c296fd56e36e60b9a6f022
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56624608"
---
# <a name="idiaenumsegmentsnext"></a>IDiaEnumSegments::Next
指定した列挙体シーケンス内のセグメント数を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next ( 
   ULONG         celt,
   IDiaSegment** rgelt,
   ULONG*        pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 celt

[in]取得する列挙子内のセグメントの数。

 rgelt

[out]情報を格納する目的である配列[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)セグメントを表すオブジェクト。

 pceltFetched

[out]フェッチされた列挙子のセグメントの数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返します`S_FALSE`ない他のセグメントがある場合。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>参照
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)