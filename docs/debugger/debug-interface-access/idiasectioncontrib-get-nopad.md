---
description: セクションを次のメモリ境界に埋め込むことができないかどうかを示すフラグを取得します。
title: IDiaSectionContrib::get_nopad | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_nopad method
ms.assetid: f5c08603-0b3e-4e81-acf1-1b95a6a83bed
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 48bbfdbd14cd7f2d00a9c0ba4530c78fed62141d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634833"
---
# <a name="idiasectioncontribget_nopad"></a>IDiaSectionContrib::get_nopad
セクションを次のメモリ境界に埋め込むことができないかどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_nopad(
   BOOL* pRetVal
};
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] セクションを次のメモリ境界に埋め込むことができない場合は、`TRUE` を返します。それ以外の場合は、`FALSE` を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 これは通常、古いファイルでのみ見られるプロパティです。

## <a name="see-also"></a>関連項目
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
