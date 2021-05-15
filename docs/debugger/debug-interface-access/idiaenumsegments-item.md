---
description: インデックスを使ってセグメントを取得します。
title: IDiaEnumSegments::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Item method
ms.assetid: ee44dd55-39a0-4b7b-97ff-2e1226eeb2bd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a8714964bdf2e267e9f9c047fb1878655e58f489
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634475"
---
# <a name="idiaenumsegmentsitem"></a>IDiaEnumSegments::Item
インデックスを使ってセグメントを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   DWORD         index,
   IDiaSegment** segment
);
```

#### <a name="parameters"></a>パラメーター
 インデックス

[in] 取得する [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) オブジェクトのインデックス。 インデックスの範囲は、0 から `count`-1 です。ここで、`count` は、[IDiaEnumSegments::get_Count](../../debugger/debug-interface-access/idiaenumsegments-get-count.md) によって返されます。

 segment

[out] 目的のセグメントを表す [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
