---
description: this ポインターが、単一継承を持つデータ メンバーをポイントしているかどうかを示します。
title: IDiaSymbol::get_isSingleInheritance | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 46cde656-059b-4c20-9476-3ca68ccc9912
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: 657c677e9415b64f0a42c0ece2ba8847cca9ed51
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635125"
---
# <a name="idiasymbolget_issingleinheritance"></a>IDiaSymbol::get_isSingleInheritance
`this` ポインターが、単一継承を持つデータ メンバーをポイントしているかどうかを示します。

## <a name="syntax"></a>構文

```C++
HRESULT get_isSingleInheritance(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] `this` ポインターが、単一継承を持つデータ メンバーをポイントしているかどうかを示す `BOOL` へのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
