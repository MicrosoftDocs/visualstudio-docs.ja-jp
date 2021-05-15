---
description: 行列またはストライド配列のストライドを取得します。
title: IDiaSymbol::get_stride | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 4264742a-3d91-44b9-9d14-87adbc77f0f0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 331949c4b37c6e4f472bc2d1f5d805d7a9f7426a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634232"
---
# <a name="idiasymbolget_stride"></a>IDiaSymbol::get_stride
行列またはストライド配列のストライドを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_stride(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] ストライドを保持する `DWORD` へのポインター。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
