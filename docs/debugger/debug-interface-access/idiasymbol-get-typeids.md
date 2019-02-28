﻿---
title: Idiasymbol::get_typeids |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeIds method
ms.assetid: 5166e647-fde5-4efe-92bf-77f8ae3fbc9b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 12024a3a024f2c9433e144790c0a513d4e33df12
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56643744"
---
# <a name="idiasymbolgettypeids"></a>IDiaSymbol::get_typeIds
このシンボルのコンパイラ固有の型識別子の値の配列を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_typeIds ( 
   DWORD  cTypeIds,
   DWORD* pcTypeIds,
   DWORD  typeIds[]
);
```

#### <a name="parameters"></a>パラメーター
 `cTypeIds`

[in]データを保持するバッファーのサイズ。

 `pcTypeIds`

[out]数を返します`typeIds`書き込まれると、または、`typeIds`は`NULL`、使用可能な型識別子の総数、します。

 `typeIds[]`

[out]型識別子を使用して格納する配列。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。

> [!NOTE]
>  戻り値`S_FALSE`プロパティが、シンボルの使用可能なことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
