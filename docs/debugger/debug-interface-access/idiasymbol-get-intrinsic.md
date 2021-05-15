---
description: クラスが組み込み型であるかどうかを指定するフラグを取得します。
title: IDiaSymbol::get_intrinsic | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_intrinsic method
ms.assetid: f969f595-d9f9-48b9-adaa-63a6e4e09575
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bddec7880c69ccc9f4ce0ff20490ef355a71cfbd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634256"
---
# <a name="idiasymbolget_intrinsic"></a>IDiaSymbol::get_intrinsic
クラスが組み込み型であるかどうかを指定するフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_intrinsic( 
   BOOL* pRetVal)
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] クラスが組み込み型の場合は、`TRUE` を返します。それ以外の場合は、`FALSE` を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
