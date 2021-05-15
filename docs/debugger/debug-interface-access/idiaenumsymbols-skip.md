---
description: 列挙型シーケンス内の指定された数のシンボルをスキップします。
title: IDiaEnumSymbols::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::Skip method
ms.assetid: e601fbc9-b10b-41c7-8180-959e57efabe8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e3a8088353dcfe13974989b84960c513afda0bb5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635028"
---
# <a name="idiaenumsymbolsskip"></a>IDiaEnumSymbols::Skip
列挙型シーケンス内の指定された数のシンボルをスキップします。

## <a name="syntax"></a>構文

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>パラメーター
 celt

[入力] 列挙型シーケンス内のスキップするシンボルの数。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合、スキップするシンボルがそれ以上なければ、`S_FALSE` を返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
