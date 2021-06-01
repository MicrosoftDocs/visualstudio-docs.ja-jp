---
title: 定数 (Debug Interface Access SDK) | Microsoft Docs
description: Debug Interface Access (DIA) SDK を使用してプログラム デバッグ データベース (PDB) ファイルのさまざまなセクションを識別するために使用できる文字列定数の一覧をご覧ください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- constants, DIA SDK
- DIA SDK, constants
ms.assetid: aca4ec77-bc08-4cdd-a6ce-8d4a28ea5ea3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 89af4172a09631cfc63065cd5c49144c42d41a6d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634217"
---
# <a name="constants-debug-interface-access-sdk"></a>定数 (Debug Interface Access SDK)
これらの文字列定数は、DIA SDK を使用してプログラム デバッグ データベース (PDB) ファイルのさまざまなセクションを識別するために使用できます。

## <a name="constants"></a>定数
次のものは C/C++ マクロとして宣言されています。

|マクロ|値|
|-----------|-----------|
|`DiaTable_Symbols`|L"Symbols"|
|`DiaTable_Sections`|L"Sections"|
|`DiaTable_SrcFiles`|L"SourceFiles"|
|`DiaTable_LineNums`|L"LineNumbers"|
|`DiaTable_SegMap`|L"SegmentMap"|
|`DiaTable_Dbg`|L"Dbg"|
|`DiaTable_InjSrc`|L"InjectedSource"|
|`DiaTable_FrameData`|L"FrameData"|

## <a name="example"></a>例
次に、これらのシンボルのいずれかを使用する例を示します。

```C++
HRESULT GetSymbolTable(IDiaEnumTables *pEnumTables, IDiaTable **pTable)
{
    HRESULT hr;
    VARIANT var;
    var.vt      = VT_BSTR;
    var.bstrVal = SysAllocString( DiaTable_Symbols );
    hr = pEnumTables->Item( var, pTable );
    return(hr);
}
```

## <a name="requirements"></a>必要条件
ヘッダー: dia2.h

## <a name="see-also"></a>関連項目
- [参照](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
