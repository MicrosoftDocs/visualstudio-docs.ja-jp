---
description: プライベート シンボルがシンボル ファイルから削除されたかどうかを示すフラグを取得します。
title: IDiaSymbol::get_isStripped | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isStripped method
ms.assetid: cc2c4a0b-ab9f-4b79-a8ff-a3badb0405d6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aa52f28bf31a8bd13d9f45ce8554696c91961340
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635263"
---
# <a name="idiasymbolget_isstripped"></a>IDiaSymbol::get_isStripped
プライベート シンボルがシンボル ファイルから削除されたかどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_isStripped(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[出力] プライベート シンボルがシンボル ファイルから削除された場合は `TRUE` を返します。それ以外の場合、`FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 このプロパティは、`SymTagExe` のシンボルの種類で使用できます (「[Exe](../../debugger/debug-interface-access/exe.md)」を参照してください)。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Exe](../../debugger/debug-interface-access/exe.md)
