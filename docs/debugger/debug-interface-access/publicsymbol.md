---
description: .exe ファイルの作成時に、各パブリック シンボル (少なくとも、各グローバル関数とデータ シンボル) に SymTagPublicSymbol タグが付与されます。
title: PublicSymbol | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- data symbols [C++]
- PublicSymbol symbol
- global functions [C++], as public symbols
ms.assetid: f8d33007-302d-4549-9dad-47fb33ea60b7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 02a706a1dc20dd61c43fce62905b2d3ac48f87fd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635205"
---
# <a name="publicsymbol"></a>PublicSymbol
.exe ファイルの作成時に、各パブリック シンボル (少なくとも、各グローバル関数とデータ シンボル) に `SymTagPublicSymbol` タグが付与されます。

## <a name="properties"></a>プロパティ
 次の表に、このシンボル型に対して有効なプロパティを示します。

|プロパティ|データ型|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|場所のオフセット部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|場所のセクション部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSymbol::get_code](../../debugger/debug-interface-access/idiasymbol-get-code.md)|`BOOL`|シンボルの場所がコード内にある場合は `TRUE`。|
|[IDiaSymbol::get_function](../../debugger/debug-interface-access/idiasymbol-get-function.md)|`BOOL`|シンボルが関数の場合は `TRUE`。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|このシンボルの長さ (バイト単位)。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|グローバル スコープのシンボル。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文上の親シンボルの ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|パブリック シンボルには静的な場所があります。詳細については、「[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」を参照してください。|
|[IDiaSymbol::get_managed](../../debugger/debug-interface-access/idiasymbol-get-managed.md)|`BOOL`|シンボルの場所がマネージド コード内にある場合は `TRUE`。|
|[IDiaSymbol::get_msil](../../debugger/debug-interface-access/idiasymbol-get-msil.md)|`BOOL`|シンボルの場所が Microsoft Intermediate Language (MSIL) コード内にある場合は `TRUE`。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|シンボルの完全装飾名。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|ブロック内でのシンボルの相対位置。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagPublicSymbol` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|`BSTR`|シンボルの非装飾名。|
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|`BSTR`|シンボルの非装飾名の一部または全体。|

## <a name="see-also"></a>関連項目
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
- [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)
