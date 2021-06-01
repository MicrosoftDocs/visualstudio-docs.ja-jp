---
description: 関数に (setjmp(/cpp/c-runtime-library/reference/setjmp) と組み合わせると、これらは例外処理の C スタイルのメソッドを形成する) longjmp コマンドが使用されているかどうかを示すフラグを取得します。
title: IDiaSymbol::get_hasLongJump | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasLongJump method
ms.assetid: 14484cb1-43b0-47a1-a9a8-081b55566886
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1c211e52e1a8e13a88b6c2a2f9404f5d8a67386f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634698"
---
# <a name="idiasymbolget_haslongjump"></a>IDiaSymbol::get_hasLongJump
関数に ([setjmp](/cpp/c-runtime-library/reference/setjmp) コマンドと組み合わせると、これらは例外処理の C スタイルのメソッドを形成する) [longjmp](/cpp/c-runtime-library/reference/longjmp) コマンドが使用されているかどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_hasLongJump
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[出力] 関数に `longjmp` コマンドが含まれている場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>要件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>こちらもご覧ください
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)
- [longjmp](/cpp/c-runtime-library/reference/longjmp)
- [setjmp](/cpp/c-runtime-library/reference/setjmp)
