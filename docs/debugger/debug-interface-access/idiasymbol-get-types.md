---
description: このシンボルのコンパイラ固有の型の配列を取得します。
title: IDiaSymbol::get_types | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_types method
ms.assetid: 5f056e0c-e15b-4e00-8f78-aadc8574f7ea
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aec5db878c87ba257f1f83458d1ae742272a9b0f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635103"
---
# <a name="idiasymbolget_types"></a>IDiaSymbol::get_types
このシンボルのコンパイラ固有の型の配列を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_types ( 
   DWORD       cTypes,
   DWORD*      pcTypes,
   IDiaSymbol* types[]
);
```

#### <a name="parameters"></a>パラメーター
 `cTypes`

[入力] データを保持するバッファーのサイズ。

 `pcTypes`

[出力] 書き込まれた型の数、または `types` パラメーターが `NULL` の場合、使用可能な型の合計数を返します。

 `types[]`

[出力] このシンボルのすべての型を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを使用して格納される配列。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
