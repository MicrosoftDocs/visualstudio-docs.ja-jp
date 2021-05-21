---
description: シンボルに含まれる場所情報の種類を示します。
title: LocationType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7f111e269f0a61e827a6d1334aee8b9250f3f46f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634567"
---
# <a name="locationtype"></a>LocationType
シンボルに含まれる場所情報の種類を示します。

## <a name="syntax"></a>構文

```C++
enum LocationType {
    LocIsNull,
    LocIsStatic,
    LocIsTLS,
    LocIsRegRel,
    LocIsThisRel,
    LocIsEnregistered,
    LocIsBitField,
    LocIsSlot,
    LocIsIlRel,
    LocInMetaData,
    LocIsConstant,
    LocTypeMax
};
```

## <a name="elements"></a>要素
`LocIsNull`: 場所情報は使用できません。

`LocIsStatic`: 場所は静的です。

`LocIsTLS`: 場所はスレッド ローカル ストレージ内にあります。

`LocIsRegRel`: 場所はレジスタ相対です。

`LocIsThisRel`: 場所は `this` 相対です。

`LocIsEnregistered`: 場所はレジスタ内にあります。

`LocIsBitField`: 場所はビット フィールド内にあります。

`LocIsSlot`: 場所は、Microsoft Intermediate Language (MSIL) スロットです。

`LocIsIlRel`: 場所は MSIL 相対です。

`LocInMetaData`: 場所はメタデータ内にあります。

`LocIsConstant`: 場所は定数値内にあります。

`LocTypeMax`: この列挙型の場所の種類の数。

## <a name="remarks"></a>解説
[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) インターフェイスで使用できるプロパティは、イメージ ファイル内のシンボルの場所によって異なります。 詳細については、「[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」を参照してください。

この列挙型の値は、[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md) メソッドの呼び出しによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)
- [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)
