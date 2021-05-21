---
description: 別のシンボルからこのシンボルのアドレスが参照されているかどうかを示すフラグを取得します。
title: IDiaSymbol::get_addressTaken | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressTaken method
ms.assetid: 0d366188-f5e1-4226-b392-58c09539d097
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2db653509b0afa40f3b59e1a4a6232763da6ef1f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634740"
---
# <a name="idiasymbolget_addresstaken"></a>IDiaSymbol::get_addressTaken
別のシンボルからこのシンボルのアドレスが参照されているかどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_addressTaken ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] 別のシンボルからこのアドレスが参照されている場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="example"></a>例
 次の例では、`B` から `A` が参照されています。 そのため、シンボル `A` の `get_addressTaken` メソッドにより、`TRUE` が返されます。

```C++
int A  = 0;
int* B = &A;
```

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
