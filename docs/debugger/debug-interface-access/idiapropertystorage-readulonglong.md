---
description: プロパティ セット内の ULONGLONG 値を読み取ります。
title: IDiaPropertyStorage::ReadULONGLONG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadULONGLONG
ms.assetid: f80a2e24-5744-4fec-bab0-3ed51aef6e58
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f314152355459ffd2437621efaae002ef284c765
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634374"
---
# <a name="idiapropertystoragereadulonglong"></a>IDiaPropertyStorage::ReadULONGLONG
プロパティ セット内の `ULONGLONG` 値を読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadULONGLONG ( 
   PROPID     id,
   ULONGLONG* pValue
);
```

#### <a name="parameters"></a>パラメーター
 `id`

[入力] 読み取るプロパティの識別子 (`PROPID` は、WTypes.h に `ULONG` として定義されます)。

 `pValue`

[出力] プロパティ値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 プロパティの型が `ULONGLONG` ではない場合、`E_INVALIDARG` を返します。

## <a name="remarks"></a>解説
 `ULONGLONG` は、Windows で、64 ビットの符号なし整数として定義されます。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
