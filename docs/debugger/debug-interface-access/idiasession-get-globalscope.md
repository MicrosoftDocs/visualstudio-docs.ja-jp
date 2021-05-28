---
description: グローバル スコープへの参照を取得します。
title: IDiaSession::get_globalScope | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::get_globalScope method
ms.assetid: 75d128a8-3dce-40ed-b392-de3fdda041b7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ce8c0c68242aef2e06a071686c57d1f5ebec2976
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634810"
---
# <a name="idiasessionget_globalscope"></a>IDiaSession::get_globalScope
グローバル スコープへの参照を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_globalScope ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] グローバル スコープを表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [Exe](../../debugger/debug-interface-access/exe.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
