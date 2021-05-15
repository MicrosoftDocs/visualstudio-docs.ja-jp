---
description: メソッドの論理 this adjustor を取得します。
title: IDiaSymbol::get_thisAdjust | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thisAdjust method
ms.assetid: 56b9a147-e8c0-4d4b-a42a-398214dd5f86
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cedb234c324f08f9de0a8c51abd5609b6b061612
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634605"
---
# <a name="idiasymbolget_thisadjust"></a>IDiaSymbol::get_thisAdjust
メソッドの論理 `this` adjustor を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_thisAdjust ( 
   LONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] メソッドの論理 `this` adjustor を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 複数の継承ケースでは、メソッド自体が `this` にオフセットを追加することによって true 値を計算する必要があり `this` ます。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
