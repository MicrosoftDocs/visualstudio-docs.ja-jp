---
title: Idiasymbol::get_issplitted |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isSplitted method
ms.assetid: ff160cf6-003b-4ef5-a406-20a7b287b2bf
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee91134997dad5f5361de6b07af1a99dfc420f5e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "64794591"
---
# <a name="idiasymbolgetissplitted"></a>IDiaSymbol::get_isSplitted
データ シンボルが、集計またはその他の記号のコレクションに分割されて かどうかを指定するフラグを取得します。コンパイラは、非常に大規模なシンボルの一部である場合でも、個別のエンティティとしてシンボルを扱います。

## <a name="syntax"></a>構文

```C++
HRESULT get_isSplitted(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[out]返します`TRUE`場合は、シンボルをシンボルの集計に分割されていますが、それ以外の場合を返します`FALSE`します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。

> [!NOTE]
> 戻り値`S_FALSE`プロパティが、シンボルの使用可能なことを意味します。

## <a name="remarks"></a>Remarks
 [Idiasymbol::get_isaggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)メソッドを返します。`TRUE`分割シンボルの一部であるすべてのシンボルです。

## <a name="requirements"></a>必要条件

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|Dia2.h|
|バージョン:|DIA SDK バージョン 8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)