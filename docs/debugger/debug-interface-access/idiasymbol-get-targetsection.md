---
description: サンク ターゲットのアドレス セクションを取得します。
title: IDiaSymbol::get_targetSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_targetSection method
ms.assetid: 95382395-da41-4aa8-87f1-5b03da128565
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d72ce83ada785cc598df123929b54a3cc8b6d7b2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634608"
---
# <a name="idiasymbolget_targetsection"></a>IDiaSymbol::get_targetSection
サンク ターゲットのアドレス セクションを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_targetSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] サンク ターゲット アドレスのセクション部分。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
