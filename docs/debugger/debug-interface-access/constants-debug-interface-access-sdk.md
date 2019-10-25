---
title: 定数 (Debug Interface Access SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- constants, DIA SDK
- DIA SDK, constants
ms.assetid: aca4ec77-bc08-4cdd-a6ce-8d4a28ea5ea3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b10ab87f056bc153ec41c125b0e01ddefa139b80
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745399"
---
# <a name="constants-debug-interface-access-sdk"></a>定数 (Debug Interface Access SDK)
これらの文字列定数を使用すると、プログラムデバッグデータベース (PDB) ファイルのさまざまなセクションを DIA SDK で識別できます。

## <a name="constants"></a>定数
次のは C/C++マクロとして宣言されています。

|マクロ|[値]|
|-----------|-----------|
|`DiaTable_Symbols`|L "記号"|
|`DiaTable_Sections`|L "セクション"|
|`DiaTable_SrcFiles`|L "SourceFiles"|
|`DiaTable_LineNums`|L"LineNumbers"|
|`DiaTable_SegMap`|L "SegmentMap"|
|`DiaTable_Dbg`|L"Dbg"|
|`DiaTable_InjSrc`|L "InjectedSource"|
|`DiaTable_FrameData`|L "フレームデータ"|

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

## <a name="requirements"></a>［要件］
ヘッダー: dia2

## <a name="see-also"></a>関連項目
- [参照](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
