---
description: サンクの種類を指定します。
title: THUNK_ORDINAL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8d9fe78eedd0166594daf43093aa525e3d8d3e88
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635197"
---
# <a name="thunk_ordinal"></a>THUNK_ORDINAL
サンクの種類を指定します。

## <a name="syntax"></a>構文

```C++
typedef enum THUNK_ORDINAL {
    THUNK_ORDINAL_NOTYPE,
    THUNK_ORDINAL_ADJUSTOR,
    THUNK_ORDINAL_VCALL,
    THUNK_ORDINAL_PCODE,
    THUNK_ORDINAL_LOAD

    // trampoline thunk ordinals - only for use in Trampoline thunk symbols
    THUNK_ORDINAL_TRAMP_INCREMENTAL,
    THUNK_ORDINAL_TRAMP_BRANCHISLAND,
} THUNK_ORDINAL;
```

## <a name="elements"></a>要素
THUNK_ORDINAL_NOTYPE 標準のサンク。

THUNK_ORDINAL_ADJUSTOR `this` を調整するサンク。

THUNK_ORDINAL_VCALL 仮想呼び出しサンク。

THUNK_ORDINAL_PCODE P コード サンク。

THUNK_ORDINAL_LOAD 遅延読み込みサンク。

THUNK_ORDINAL_TRAMP_INCREMENTAL 増分トランポリン サンク (トランポリン サンクは、あるメモリ空間からの呼び出しを別のものにバウンスするために使用します)。

THUNK_ORDINAL_TRAMP_BRANCHISLAND ブランチ ポイント トランポリン サンク。

## <a name="remarks"></a>解説
この列挙の値は、[IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md) メソッドへの呼び出しから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)
