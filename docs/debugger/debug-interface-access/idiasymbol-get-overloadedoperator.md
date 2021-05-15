---
description: ユーザー定義のデータ型にオーバーロードされた演算子があるかどうかを指定するフラグを取得します。
title: IDiaSymbol::get_overloadedOperator | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_overloadedOperator method
ms.assetid: 257a9894-e980-47ae-bdc0-c5e2293ea734
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c30cfd825379e88293aa8f32b9b994798ea5f8a8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634636"
---
# <a name="idiasymbolget_overloadedoperator"></a>IDiaSymbol::get_overloadedOperator
ユーザー定義のデータ型にオーバーロードされた演算子があるかどうかを指定するフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_overloadedOperator ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] ユーザー定義のデータ型にオーバーロードされた演算子がある場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
