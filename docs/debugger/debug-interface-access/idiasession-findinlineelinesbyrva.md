---
description: IDiaSession::findInlineeLinesByRVA は、指定された親シンボルで直接または間接的にインライン化されていて、かつ指定された相対仮想アドレス (RVA) 内に含まれている、すべての関数の行番号情報をクライアントで反復処理するための列挙値を取得します。
title: IDiaSession::findInlineeLinesByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 7a74d5ee-0dbf-47c0-92b4-47ec03b13ce9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b9989ffd3c8b4cf03b82cbb0f310840572315031
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634319"
---
# <a name="idiasessionfindinlineelinesbyrva"></a>IDiaSession::findInlineeLinesByRVA
指定された親シンボルで直接または間接的にインライン化されていて、かつ指定された相対仮想アドレス (RVA) 内に含まれている、すべての関数の行番号情報をクライアントで反復処理するための列挙値を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findInlineeLinesByRVA ( 
   IDiaSymbol*           parent,
   DWORD                 rva,
   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `parent`

[入力] 親を表す `IDiaSymbol` オブジェクト。

 `rva`

[入力] アドレスを RVA として指定します。

 `length`

[入力] このクエリでカバーするアドレス範囲をバイト数で指定します。

 `ppResult`

[出力] 取得された行番号の一覧を含む `IDiaEnumLineNumbers` オブジェクトを保持します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
