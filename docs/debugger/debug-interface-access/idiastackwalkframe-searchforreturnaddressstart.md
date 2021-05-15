---
description: 指定されたスタック フレーム内で、指定されたアドレスまたはその近くのリターン アドレスを検索します。
title: IDiaStackWalkFrame::searchForReturnAddressStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::searchForReturnAddressStart method
ms.assetid: 47660b9b-6e4f-4dfa-88ab-63dce28f7412
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 49beac1d7f7c998b5ad3a73222903830a934bc9c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635004"
---
# <a name="idiastackwalkframesearchforreturnaddressstart"></a>IDiaStackWalkFrame::searchForReturnAddressStart
指定されたスタック フレーム内で、指定されたアドレスまたはその近くのリターン アドレスを検索します。

## <a name="syntax"></a>構文

```C++
HRESULT searchForReturnAddressStart ( 
   IDiaFrameData* frame,
   ULONGLONG      startAddress,
   ULONGLONG*     returnAddress
);
```

#### <a name="parameters"></a>パラメーター
 `frame`

[入力] 現在のスタック フレームを表す [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) オブジェクト。

 `startAddress`

[入力] 検索を開始する仮想メモリ アドレス。

 `returnAddress`

[出力] `startAddress` に最も近い関数のリターン アドレスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
