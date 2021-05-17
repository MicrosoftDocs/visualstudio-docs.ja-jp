---
description: 指定された親識別子の子で、名前とシンボルの種類に一致するものをすべて取得します。
title: IDiaSession::findChildren | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findChildren method
ms.assetid: 5d19046f-f668-4aa9-8788-95cda9a98997
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ea45a427b00d7627eaba21bdd628f2cff2cefbf0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634333"
---
# <a name="idiasessionfindchildren"></a>IDiaSession::findChildren
指定された親識別子の子で、名前とシンボルの種類に一致するものをすべて取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findChildren ( 
   IDiaSymbol*       parent,
   SymTagEnum        symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `parent`

[入力] 親を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。 この親シンボルが関数、モジュール、またはブロックの場合、その構文上の子が `ppResult` で返されます。 親シンボルが型の場合は、そのクラスの子が返されます。 このパラメーターが `NULL` の場合は、`symtag` を `SymTagExe` または `SymTagNull` に設定する必要があります。これにより、グローバル スコープ (.exe ファイル) が返されます。

 `symtag`

[入力] 取得する子のシンボル タグを指定します。 値は、[SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の列挙体から取得されます。 すべての子を取得するには、`SymTagNull` に設定します。

 `name`

[入力] 取得する子の名前を指定します。 すべての子を取得するには、`NULL` に設定します。

 `compareFlags`

[入力] 名前の照合に適用する比較オプションを指定します。 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)の列挙体の値は、単独で使用することも、組み合わせて使用することもできます。

 `ppResult`

[出力] 取得された子シンボルの一覧を含む [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例
 次の例では、名前 `szVarName` に一致する関数 `pFunc` のローカル変数を検索する方法を示します。

```C++
IDiaEnumSymbols* pEnum;
pSession->findChildren( pFunc, SymTagData, szVarName, nsCaseSensitive, &pEnum );
```

## <a name="see-also"></a>関連項目
- [概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
