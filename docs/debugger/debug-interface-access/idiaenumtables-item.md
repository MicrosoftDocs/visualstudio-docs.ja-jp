---
description: インデックスまたは名前を使用してテーブルを取得します。
title: IDiaEnumTables::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Item method
ms.assetid: d65ab262-10c6-48ce-95a3-b5e4cb2c85af
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dc222672b0ba52f19f153a8e0c9e97137a069607
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634436"
---
# <a name="idiaenumtablesitem"></a>IDiaEnumTables::Item
インデックスまたは名前を使用してテーブルを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   VARIANT     index,
   IDiaTable** table
);
```

#### <a name="parameters"></a>パラメーター
 `index`

[入力] 取得する [IDiaTable](../../debugger/debug-interface-access/idiatable.md) のインデックスまたは名前。 整数バリアントが使用される場合、それは 0 から `count`-1 までの範囲に含まれる必要があります。`count` は、[IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md) メソッドによって返されるものです。

 `table`

[出力] 目的のテーブルを表す [IDiaTable](../../debugger/debug-interface-access/idiatable.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 文字列バリアントが指定されている場合、文字列は特定のテーブルの名前を表します。 名前は、[定数 (Debug Interface Access SDK)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md) で定義されているテーブル名のいずれかである必要があります。

## <a name="example"></a>例

```C++
VARIANT var;
var.vt = VT_BSTR;
var.bstrVal = SysAllocString(DiaTable_Symbols );
IDiaTable* pTable;
pEnumTables->Item( var, &pTable );
```

## <a name="see-also"></a>関連項目
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaEnumTables::get_Count](../../debugger/debug-interface-access/idiaenumtables-get-count.md)
- [定数 (Debug Interface Access SDK)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)
