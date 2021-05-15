---
description: データ シンボルの変数の分類を取得します。
title: IDiaSymbol::get_dataKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_dataKind method
ms.assetid: 45005ad0-8b29-4cde-9d33-6bef72f6e463
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 833ff0fb6602d7f33aabbb9aa1a442bda07a379b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635161"
---
# <a name="idiasymbolget_datakind"></a>IDiaSymbol::get_dataKind
データ シンボルの変数の分類を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_dataKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] たとえば、グローバル、静的、または定数などのデータの種類を示し、[DataKind Enumeration](../../debugger/debug-interface-access/datakind.md) 列挙型から値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [DataKind 列挙型](../../debugger/debug-interface-access/datakind.md)
