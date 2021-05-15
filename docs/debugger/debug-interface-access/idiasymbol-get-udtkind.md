---
description: さまざまなユーザー定義型 (UDT) を取得します。
title: IDiaSymbol::get_udtKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_udtKind method
ms.assetid: 4002f887-aea6-4475-b302-67c57079fe0a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6c49fc5b27a9af2a986b0cde1dc41b3a07df7150
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634592"
---
# <a name="idiasymbolget_udtkind"></a>IDiaSymbol::get_udtKind
さまざまなユーザー定義型 (UDT) を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_udtKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] UDT の種類 (構造体、クラス、または共用体) を指定する [UdtKind 列挙型](../../debugger/debug-interface-access/udtkind.md)の列挙から値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [UdtKind 列挙型](../../debugger/debug-interface-access/udtkind.md)
