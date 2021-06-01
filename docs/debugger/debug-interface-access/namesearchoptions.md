---
description: シンボルおよびファイルの名前の検索オプションを指定します。
title: NameSearchOptions | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- NameSearchOptions enumeration
ms.assetid: 67dfbede-2678-47df-b664-5c49841d0b9b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bd074de0c44803a06d5399f2bd4dc1e3c43618a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634563"
---
# <a name="namesearchoptions"></a>NameSearchOptions
シンボルおよびファイルの名前の検索オプションを指定します。

## <a name="syntax"></a>構文

```C++
enum NameSearchOptions {
    nsNone,
    nsfCaseSensitive     = 0x1,
    nsfCaseInsensitive   = 0x2,
    nsfFNameExt          = 0x4,
    nsfRegularExpression = 0x8,
    nsfUndecoratedName   = 0x10,

// For backward compatibility:
    nsCaseSensitive           = nsfCaseSensitive,
    nsCaseInsensitive         = nsfCaseInsensitive,
    nsFNameExt                = nsfCaseInsensitive | nsfFNameExt,
    nsRegularExpression       = nsfRegularExpression | nsfCaseSensitive,
    nsCaseInRegularExpression = nsfRegularExpression | nsfCaseInsensitive
};
```

## <a name="elements"></a>要素
`nsNone` オプションは指定されていません。

`nsfCaseSensitive` 大文字と小文字を区別した名前の一致を適用します。

`nsfCaseInsensitive` 大文字と小文字を区別しない名前の一致を適用します。

`nsfFNameExt` 名前をパスとして扱い、filename.ext の名前の一致を適用します。

`nsfRegularExpression` アスタリスク (*) と疑問符 (?) をワイルドカードとして使用して、大文字と小文字を区別した名前の一致を適用します。 (その他の一般的な正規表現文字はサポートされていません。)

`nsfUndecoratedName` 非装飾名と装飾名の両方を持つシンボルにのみ適用されます。

## <a name="remarks"></a>解説
この列挙型の値は次のメソッドに渡されます。

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

## <a name="requirements"></a>必要条件
ヘッダー: dia2.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
