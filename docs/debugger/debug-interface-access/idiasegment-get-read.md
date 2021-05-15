---
description: セグメントが読み取り可能かどうかを示すフラグを取得します。
title: IDiaSegment::get_read | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSegment::get_read method
ms.assetid: aafbc86d-352c-4e1a-911a-1472d2d59212
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a1ed49889432d29b8058dcf269549dd31d6f9cf
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634825"
---
# <a name="idiasegmentget_read"></a>IDiaSegment::get_read
セグメントが読み取り可能かどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_read ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] セグメントが読み取リ可能である場合は、`TRUE` を返します。それ以外の場合は、`FALSE` を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
