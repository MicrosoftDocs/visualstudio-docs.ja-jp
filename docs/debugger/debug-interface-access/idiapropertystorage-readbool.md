---
description: プロパティ セット内の BOOL 値を読み取ります。
title: IDiaPropertyStorage::ReadBOOL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBOOL
ms.assetid: ad1822db-4572-48f7-9919-f8137f6701f2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3a279cf7d8af13751a8464b5bccae1fd0b8a0acb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634380"
---
# <a name="idiapropertystoragereadbool"></a>IDiaPropertyStorage::ReadBOOL
プロパティ セット内の `BOOL` 値を読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadBOOL ( 
   PROPID id,
   BOOL*  pValue
);
```

#### <a name="parameters"></a>パラメーター
 `id`

[入力] 読み取るプロパティの識別子 (`PROPID` は、WTypes.h に `ULONG` として定義されます)。

 `pValue`

[出力] プロパティ値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 プロパティの型が `BOOL` ではない場合、`E_INVALIDARG` を返します。

## <a name="remarks"></a>解説
 一貫した結果を得るには、0 以外の値が `TRUE` で、0 が `FALSE` になるように、`BOOL` 値を解釈します。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
