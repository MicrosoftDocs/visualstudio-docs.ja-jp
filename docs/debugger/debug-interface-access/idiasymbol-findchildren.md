---
title: Idiasymbol::findchildren |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildren method
ms.assetid: 5fe7573a-e48b-428d-9c17-7421b7209246
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5199be7307fdaa607f5aa6a5f554d9fcc82f452d
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56623152"
---
# <a name="idiasymbolfindchildren"></a>IDiaSymbol::findChildren
シンボルの子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findChildren ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `symtag`

[in]定義されているを取得するには、子のシンボル タグを指定します、 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)します。 設定`SymTagNull`のすべての子を取得します。

 `name`

[in]取得する子の名前を指定します。 設定`NULL`のすべての子を取得します。

 `compareFlags`

[in]名前の一致に適用される比較オプションを指定します。 値から、 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)列挙体は、単独または組み合わせて使用できます。

 `ppResult`

[out]返します、 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)子シンボルの一覧を含むオブジェクトを取得します。

## <a name="return-value"></a>戻り値
 返します`S_OK`シンボルの少なくとも 1 つの子が検出されましたが、または返す`S_FALSE`場合は子が見つかりませんでした。 エラー コードを返しますそれ以外の場合。

## <a name="remarks"></a>解説
 このメソッドを呼び出すことは、 [idiasession::findchildren](../../debugger/debug-interface-access/idiasession-findchildren.md)このシンボルを最初のパラメーターとしてメソッド。

## <a name="see-also"></a>参照
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)