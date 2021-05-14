---
description: ソースの言語を取得します。
title: IDiaSymbol::get_language | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_language method
ms.assetid: c759ad3c-1c21-4234-869b-86aa3a608a38
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 50d4ee9899b7d625a18babc3551d41b4e2ddc8bc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635259"
---
# <a name="idiasymbolget_language"></a>IDiaSymbol::get_language
ソースの言語を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_language ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] [CV_CFL_LANG 列挙型](../../debugger/debug-interface-access/cv-cfl-lang.md)に関するページにある列挙型から、ソースの言語を指定する値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CV_CFL_LANG 列挙型](../../debugger/debug-interface-access/cv-cfl-lang.md)
