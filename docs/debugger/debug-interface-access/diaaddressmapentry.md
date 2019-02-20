---
title: DiaAddressMapEntry |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b472c52934353e6324d72077f8ea878467159cbd
ms.sourcegitcommit: 752f03977f45169585e407ef719450dbe219b7fc
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56318642"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
アドレス マップ内のエントリについて説明します。

## <a name="syntax"></a>構文

```C++
struct DiaAddressMapEntry {
    DWORD rva,
    DWORD rvaTo
};
```

## <a name="elements"></a>Elements
`rva`  
A. イメージの相対仮想アドレス (RVA)

`rvaTo`  
相対仮想アドレス`rva`B. イメージ内にマップされます

## <a name="remarks"></a>解説
アドレス マップは、(A) をもう 1 つ (B) 1 つのイメージのレイアウトからの翻訳を提供します。 配列の`DiaAddressMapEntry`構造体の順に並べ替えて`rva`アドレス マップを定義します。

アドレスに変換する`addrA`、イメージ アドレス内`addrB`B の図で、次の手順に従います。

1. マップのエントリを検索`e`が大きいもの`rva`に等しいまたはそれよりも小さい`addrA`します。

2. `delta = addrA - e.rva` を設定します。

3. `addrB = e.rvaTo + delta` を設定します。

    配列の`DiaAddressMapEntry`に構造体が渡される、 [idiaaddressmap::set_addressmap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)メソッド。

## <a name="requirements"></a>要件
ヘッダー: dia2.h

## <a name="see-also"></a>参照
[列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)  
[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
