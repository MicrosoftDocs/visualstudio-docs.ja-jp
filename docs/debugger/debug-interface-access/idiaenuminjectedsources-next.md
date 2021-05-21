---
description: 列挙シーケンス内の指定された数の挿入されたソースを取得します。
title: IDiaEnumInjectedSources::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources::Next method
ms.assetid: 38af80fc-748f-4b15-bff1-823db21dd4d0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bdc57bd1b15150b93e8c42537e5a4abed8dfae57
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634946"
---
# <a name="idiaenuminjectedsourcesnext"></a>IDiaEnumInjectedSources::Next
列挙シーケンス内の指定された数の挿入されたソースを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next ( 
   ULONG                celt,
   IDiaInjectedSource** rgelt,
   ULONG*               pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 celt

[入力] 取得する列挙子内の挿入されたソースの数。

 rgelt

[出力] 目的の挿入されたソースを表す [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) オブジェクトの配列を返します。

 pceltFetched

[出力] フェッチされた列挙子内の挿入されたソースの数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 挿入されたソースがそれ以上ない場合は `S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
