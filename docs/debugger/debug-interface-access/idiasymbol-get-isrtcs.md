---
description: 関数がスタック フレームの実行時エラー チェックでコンパイルされたかどうかを示す値を取得します。 これは /RTCs フラグです。
title: IDiaSymbol::get_isRTCs | Microsoft Docs
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isRTCs method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a297abe6326af6f04058e6095f59f880f526adb
ms.sourcegitcommit: 30c404655fb83ea28f96ab1edb1c09b4d8d7eec4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "108635450"
---
# <a name="idiasymbolget_isrtcs"></a>IDiaSymbol::get_isRTCs

関数がスタック フレームの実行時エラー チェックでコンパイルされたかどうかを示す値を返します。 これは /RTCs フラグです。

## <a name="syntax"></a>構文

```C++
HRESULT get_isRTCs ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター

 `pRetVal`

[出力] 関数がスタック フレームの実行時エラー チェックでコンパイルされたかどうかを指定する BOOL へのポインター。

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
