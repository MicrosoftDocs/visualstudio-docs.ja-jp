---
description: 指定した仮想アドレスを含むシンボルを取得します。
title: IDiaStackWalkHelper::symbolForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::symbolForVA method
ms.assetid: 8dd9455d-d44c-4dd6-a0aa-31131cbea2aa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4f75ba05573c5c41baea3ab24ec5b7d06c916c0e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634769"
---
# <a name="idiastackwalkhelpersymbolforva"></a>IDiaStackWalkHelper::symbolForVA
指定した仮想アドレスを含むシンボルを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT symbolForVA( 
   ULONGLONG     va,
   IDiaSymbol**  ppSymbol
);
```

#### <a name="parameters"></a>パラメーター
 `va`

[入力] 要求されたシンボルに含まれている仮想アドレス。 このシンボルは、`SymTagFunctionType` ([Symtagenum 列挙型](../../debugger/debug-interface-access/symtagenum.md)列挙の値) である必要があります。

 `ppSymbol`

[出力] 指定したアドレスにあるシンボルを表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
