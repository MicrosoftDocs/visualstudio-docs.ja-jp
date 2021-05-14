---
description: 列挙型シーケンス内の指定された数のセクション コントリビューションをスキップします。
title: IDiaEnumSectionContribs::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Skip method
ms.assetid: 7471a178-5134-41b2-80a6-51ff96abe916
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 345aa9219071a64fdd497a9e5409ee7dab3068ad
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635059"
---
# <a name="idiaenumsectioncontribsskip"></a>IDiaEnumSectionContribs::Skip
列挙型シーケンス内の指定された数のセクション コントリビューションをスキップします。

## <a name="syntax"></a>構文

```C++
HRESULT Skip( 
   ULONG celt
);
```

#### <a name="parameters"></a>パラメーター
 `celt`

[入力] 列挙型シーケンス内のスキップするセクション コントリビューションの数。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合、スキップするセクション コントリビューションがそれ以上なければ、`S_FALSE` を返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
