---
description: 検索されたシンボル検索パスに関する状態情報が含まれます。
title: MODULE_SYMBOL_SEARCH_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_SYMBOL_SEARCH_INFO
helpviewer_keywords:
- MODULE_SYMBOL_SEARCH_INFO structure
ms.assetid: 432aff03-08a5-4c5a-b2d5-e212090fc70a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 266d786df422e5260e212a4005feb7d3167af099
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057898"
---
# <a name="module_symbol_search_info"></a>MODULE_SYMBOL_SEARCH_INFO

検索されたシンボル検索パスに関する状態情報が含まれます。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagSYMBOL_SEARCH_INFO
{
    SYMBOL_SEARCH_INFO_FIELDS dwValidFields;
    BSTR                      bstrVerboseSearchInfo;
} MODULE_SYMBOL_SEARCH_INFO;
```

```csharp
public struct MODULE_SYMBOL_SEARCH_INFO {
    public uint   dwValidFields;
    public string bstrVerboseSearchInfo;
}
```

## <a name="members"></a>メンバー

`dwValidFields`\
この構造体で記述されている検索情報の種類を指定する、[SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) 列挙型のフラグの組み合わせ。

`bstrVerboseSearchInfo`\
検索パスと結果が 1 つの文字列に連結されます。

## <a name="remarks"></a>解説

この構造体は、[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md) メソッドの呼び出しから返されます。

`bstrVerboseSearchInfo` フィールドが空でない場合は、検索したパスとその検索結果の一覧が含まれています。 リストはパス、その後に省略記号 ("...")、その後に結果が続く形で書式設定されています。 複数のパスの結果のペアがある場合、各ペアは "\r\n" (キャリッジリターン/ラインフィード) ペアで区切られます。 パターンは次のようになります。

\<path>...\<result>\r\n\<path>...\<result>\r\n\<path>...\<result>

最後のエントリには \r\n シーケンスがないことに注意してください。

次に示すのは、標準出力に送信された `bstrVerboseSearchInfo` 文字列です。

`c:\symbols\user32.pdb... File not found.`

`c:\winnt\symbols\user32.pdb... Version does not match.`

`\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... Symbols loaded.`

## <a name="requirements"></a>必要条件

ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)
