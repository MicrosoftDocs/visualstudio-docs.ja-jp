---
description: OEM (相手先ブランド供給) のシンボルの ID 値を取得します。
title: IDiaSymbol::get_oemSymbolId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_oemSymbolId method
ms.assetid: 187801f0-bd82-4c5b-9fae-8eeb1a4ac0ce
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bd7ce01dea21a8d9fe2886fb5fe7b4277f458636
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634641"
---
# <a name="idiasymbolget_oemsymbolid"></a>IDiaSymbol::get_oemSymbolId
OEM (相手先ブランド供給) のシンボルの ID 値を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_oemSymbolId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] OEM が内部で割り当てたシンボルの ID を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 識別子は、すべてのシンボルを一意としてマークするために DIA SDK によって作成される一意の値です。

 このプロパティは、[Symtagenum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の型が `SymTagCustomType` のシンボルにのみ適用されます。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
