---
description: 列挙シーケンス内の指定した数のセグメントを取得します。
title: IDiaEnumSegments::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Next method
ms.assetid: 53f61874-d821-47ab-a1f5-27e982804a6a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 95d4ac6d566033472d7769e4a1a5df86cdf7ff70
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635048"
---
# <a name="idiaenumsegmentsnext"></a>IDiaEnumSegments::Next
列挙シーケンス内の指定した数のセグメントを取得します。

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

[入力] 取得する列挙子内のセグメントの数。

 rgelt

[出力] そのセグメントを表す目的の [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) オブジェクトを使用して格納する配列。

 pceltFetched

[出力] フェッチされた列挙子内のセグメントの数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 セグメントがそれ以上ない場合は `S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
