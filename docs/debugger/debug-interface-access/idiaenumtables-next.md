---
description: 列挙体シーケンス内の指定した数のテーブルを取得します。
title: IDiaEnumTables::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Next method
ms.assetid: 8d7bd359-d33e-4317-9674-d89283efd7de
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fdc207633a083e841221e3c6ca527c7ffb3dbcf7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634928"
---
# <a name="idiaenumtablesnext"></a>IDiaEnumTables::Next
列挙体シーケンス内の指定した数のテーブルを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next ( 
   ULONG       celt,
   IDiaTable** rgelt,
   ULONG*      pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 `celt`

[入力] 取得する列挙子内のテーブルの数。

 `rgelt`

[出力] 目的のテーブルを表す [IDiaTable](../../debugger/debug-interface-access/idiatable.md) オブジェクトを入力する配列。

 `pceltFetched`

[出力] フェッチされた列挙子内のテーブルの数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 テーブルがそれ以上ない場合は `S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
