---
description: プロパティ セット内の DWORD 値を読み取ります。
title: IDiaPropertyStorage::ReadDWORD | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadDWORD
ms.assetid: 5f4c034e-a9d3-4560-94b5-ede524741439
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 70eb083c3b4469037195334a0bbfa3784462c89e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634377"
---
# <a name="idiapropertystoragereaddword"></a>IDiaPropertyStorage::ReadDWORD
プロパティ セット内の `DWORD` 値を読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadDWORD ( 
   PROPID id,
   DWORD* pValue
);
```

#### <a name="parameters"></a>パラメーター
 `id`

[in] 読み取るプロパティの識別子 (`PROPID` は、WTypes.h で `ULONG` として定義されます)。

 `pValue`

[out] プロパティ値を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 プロパティが型 `DWORD` ではない場合、`E_INVALIDARG` を返します。

## <a name="remarks"></a>解説
 `DWORD` は、Windows によって、32 ビットの符号なし整数として定義されます。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
