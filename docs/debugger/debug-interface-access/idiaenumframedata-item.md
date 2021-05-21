---
description: インデックスを使用してフレーム データ要素を取得します。
title: IDiaEnumFrameData::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Item method
ms.assetid: 2761a72d-1868-4f5b-a32e-c2a1d9358c91
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c22983881c6f4e7d1bbb8e25ec6030d85411145c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634501"
---
# <a name="idiaenumframedataitem"></a>IDiaEnumFrameData::Item
インデックスを使用してフレーム データ要素を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   DWORD           index,
   IDiaFrameData** section
);
```

#### <a name="parameters"></a>パラメーター
 インデックス

[入力] 取得する [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) オブジェクトのインデックス。 インデックスの範囲は、0 から `count`-1 です。ここで、`count` は、[IDiaEnumFrameData::get_Count](../../debugger/debug-interface-access/idiaenumframedata-get-count.md) メソッドによって返されます。

 section

[出力] 目的のフレーム データ要素を表す [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
