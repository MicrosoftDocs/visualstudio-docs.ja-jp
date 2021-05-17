---
description: コンパイラのバックエンド ビルド番号を取得します。
title: IDiaSymbol::get_backEndBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_backEndBuild method
ms.assetid: 423af497-9294-438e-92b4-456c6f56dc56
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 02864e046e5227d22e6c07fb70efad80b53e3689
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634737"
---
# <a name="idiasymbolget_backendbuild"></a>IDiaSymbol::get_backEndBuild
コンパイラのバックエンド ビルド番号を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_backEndBuild ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] バックエンド ビルド番号を返します。 「解説」を参照してください。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 通常、コンパイラは、ソース コードを中間形式に解析するフロントエンド (パーサー) と、中間形式をアセンブリに変換するバックエンド (コード ジェネレーター) の 2 つの主要要素で構成されています。 フロントエンドとバックエンドのバージョンが異なるのは珍しくありません。

 フロントエンドまたはバックエンドのバージョン番号は、\<major>.\<minor>.\<build> の 3 つの部分で構成されています (ここで、\<major> はメジャー バージョン番号、\<minor> はマイナー バージョン番号、\<build> はビルド番号です)。 例: 13.10.3077。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
