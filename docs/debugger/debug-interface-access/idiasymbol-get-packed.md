---
description: ユーザー定義のデータ型 (UDT) がパックされているかどうかを示すフラグを取得します。
title: IDiaSymbol::get_packed | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_packed method
ms.assetid: e42ff368-56c4-49a2-8676-f80e349efa21
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a5e6cf89aa0bdd31b826ac8e73000c1bfa8c595c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635246"
---
# <a name="idiasymbolget_packed"></a>IDiaSymbol::get_packed
ユーザー定義のデータ型 (UDT) がパックされているかどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_packed ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] UDT がパックされている場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 "パック済み" は、UDT のすべてのメンバーができるだけ近い場所に配置されることを意味し、メモリ境界に合わせるための埋め込みは行われません。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
