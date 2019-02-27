---
title: Idiasymbol::get_container |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_container method
ms.assetid: 24e832eb-80b3-484c-a41b-11477ec9de99
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ca0b183f0616705ec61475c4570fa11ce89640d
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56622281"
---
# <a name="idiasymbolgetcontainer"></a>IDiaSymbol::get_container
この関数は、この記号の親/コンテナーを表すシンボルへのポインターを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_container(
   IDiaSymbol **pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out]ポインターを返します、`IDiaSymbol`このシンボルのコンテナーに関する情報を格納します。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、S_FALSE またはエラー コードを返します。

> [!NOTE]
>  S_FALSE の戻り値は、プロパティがシンボルを使用できないことを意味します。

## <a name="requirements"></a>要件

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK バージョン 8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)