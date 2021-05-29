---
description: 関数のサンク型を取得します。
title: IDiaSymbol::get_thunkOrdinal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thunkOrdinal method
ms.assetid: 4b28d78a-1974-4d8a-8bb7-781bf630f2f4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: de9b0fa692ff44096e962bc952b91c3f2fd314f2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635105"
---
# <a name="idiasymbolget_thunkordinal"></a>IDiaSymbol::get_thunkOrdinal
関数のサンク型を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_thunkOrdinal ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] 関数のサンク型を指定する [THUNK_ORDINAL 列挙型](../../debugger/debug-interface-access/thunk-ordinal.md)の列挙体から値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 このプロパティは、シンボルが `SymTagThunk` の [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値である場合にのみ有効です。

 "サンク" とは、32 ビットのメモリ アドレス空間 (フラット アドレス空間とも呼ばれる) と 16 ビットのアドレス空間 (セグメント化されたアドレス空間とも呼ばれる) との間の変換を行うコードです。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [THUNK_ORDINAL 列挙型](../../debugger/debug-interface-access/thunk-ordinal.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
