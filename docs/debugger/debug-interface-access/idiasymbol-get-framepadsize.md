---
description: 各関数に追加された必要以上のパッドのサイズを取得します。
title: IDiaSymbol::get_framePadSize | Microsoft Docs
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePadSize method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d361ec3e144730e49345d3560f815ee5fe0be469
ms.sourcegitcommit: 30c404655fb83ea28f96ab1edb1c09b4d8d7eec4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "108635449"
---
# <a name="idiasymbolget_framepadsize"></a>IDiaSymbol::get_framePadSize

各関数に追加された必要以上のパッドのサイズを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_framePadSize ( 
   DWORD* pPadSize
);
```

#### <a name="parameters"></a>パラメーター

 `pPadSize`

[出力] 各関数に追加された必要以上のパッドのサイズを返します。

## <a name="return-value"></a>戻り値

 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説

必要以上のパッドのサイズは通常、エディット コンティニュで使用されます。

このメソッドは、Visual Studio 2019 バージョン 16.10 Preview 2 以降でサポートされています。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
