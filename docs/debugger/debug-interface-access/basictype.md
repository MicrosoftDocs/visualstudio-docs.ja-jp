---
title: BasicType | Microsoft Docs
description: Visual Studio Debug Interface Access SDK でシンボルの基本型を指定する、BasicType 列挙型に関する参照情報を検索します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- BasicType enumeration
ms.assetid: 19ae53ba-cd6e-47b6-9f94-27ae663ce955
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a86a25d02b1aa51e49d80b71dbd37b2aa4c2d103
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634225"
---
# <a name="basictype"></a>BasicType
シンボルの基本型を指定します。

## <a name="syntax"></a>構文

```C++
enum BasicType {
    btNoType   = 0,
    btVoid     = 1,
    btChar     = 2,
    btWChar    = 3,
    btInt      = 6,
    btUInt     = 7,
    btFloat    = 8,
    btBCD      = 9,
    btBool     = 10,
    btLong     = 13,
    btULong    = 14,
    btCurrency = 25,
    btDate     = 26,
    btVariant  = 27,
    btComplex  = 28,
    btBit      = 29,
    btBSTR     = 30,
    btHresult  = 31,
    btChar16   = 32,  // char16_t
    btChar32   = 33,  // char32_t
};
```

## <a name="elements"></a>要素
btNoType 基本型が指定されていません。

btVoid 基本型は `void` です。

btChar 基本型は `char` (C/C++ 型) です。

btWChar 基本型はワイド (Unicode) 文字 (`WCHAR`) です。

btInt 基本型は `signed int` (C/C++ 型) です。

btUInt 基本型は `unsigned int` (C/C++ 型) です。

btFloat 基本型は浮動小数点数 (`FLOAT`) です。

btBCD 基本型は、2 進化 10 進数 (`BCD`) です。

btBool 基本型はブール値 (`BOOL`) です。

btLong 基本型は `long int` (C/C++ 型) です。

btULong 基本型は `unsigned long int` (C/C++ 型) です。

btCurrency 基本型は通貨です。

btDate 基本型は日時 (`DATE`) です。

btVariant 基本型は変数型の構造体 (`VARIANT`) です。

btComplex 基本型は複素数です。

btBit 基本型はビットです。

btBSTR 基本型は、基本またはバイナリ文字列 (`BSTR`) です。

btHresult 基本型は `HRESULT` です。

## <a name="remarks"></a>解説
この列挙型の値は、[IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md) メソッドによって返されます。

## <a name="requirements"></a>要件
ヘッダー: cvconst.h

## <a name="see-also"></a>こちらもご覧ください
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)
- [IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)
