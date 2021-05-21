---
description: この関数を使用すると、このシンボルの親またはコンテナーを表すシンボルへのポインターを取得できます。
title: IDiaSymbol::get_container | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_container method
ms.assetid: 24e832eb-80b3-484c-a41b-11477ec9de99
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 724127e50708585613175b0f5773f231f1b33944
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634708"
---
# <a name="idiasymbolget_container"></a>IDiaSymbol::get_container
この関数を使用すると、このシンボルの親またはコンテナーを表すシンボルへのポインターを取得できます。

## <a name="syntax"></a>構文

```C++
HRESULT get_container(
   IDiaSymbol **pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] このシンボルのコンテナーに関する情報を含む `IDiaSymbol` へのポインターを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、S_FALSE またはエラー コードを返します。

> [!NOTE]
> 戻り値 S_FALSE は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
