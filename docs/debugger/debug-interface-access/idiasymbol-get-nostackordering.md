---
description: この関数は、スタック バッファー チェック ([/GS (バッファーのセキュリティ チェック)](/cpp/build/reference/gs-buffer-security-check) コンパイラ オプション) の一部としてスタックの順序付けを実行できなかったことを示すフラグを取得します。
title: IDiaSymbol::get_noStackOrdering | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noStackOrdering method
ms.assetid: a1753917-705b-4165-9880-d05e91e6dcb4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fbfcb8c4404179431c4c480ee036210cb2d0be77
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634235"
---
# <a name="idiasymbolget_nostackordering"></a>IDiaSymbol::get_noStackOrdering
この関数は、スタック バッファー チェック ([/GS (バッファーのセキュリティ チェック)](/cpp/build/reference/gs-buffer-security-check) コンパイラ オプション) の一部としてスタックの順序付けを実行できなかったことを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_noStackOrdering(
   BOOL *pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] スタック バッファー チェックの一部としてスタックの順序付けを実行できなかった場合は `TRUE` を返します。それ以外の場合は `FALSE` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [/GS (バッファーのセキュリティ チェック)](/cpp/build/reference/gs-buffer-security-check)
