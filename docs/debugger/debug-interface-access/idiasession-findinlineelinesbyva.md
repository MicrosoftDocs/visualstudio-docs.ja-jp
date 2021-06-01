---
description: IDiaSession::findInlineeLinesByVA は、指定された親シンボルによって直接または間接的にインライン化され指定された仮想アドレス (VA) 内に含まれているすべての関数の行番号情報をクライアントが反復処理することを可能にする列挙を取得します。
title: IDiaSession::findInlineeLinesByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: dffe6594-e0d1-4ed5-aeea-8773f88d82a6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5b777a035585e2aa9cab60e02da39a6e1858b193
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634819"
---
# <a name="idiasessionfindinlineelinesbyva"></a>IDiaSession::findInlineeLinesByVA
指定された親シンボルによって直接または間接的にインライン化され指定された仮想アドレス (VA) 内に含まれているすべての関数の行番号情報をクライアントが反復処理することを可能にする列挙を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           parent,   ULONGLONG             va,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `parent`

[入力] 親を表す `IDiaSymbol` オブジェクト。

 `va`

[入力] アドレスを VA として指定します。

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
