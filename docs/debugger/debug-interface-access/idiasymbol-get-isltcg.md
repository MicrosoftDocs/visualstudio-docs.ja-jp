---
description: コンパイル単位が、プログラム全体の最適化を支援するリンカー スイッチ、/LTCG (リンク時のコード生成) (/cpp/build/reference/ltcg-link-time-code-generation) にリンクされているかどうかを示すフラグを取得します。
title: IDiaSymbol::get_isLTCG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isLTCG method
ms.assetid: 5f7f05b8-6b71-4958-9e1e-e4924ef9c59b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1b8306dabe6533287d7d28841ea76f2d6478e4a3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635132"
---
# <a name="idiasymbolget_isltcg"></a>IDiaSymbol::get_isLTCG
[コンパイル単位](../../debugger/debug-interface-access/compiland.md)が、プログラム全体の最適化を支援するリンカー スイッチ、[/LTCG (リンク時のコード生成)](/cpp/build/reference/ltcg-link-time-code-generation) にリンクされているかどうかを示すフラグを取得します。 このスイッチは、マネージド コードにのみ適用できます。

## <a name="syntax"></a>構文

```C++
HRESULT get_iSLTCG(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>パラメーター
 pFlag

[出力] `compiland` が /LTCG のリンカー スイッチにリンクされている場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
