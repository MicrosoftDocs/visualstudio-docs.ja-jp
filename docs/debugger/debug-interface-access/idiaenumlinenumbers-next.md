---
description: 列挙シーケンス内の指定された数の行番号を取得します。
title: IDiaEnumLineNumbers::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Next method
ms.assetid: 363d5b40-1316-4ab8-836f-63637f619e0a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9301c10634919774b8253eea77dba6acdd3c324a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634939"
---
# <a name="idiaenumlinenumbersnext"></a>IDiaEnumLineNumbers::Next
列挙シーケンス内の指定された数の行番号を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next ( 
   ULONG            celt,
   IDiaLineNumber** rgelt,
   ULONG*           pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 celt

[入力] 取得する列挙子内の行番号の数。

 rgelt

[出力] 目的の行番号を表す [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) オブジェクトの配列を返します。

 pceltFetched

[出力] フェッチされた列挙子内の行番号の数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 行番号がそれ以上ない場合は `S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
