---
description: 列挙型シーケンス内の指定された数のフレーム データ要素をスキップします。
title: IDiaEnumFrameData::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Skip method
ms.assetid: 67140b4c-7125-4895-932d-42412326da29
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e2fe993c524a846545a13ab14787c9c6fd5c92e0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634950"
---
# <a name="idiaenumframedataskip"></a>IDiaEnumFrameData::Skip
列挙型シーケンス内の指定された数のフレーム データ要素をスキップします。

## <a name="syntax"></a>構文

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>パラメーター
 celt

[入力] 列挙型シーケンス内のスキップするフレーム データ要素の数。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合、スキップするレコードがそれ以上なければ、`S_FALSE` を返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
