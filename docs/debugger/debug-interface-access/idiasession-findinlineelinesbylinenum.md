---
description: 指定されたソース ファイルと行番号に直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理することを可能にする列挙体を取得します。
title: IDiaSession::findInlineeLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: cf32ae7c-a0c8-4800-bc8f-d64fdd15fb06
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 130c270e0be0e38768018467e117361c9befd796
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634320"
---
# <a name="idiasessionfindinlineelinesbylinenum"></a>IDiaSession::findInlineeLinesByLinenum
指定されたソース ファイルと行番号に直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理することを可能にする列挙体を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           compiland,
   IDiaSourceFile*       file,
   DWORD                 linenum,
   DWORD                 column,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `compiland`

[入力] 行番号を検索するコンパイル単位を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。 このパラメーターを `NULL` とすることはできません。

 `file`

[入力] 検索するソース ファイルを表す [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) オブジェクト。 このパラメーターを `NULL` とすることはできません。

 `linenum`

[入力] 1 から始まる行番号を指定します。

> [!NOTE]
> 0 を使用してすべての行を指定することはできません (すべての行を検索するには、[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md) メソッドを使用します)。

 `column`

[入力] 列番号を指定します。 すべての列を指定するには 0 を使用します。 列は、1 行内のバイト オフセットです。

 `ppResult`

[出力] 取得された行番号の一覧を含む [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
