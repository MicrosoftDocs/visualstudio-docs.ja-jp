---
description: この関数は、関数が (inline、_inline、_forceinline 属性のいずれかを使用して) インラインとしてマークされたかどうかを示すフラグを取得します。
title: IDiaSymbol::get_InlSpec | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_InlSpec method
ms.assetid: 30af6a2f-be84-429e-a96a-d0f9ed9343fb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f727e83d067fed37698eb750bb39309a9454535a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635142"
---
# <a name="idiasymbolget_inlspec"></a>IDiaSymbol::get_InlSpec
この関数は、関数が ([inline、_inline、\__forceinline](/cpp/cpp/inline-functions-cpp) 属性のいずれかを使用して) インラインとしてマークされたかどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_inlSpec(
   BOOL *pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] 関数がインラインとしてマークされている場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [inline、__inline、\__forceinline](/cpp/cpp/inline-functions-cpp)
