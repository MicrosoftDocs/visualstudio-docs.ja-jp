---
description: シンボルの読み込み元のファイルの名前を取得します。
title: IDiaSymbol::get_symbolsFileName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_symbolsFileName method
ms.assetid: c1aa39ee-d645-431e-bf5f-0640c0998934
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fe20bacc1100fc28258422626e44274813ce7253
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634620"
---
# <a name="idiasymbolget_symbolsfilename"></a>IDiaSymbol::get_symbolsFileName
シンボルの読み込み元のファイルの名前を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_symbolsFileName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] シンボルの読み込み元のファイルの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 このプロパティは、`SymTagExe` の [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)値と共にグローバル スコープも持つシンボルに対してのみ有効です。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
