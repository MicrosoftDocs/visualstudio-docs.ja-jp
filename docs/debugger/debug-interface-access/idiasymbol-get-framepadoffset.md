---
description: フレーム ポインター レジスタからスタック パッドのオフセットを取得します。
title: IDiaSymbol::get_framePadOffset | Microsoft Docs
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePadOffset method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 455e617188a58090f3bd6229ab008847912b1f19
ms.sourcegitcommit: 30c404655fb83ea28f96ab1edb1c09b4d8d7eec4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "108635451"
---
# <a name="idiasymbolget_framepadoffset"></a>IDiaSymbol::get_framePadOffset

フレーム ポインター レジスタからスタック パッドのオフセットを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_framePadOffset ( 
   DWORD* pPadOffset
);
```

#### <a name="parameters"></a>パラメーター

 `pPadOffset`

[出力] スタック パッドのオフセットを返します。

## <a name="return-value"></a>戻り値

 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説

このメソッドは、Visual Studio 2019 バージョン 16.10 Preview 2 以降でサポートされています。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
