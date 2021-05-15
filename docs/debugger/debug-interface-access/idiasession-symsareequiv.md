---
description: 2 つのシンボルが等しいかどうかを確認します。
title: IDiaSession::symsAreEquiv | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symsAreEquiv method
ms.assetid: 9941d520-e203-46c0-83c3-b3a967f4fc59
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c5f887b13195bdde133c4bca845291b1255b99ea
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634801"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
2 つのシンボルが等しいかどうかを確認します。

## <a name="syntax"></a>構文

```C++
HRESULT symsAreEquiv ( 
   IDiaSymbol* symbolA,
   IDiaSymbol* symbolB
);
```

#### <a name="parameters"></a>パラメーター
 `symbolA`

[入力] 比較で使用される最初の [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。

 `symbolB`

[入力] 比較で使用される 2 番目の `IDiaSymbol` オブジェクト。

## <a name="return-value"></a>戻り値
 シンボルが等しい場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` を返します。その場合、シンボルは等しくありません。 それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
