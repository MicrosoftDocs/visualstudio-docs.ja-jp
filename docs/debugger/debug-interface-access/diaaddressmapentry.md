---
description: アドレス マップのエントリを記述します。
title: DiaAddressMapEntry | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bdac0233901ac8571bbfb2a5d6659adf69e35298
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634521"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
アドレス マップのエントリを記述します。

## <a name="syntax"></a>構文

```C++
struct DiaAddressMapEntry {
    DWORD rva,
    DWORD rvaTo
};
```

## <a name="elements"></a>要素
`rva` イメージ A の相対仮想アドレス (RVA)。

`rvaTo` 相対仮想アドレス `rva` はイメージ B 内にマップされます。

## <a name="remarks"></a>解説
アドレス マップにより、あるイメージ レイアウト (A) から別のイメージ レイアウト (B) への変換が提供されます。 `rva` によって並べ替えられた `DiaAddressMapEntry` 構造体の配列により、アドレス マップが定義されます。

イメージ A 内のアドレス `addrA` をイメージ B 内のアドレス `addrB` に変換するには、次の手順を実行します。

1. `addrA` 以下で最大の `rva` を持つエントリ `e` をマップで検索します。

2. `delta = addrA - e.rva` を設定します。

3. `addrB = e.rvaTo + delta` を設定します。

    `DiaAddressMapEntry` 構造体の配列を、[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) メソッドに渡します。

## <a name="requirements"></a>必要条件
ヘッダー: dia2.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
