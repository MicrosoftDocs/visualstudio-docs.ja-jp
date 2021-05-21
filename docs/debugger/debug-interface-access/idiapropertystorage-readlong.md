---
description: プロパティ セット内の LONG 値を読み取ります。
title: IDiaPropertyStorage::ReadLONG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadLONG
ms.assetid: 32054cbc-db55-4513-a1b4-de80e77aac8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3328048efaad86f987511e390ca2a041161f029a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634376"
---
# <a name="idiapropertystoragereadlong"></a>IDiaPropertyStorage::ReadLONG
プロパティ セット内の `LONG` 値を読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadDLONG ( 
   PROPID id,
   LONG*  pValue
);
```

#### <a name="parameters"></a>パラメーター
 `id`

[入力] 読み取るプロパティの識別子 (`PROPID` は、WTypes.h に `ULONG` として定義されます)。

 `pValue`

[出力] プロパティ値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 プロパティの型が `LONG` ではない場合、`E_INVALIDARG` を返します。

## <a name="remarks"></a>解説
 `LONG` は、Windows で、32 ビットの符号なし整数として定義されます。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
