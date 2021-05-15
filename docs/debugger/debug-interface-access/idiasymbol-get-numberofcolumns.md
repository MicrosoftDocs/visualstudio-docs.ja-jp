---
description: マトリックス内の列の数を取得します。
title: IDiaSymbol::get_numberOfColumns | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 64834351-e2c9-4f1c-9dc0-2abb5478bc63
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: de5f0a17055b758da56c7af2edec6f8cb2de4157
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635123"
---
# <a name="idiasymbolget_numberofcolumns"></a>IDiaSymbol::get_numberOfColumns
マトリックス内の列の数を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_numberOfColumns(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] マトリックス内の列の数を保持する `DWORD` へのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
