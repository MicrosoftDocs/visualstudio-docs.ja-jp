---
title: CV_CFL_LANG | Microsoft Docs
description: Debug Interface Access SDK でアプリケーションまたはリンクされたモジュールのコード言語を指定する、CV_CFL_LANG 列挙型に関する情報を取得します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_CFL_LANG enumeration
ms.assetid: 4e8e0613-ad02-4de9-9f46-e4753c5b0251
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 46c20fbe0c46a6c964a05b92ccd3a8bcf73cd1f9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634195"
---
# <a name="cv_cfl_lang"></a>CV_CFL_LANG
アプリケーションまたはリンクされたモジュールのソース コード言語を指定します。

## <a name="syntax"></a>構文

```C++
typedef enum CV_CFL_LANG {
    CV_CFL_C       = 0x00,
    CV_CFL_CXX     = 0x01,
    CV_CFL_FORTRAN = 0x02,
    CV_CFL_MASM    = 0x03,
    CV_CFL_PASCAL  = 0x04,
    CV_CFL_BASIC   = 0x05,
    CV_CFL_COBOL   = 0x06,
    CV_CFL_LINK    = 0x07,
    CV_CFL_CVTRES  = 0x08,
    CV_CFL_CVTPGD  = 0x09,
    CV_CFL_CSHARP  = 0x0A,
    CV_CFL_VB      = 0x0B,
    CV_CFL_ILASM   = 0x0C,
    CV_CFL_JAVA    = 0x0D,
    CV_CFL_JSCRIPT = 0x0E,
    CV_CFL_MSIL    = 0x0F,
    CV_CFL_HLSL    = 0x10
} CV_CFL_LANG;
```

## <a name="elements"></a>要素
CV_CFL_C アプリケーション言語は C です。

CV_CFL_CXX アプリケーション言語は C++ です。

CV_CFL_FORTRAN アプリケーション言語は FORTRAN です。

CV_CFL_MASM アプリケーション言語は Microsoft Macro Assembler です。

CV_CFL_PASCAL アプリケーション言語は Pascal です。

CV_CFL_BASIC アプリケーション言語は BASIC です。

CV_CFL_COBOL アプリケーション言語は COBOL です。

CV_CFL_LINK アプリケーションは、リンカーによって生成されたモジュールです。

CV_CFL_CVTRES アプリケーションは、CVTRES ツールで変換されたリソース モジュールです。

CV_CFL_CVTPGD アプリケーションは、CVTPGD ツールで生成された POGO 最適化モジュールです。

CV_CFL_CSHARP アプリケーション言語は C# です。

CV_CFL_VB アプリケーション言語は Visual Basic です。

CV_CFL_ILASM アプリケーション言語は、中間言語アセンブリ (つまり、共通言語ランタイム (CLR) アセンブリ) です。

CV_CFL_JAVA アプリケーション言語は Java です。

CV_CFL_JSCRIPT アプリケーション言語は Jscript です。

CV_CFL_MSIL アプリケーション言語は、不明な Microsoft Intermediate Language (MSIL) です。これは、[/LTCG (リンク時のコード生成)](/cpp/build/reference/ltcg-link-time-code-generation) スイッチを使用した結果である可能性があります。

CV_CFL_HLSL アプリケーション言語は、ハイレベル シェーダー言語です。

## <a name="remarks"></a>解説
この列挙型の値は、[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md) メソッドへの呼び出しによって返されます。

## <a name="requirements"></a>要件
ヘッダー: cvconst.h

## <a name="see-also"></a>こちらもご覧ください
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)
