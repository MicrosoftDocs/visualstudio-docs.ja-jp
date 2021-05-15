---
description: 指定したスタック フレーム内で、指定したスタック アドレスまたはその近くのリターン アドレスを検索します。
title: IDiaStackWalkHelper::searchForReturnAddressStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::searchForReturnAddressStart method
ms.assetid: 0a33142e-5d31-44ea-874a-a2e94d95cbd2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5dfda60c2be8f7900a8b2fc0db54e4801c628bb7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634771"
---
# <a name="idiastackwalkhelpersearchforreturnaddressstart"></a>IDiaStackWalkHelper::searchForReturnAddressStart
指定したスタック フレーム内で、指定したスタック アドレスまたはその近くのリターン アドレスを検索します。

## <a name="syntax"></a>構文

```C++
HRESULT searchForReturnAddressStart( 
   IDiaFrameData*  frame,
   ULONGLONG       startAddress,
   ULONGLONG*      returnAddress
);
```

#### <a name="parameters"></a>パラメーター
 `frame`

[入力] 現在のスタック フレームを表す [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) オブジェクト。

 `startAddress`

[入力] 検索を開始する仮想メモリ アドレス。

 `ReturnAddress`

[出力] `startAddress` に最も近い関数のリターン アドレスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
