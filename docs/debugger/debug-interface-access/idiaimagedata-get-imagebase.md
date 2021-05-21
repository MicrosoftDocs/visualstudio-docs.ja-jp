---
description: イメージのベースとなるメモリの場所を取得します。
title: IDiaImageData::get_imageBase | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData::get_imageBase method
ms.assetid: 4ba3d9e4-b205-4ee6-a41d-6996972f1f85
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 82f80f95689a176118d5be6dcc5cfe4fdb903e0f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634418"
---
# <a name="idiaimagedataget_imagebase"></a>IDiaImageData::get_imageBase
イメージのベースとなるメモリの場所を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_imageBase ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] 推奨されるイメージ ベース値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 イメージ ベースの競合により、イメージは、読み込み時に、未使用のメモリの場所に自動的に再配置される場合があります。 このメソッドからは、コンパイル時にモジュールに格納された、ベースに関するヒント (推奨されるメモリの場所) が返されます。

## <a name="see-also"></a>関連項目
- [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)
