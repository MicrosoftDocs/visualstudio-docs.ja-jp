---
description: 外側の関数のフレーム データ インターフェイスを取得します。
title: IDiaFrameData::get_functionParent | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_functionParent method
ms.assetid: f00b9ab1-d4da-4818-973a-58f8f0e66769
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c03eb86e7575652fd260aa9a7018081992b78010
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634909"
---
# <a name="idiaframedataget_functionparent"></a>IDiaFrameData::get_functionParent
外側の関数のフレーム データ インターフェイスを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_functionParent ( 
   IDiaFrameData** pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] 外側の関数の [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
