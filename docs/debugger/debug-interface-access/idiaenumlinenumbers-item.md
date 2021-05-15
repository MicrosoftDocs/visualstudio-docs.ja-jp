---
description: インデックスを使って行番号を取得します。
title: IDiaEnumLineNumbers::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Item method
ms.assetid: 08efbeaf-22f7-49e9-96a8-bb906dfe4fd8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6eeea52f2152d1674710d7c5ee2b5970a8cd91cd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634944"
---
# <a name="idiaenumlinenumbersitem"></a>IDiaEnumLineNumbers::Item
インデックスを使って行番号を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   DWORD            index,
   IDiaLineNumber** lineNumber
);
```

#### <a name="parameters"></a>パラメーター
 インデックス

[入力] 取得する [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) オブジェクトのインデックス。 インデックスの範囲は 0 から `count`-1 です。ここで、`count` は [IDiaEnumLineNumbers::get_Count](../../debugger/debug-interface-access/idiaenumlinenumbers-get-count.md) メソッドによって返されます。

 lineNumber

[出力] 目的の行番号を表す [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
