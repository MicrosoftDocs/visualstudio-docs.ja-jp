---
description: インデックスを使ってセクション コントリビューションを取得します。
title: IDiaEnumSectionContribs::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Item method
ms.assetid: 63a28f23-0ca0-44a7-b11b-ca0206d642a0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b39ba7092f163602426aa6194e9109f1db1b4485
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634478"
---
# <a name="idiaenumsectioncontribsitem"></a>IDiaEnumSectionContribs::Item
インデックスを使ってセクション コントリビューションを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   DWORD                index,
   IDiaSectionContrib** section
);
```

#### <a name="parameters"></a>パラメーター
 インデックス

[in] 取得する [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) のインデックス。 インデックスの範囲は、0 から `count`-1 です。ここで、`count` は、[IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md) によって返されます。

 section

[out] 目的のセクション コントリビューションを表す [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
