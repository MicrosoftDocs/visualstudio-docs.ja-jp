---
description: フロントエンド メジャー バージョン番号を取得します。
title: IDiaSymbol::get_frontEndMajor | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_frontEndMajor method
ms.assetid: f8a067c5-3306-4fc5-bc20-8910a47ed504
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bf5bc125b00fa8194475c9f6101e697dbf66062a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635276"
---
# <a name="idiasymbolget_frontendmajor"></a>IDiaSymbol::get_frontEndMajor
フロントエンド メジャー バージョン番号を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_frontEndMajor ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] フロントエンド メジャー バージョン番号を返します。 「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

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
