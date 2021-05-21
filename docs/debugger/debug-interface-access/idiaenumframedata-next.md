---
description: 列挙シーケンス内の指定された数のフレーム データ要素を取得します。
title: IDiaEnumFrameData::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Next method
ms.assetid: 546e2e23-efb2-425a-96a1-808c67c519fb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: adc27c29eedc98375f9feefc8872b5a75b7b219b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634951"
---
# <a name="idiaenumframedatanext"></a>IDiaEnumFrameData::Next
列挙シーケンス内の指定された数のフレーム データ要素を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next ( 
   ULONG           celt,
   IDiaFrameData** rgelt,
   ULONG*          pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 celt

[入力] 取得する列挙子内のフレーム データ要素の数。

 rgelt

[出力] 要求されたフレーム データ要素が入力される [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) オブジェクトの配列。

 pceltFetched

[出力] フェッチされた列挙子内のフレーム データ要素の数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 他にレコードが存在しない場合は `S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
