---
description: 指定されたプロパティ識別子に対応する文字列名を取得します。
title: IDiaPropertyStorage::ReadPropertyNames | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadPropertyNames
ms.assetid: f8bcab77-afca-4a8f-8710-697842f8a518
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cbb6d511a6be9ed408b076162a3d00d22705075a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634373"
---
# <a name="idiapropertystoragereadpropertynames"></a>IDiaPropertyStorage::ReadPropertyNames
指定されたプロパティ識別子に対応する文字列名を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT ReadPropertyNames (
   ULONG         cpropid,
   PROPID const* rgpropid,
   BSTR*         rglpwstrName
);
```

#### <a name="parameters"></a>パラメーター
 `cpropid`

[入力] `rgpropid` に格納されているプロパティ ID の数。

 `rgpropid`

[入力] 名前を取得するプロパティ ID の配列 (`PROPID` は、WTypes.h で `ULONG` として定義されています)。

 `rglpwstrName`

[入力、出力] 指定されたプロパティ ID に対するプロパティ名の配列。 要求する数のプロパティ名を保持するための配列を、事前に割り当てておく必要があり、この配列は少なくとも `cpropid``BSTR` 個の文字列を保持できる必要があります。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 返されたプロパティ名は、不要になったら (`SysFreeString` 関数を呼び出すことによって) 解放する必要があります。

## <a name="see-also"></a>関連項目
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
