---
description: プロパティ セット内の BSTR 値を読み取ります。
title: IDiaPropertyStorage::ReadBSTR | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBSTR
ms.assetid: 7214643b-3286-48ed-90aa-0fe95b4cae5b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9702603dd12ea1f88a194ae8af36b5a29ff53c1a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634378"
---
# <a name="idiapropertystoragereadbstr"></a>IDiaPropertyStorage::ReadBSTR
プロパティ セット内の `BSTR` 値を読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadBSTR ( 
   PROPID id,
   BSTR*  pValue
);
```

#### <a name="parameters"></a>パラメーター
 `id`

[in] 読み取るプロパティの識別子 (`PROPID` は、WTypes.h で `ULONG` として定義されます)。

 `pValue`

[out] プロパティ値を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 プロパティが型 `BSTR` ではない場合、`E_INVALIDARG` を返します。

## <a name="remarks"></a>解説
 `BSTR` は、Windows によって、0 で終わるワイド文字として定義されます。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
