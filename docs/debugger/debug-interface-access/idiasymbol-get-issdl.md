---
description: モジュールが /SDL オプションを使用してコンパイルされているかどうかを指定します。
title: IDiaSymbol::get_isSdl | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 6aa0e116-da75-4643-a4d7-d8e142231e21
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f9cb707c0afb2370224ac87924906b56391babbc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634662"
---
# <a name="idiasymbolget_issdl"></a>IDiaSymbol::get_isSdl
モジュールが /SDL オプションを使用してコンパイルされているかどうかを指定します。

## <a name="syntax"></a>構文

```C++
HRESULT get_isSdl(
   BOOL *pRetVal);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] モジュールが /SDL オプションを使用してコンパイルされているかどうかを指定する `BOOL` へのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
