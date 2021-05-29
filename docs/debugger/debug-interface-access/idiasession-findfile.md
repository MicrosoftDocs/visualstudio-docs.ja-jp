---
description: コンパイル単位と名前を指定してソース ファイルを取得します。
title: IDiaSession::findFile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findFile method
ms.assetid: a215dc21-b316-40d7-9923-55bfa014976b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: af547f9e504e9d832968bd18a370cb43e816e786
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635015"
---
# <a name="idiasessionfindfile"></a>IDiaSession::findFile
コンパイル単位と名前を指定してソース ファイルを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findFile ( 
   IDiaSymbol*           pCompiland,
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumSourceFiles** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `pCompiland`

[入力] 検索のコンテキストとして使用されるコンパイル単位を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。 すべてのコンパイル単位でソース ファイルを検索するには、このパラメーターを `NULL` に設定します。

 `name`

[入力] 取得するソース ファイルの名前を指定します。 取得するすべてのソース ファイルに対して、このパラメーターを `NULL` に設定します。

 `option`

[入力] 名前の検索に適用する比較オプションを指定します。 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)に関するページの列挙型の値は、単独で使用することも、組み合わせて使用することもできます。

 `ppResult`

[出力] 取得したソース ファイルの一覧を含む [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例

```C++
IDiaEnumSourceFiles* pEnum;
pSession->findFile( NULL, L"sourcefile.cpp", nsFNameExt, &pEnum );
```

## <a name="see-also"></a>関連項目
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)
