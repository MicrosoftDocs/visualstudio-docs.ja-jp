---
description: シンボルを検索するパスと、各パスの検索結果のリストを取得します。
title: IDebugModule3::GetSymbolInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::GetSymbolInfo
helpviewer_keywords:
- GetSymbolInfo method
- IDebugModule3::GetSymbolInfo method
ms.assetid: dda5e8e1-6878-4aa9-9ee4-e7d0dcc11210
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9cc4c8d7c88e4b973ad7055327da73472a6ed4d2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065529"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
シンボルを検索するパスと、各パスの検索結果のリストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSymbolInfo(
    SYMBOL_SEARCH_INFO_FIELDS  dwFields,
    MODULE_SYMBOL_SEARCH_INFO* pInfo
);
```

```csharp
int GetSymbolInfo(
    enum_SYMBOL_SEARCH_INFO_FIELDS dwFields,
    MODULE_SYMBOL_SEARCH_INFO[]    pinfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[入力] 入力される `pInfo` のフィールドを指定する [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) 列挙型のフラグの組み合わせ。

`pInfo`\
[出力] 指定された情報を使用してそのメンバーが満たされる [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) 構造体。 これが null 値の場合、このメソッドは `E_INVALIDARG` を返します。

## <a name="return-value"></a>戻り値
メソッドが成功した場合、`S_OK` を返します。それ以外の場合はエラー コードを返します。

> [!NOTE]
> `S_OK` が返された場合でも、(`MODULE_SYMBOL_SEARCH_INFO` 構造体に) 返された文字列が空である可能性があります。 これは、返すべき検索情報がなかったことを示しています。

## <a name="remarks"></a>解説
`MODULE_SYMBOL_SEARCH_INFO` 構造体の `bstrVerboseSearchInfo` フィールドが空でない場合は、検索したパスとその検索結果のリストが含まれています。 リストはパス、その後に省略記号 ("...")、その後に結果が続く形で書式設定されています。 複数のパスの結果のペアがある場合、各ペアは "\r\n" (キャリッジリターン/ラインフィード) ペアで区切られます。 パターンは次のようになります。

\<path>...\<result>\r\n\<path>...\<result>\r\n\<path>...\<result>

最後のエントリには \r\n シーケンスがないことに注意してください。

## <a name="example"></a>例
この例では、このメソッドは 3 つのパスと 3 通りの異なる検索結果を返します。 各行の末尾はキャリッジリターン/ラインフィードのペアになります。 この出力例では、検索結果を単一の文字列として出力するだけです。

> [!NOTE]
> "..." の直後から行末までのすべての部分が状態の結果です。

```cpp
void ShowSymbolSearchResults(IDebugModule3 *pIDebugModule3)
{
    MODULE_SYMBOL_SEARCH_INFO ssi = { 0 };
    HRESULT hr;
    hr = pIDebugModule3->GetSymbolInfo(SSIF_VERBOSE_SEARCH_INFO,&ssi);
    if (SUCCEEDED(hr)) {
        CComBSTR searchInfo = ssi.bstrVerboseSearchInfo;
        if (searchInfo.Length() != 0) {
            std::wcout << (wchar_t *)(BSTR)searchInfo;
            std::wcout << std::endl;
        }
    }
}
```

**c:\symbols\user32.pdb... ファイルが見つかりません。** 
**c:\winnt\symbols\user32.pdb... バージョンが一致しません。** 
 **\\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... シンボルが読み込まれました。**

## <a name="see-also"></a>関連項目

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
