---
description: 各サンクは SymTagThunk タグで識別されます。
title: サンク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- thunk properties [DIA SDK]
- thunk symbol
ms.assetid: 01abb95f-d89a-465c-a4eb-8e8509598c95
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2dc512192299c165ec837ac26eaf27787bdf6a08
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635195"
---
# <a name="thunk"></a>サンク
各 `thunk` は `SymTagThunk` タグで識別されます。

## <a name="properties"></a>プロパティ
 次の表に、このシンボル型に対して有効なプロパティを示します。

|プロパティ|データ型|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|`DWORD`|[CV_access_e 列挙型](../../debugger/debug-interface-access/cv-access-e.md)の値の 1 つである、アクセス修飾子属性 (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|場所のオフセット部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSegment::get_addressSection](../../debugger/debug-interface-access/idiasegment-get-addresssection.md)|`DWORD`|場所のセクション部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|外側のクラスの親 (存在する場合) (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|外側のクラスの親シンボルの ID (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|サンクが定数としてマークされている場合は TRUE (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|`BOOL`|サンクが仮想関数の導入部である場合は TRUE (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|サンクが静的と見なされる場合は TRUE (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|サンク内のコードのバイト数。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|外側のコンパイル単位、ブロック、または関数のシンボル。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文上の親シンボルの ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|終了ポイントには静的な場所があります。詳細については、「[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」の列挙型を参照してください。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|サンクの名前。|
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|`BOOL`|サンクが純粋に仮想である場合は TRUE (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|モジュール内でのこのサンクの相対位置。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagThunk` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|
|[IDiaSymbol::get_targetOffset](../../debugger/debug-interface-access/idiasymbol-get-targetoffset.md)|`DWORD`|サンク ターゲットの場所のオフセット部分。|
|[IDiaSymbol::get_targetRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetrelativevirtualaddress.md)|`DWORD`|外側のブロック内のサンク ターゲットの相対仮想アドレス。|
|[IDiaSymbol::get_targetSection](../../debugger/debug-interface-access/idiasymbol-get-targetsection.md)|`DWORD`|サンク ターゲットのセクション部分。|
|[IDiaSymbol::get_targetVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetvirtualaddress.md)|`ULONGLONG`|実行可能イメージ内でのサンク ターゲットの位置。|
|[IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)|`DWORD`|[THUNK_ORDINAL 列挙型](../../debugger/debug-interface-access/thunk-ordinal.md)で定義されているサンクの種類。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|このサンクの種類 (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|種類のシンボルの ID (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|サンクが整列されていない場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|`BOOL`|サンクが仮想である場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|実行可能イメージ内でのこのサンクの位置。|
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|`DWORD`|このサンクに対する仮想テーブル内のオフセット (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|サンクが揮発性としてマークされている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|

## <a name="see-also"></a>関連項目
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
- [THUNK_ORDINAL 列挙型](../../debugger/debug-interface-access/thunk-ordinal.md)
