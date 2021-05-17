---
description: IDiaSession::findInlineeLinesByAddr は、指定された親シンボルによって直接または間接的にインライン化され指定されたアドレス範囲内に含まれているすべての関数の行番号情報をクライアントが反復処理することを可能にする列挙体を取得します。
title: IDiaSession::findInlineeLinesByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: bb70e408-eed1-4c9c-b5b1-44323125f48b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 917da4855990844fb6bc0c3fc995174b519b129e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634321"
---
# <a name="idiasessionfindinlineelinesbyaddr"></a>IDiaSession::findInlineeLinesByAddr
指定された親シンボルによって直接または間接的にインライン化され指定されたアドレス範囲内に含まれているすべての関数の行番号情報をクライアントが反復処理することを可能にする列挙体を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findInlineeLinesByAddr ( 
   IDiaSymbol*           parent,   DWORD                 isect,   DWORD                 offset,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `parent`

[入力] 親を表す `IDiaSymbol` オブジェクト。

 `isect`

[入力] アドレスのセクション部分を指定します。

 `offset`

[入力] アドレスのオフセット部分を指定します。

 `length`

[入力] このクエリでカバーするアドレス範囲をバイト数で指定します。

 `ppResult`

[出力] 取得された行番号の一覧を含む `IDiaEnumLineNumbers` オブジェクトを保持します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
