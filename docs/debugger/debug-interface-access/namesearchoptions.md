﻿---
title: NameSearchOptions |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- NameSearchOptions enumeration
ms.assetid: 67dfbede-2678-47df-b664-5c49841d0b9b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8fa637a5f403a4651541d920c6390204ee579994
ms.sourcegitcommit: 752f03977f45169585e407ef719450dbe219b7fc
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56318616"
---
# <a name="namesearchoptions"></a>NameSearchOptions
シンボルとファイル名の検索オプションを指定します。

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

## <a name="elements"></a>Elements
`nsNone`  
オプションは指定されていません。

`nsfCaseSensitive`  
大文字小文字を区別する名前の一致を適用します。

`nsfCaseInsensitive`  
大文字の名前の一致を適用します。

`nsfFNameExt`  
パスと名前を処理し、.ext という名前の一致を適用します。

`nsfRegularExpression`  
ワイルドカードとしてアスタリスク (*) や疑問符 (?) を使用して区別する名前の一致を適用します。

`nsfUndecoratedName`  
装飾されていないし、装飾名がシンボルにのみ適用されます。

## <a name="remarks"></a>解説
この列挙の値は、次のメソッドに渡されます。

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

## <a name="requirements"></a>要件
ヘッダー: dia2.h

## <a name="see-also"></a>参照
[列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)  
[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)  
[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)  
[IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
