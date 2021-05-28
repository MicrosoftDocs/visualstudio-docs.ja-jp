---
description: クライアントが反復処理できるように、指定された名前に一致するすべてのインライン関数の行番号情報の列挙を取得します。
title: IDiaSession::findInlineesByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 9860336d-f703-4ecb-bfc4-3f5beb175a76
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6c5f39638c16444f7a60df028813c66525b0d025
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634318"
---
# <a name="idiasessionfindinlineesbyname"></a>IDiaSession::findInlineesByName
クライアントが反復処理できるように、指定された名前に一致するすべてのインライン関数の行番号情報の列挙を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findInlineesByName ( 
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `name`

[入力] 比較に使用する名前を指定します。

 `option`

[入力] 名前の検索に適用する比較オプションを指定します。 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)に関するページの列挙型の値は、単独で使用することも、組み合わせて使用することもできます。

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
