---
description: このシンボルについてコンパイラ固有の型識別子の値の配列を取得します。
title: IDiaSymbol::get_typeIds | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeIds method
ms.assetid: 5166e647-fde5-4efe-92bf-77f8ae3fbc9b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 04a39af21ebb8a409656bd8b8ae0b4323da33c60
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634601"
---
# <a name="idiasymbolget_typeids"></a>IDiaSymbol::get_typeIds
このシンボルについてコンパイラ固有の型識別子の値の配列を取得します。

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

[入力] データを保持するバッファーのサイズ。

 `pcTypeIds`

[出力] 書き込まれた `typeIds` の数を返します。または、`typeIds` が `NULL` の場合は、使用可能な型識別子の総数を返します。

 `typeIds[]`

[出力] 型識別子が格納される配列。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
