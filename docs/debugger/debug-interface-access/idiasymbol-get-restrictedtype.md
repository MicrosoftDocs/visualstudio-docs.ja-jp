---
description: このポインターに制限ありのフラグが設定されているかどうかを指定します。
title: IDiaSymbol::get_restrictedType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: c48b00a6-26b0-47b0-b824-fe44dedbc756
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c75e11b4b16f2a8123c833999d7bb793915e2dad
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635236"
---
# <a name="idiasymbolget_restrictedtype"></a>IDiaSymbol::get_restrictedType
`this` ポインターに制限ありのフラグが設定されているかどうかを指定します。

## <a name="syntax"></a>構文

```C++
HRESULT get_restrictedType(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] `this` ポインターに制限ありのフラグが設定されているかどうかを指定する `BOOL` へのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
