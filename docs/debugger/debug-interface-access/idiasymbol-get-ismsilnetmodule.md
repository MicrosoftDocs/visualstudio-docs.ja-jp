---
description: モジュールが .netmodule (メタデータのみを含み、ネイティブ シンボルは含まない Microsoft 中間言語 (MSIL) のモジュール) かどうかを示すフラグを取得します。
title: IDiaSymbol::get_isMSILNetmodule | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isMSILNetmodule method
ms.assetid: 593827f3-8437-4a12-ada4-ff715ec95fb2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 27d1294e5cbced8cd2f521a25858a37efe9f5b8c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635126"
---
# <a name="idiasymbolget_ismsilnetmodule"></a>IDiaSymbol::get_isMSILNetmodule
モジュールが .netmodule (メタデータのみを含み、ネイティブ シンボルは含まない Microsoft 中間言語 (MSIL) のモジュール) かどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_isMSILNetmodule(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[出力] モジュールが MSIL の場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 このプロパティは、`SymTagCompilandDetails` のシンボルの種類で使用できます (「[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)」を参照してください)。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)
