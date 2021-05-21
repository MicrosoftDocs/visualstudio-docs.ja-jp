---
description: 関数に naked 属性がある (つまり、関数にコンパイラによって追加されたプロローグまたはエピローグ コードがない) かどうかを指定するフラグを取得します。
title: IDiaSymbol::get_isNaked | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isNaked method
ms.assetid: b16629dc-8e17-476b-9c7b-58e7277c61ed
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6ec1d273ce826a87ae658f7ed22fe7680edad25d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634678"
---
# <a name="idiasymbolget_isnaked"></a>IDiaSymbol::get_isNaked
関数に [naked](/cpp/cpp/naked-cpp) 属性がある (つまり、関数にコンパイラによって追加されたプロローグまたはエピローグ コードがない) かどうかを指定するフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_isNaked(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[出力] 関数に `naked` 属性がある場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [naked 関数呼び出し](/cpp/cpp/naked-function-calls)
