---
title: IDiaSymbol::findChildrenEx |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenEx
ms.assetid: 6e045045-da8c-4338-9423-81a1ca20c405
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b833353beb009bb4eabbf000d45e0eb44a5794f
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "62837876"
---
# <a name="idiasymbolfindchildrenex"></a>IDiaSymbol::findChildrenEx
シンボルの子を取得します。 返されるローカル シンボルにはで最適化を使用して、プログラムがコンパイルされている場合、ライブの範囲の情報が含まれます。

## <a name="syntax"></a>構文

```C++
HRESULT findChildrenEx ( 
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
 返します`S_OK`シンボルの少なくとも 1 つの子が検出されましたが、またはを返す`S_FALSE`場合は子が見つかりませんでした。 それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、拡張のバージョンの[idiasymbol::findchildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)します。

## <a name="requirements"></a>必要条件
 ヘッダー:Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)