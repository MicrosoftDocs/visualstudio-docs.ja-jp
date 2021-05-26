---
description: 関数にデバッグを終了するポイントが定義されている場合、デバッグ開始ポイントは、SymTagFuncDebugEnd タグが設定されたシンボルで識別されます。
title: FuncDebugEnd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- FuncDebugEnd symbol
- debugging [DIA SDK], end point
ms.assetid: 68f84fff-7cd3-4636-b929-7063a45009f8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5b28fe8f1a436dd308487187897fa62fd247a293
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634517"
---
# <a name="funcdebugend"></a>FuncDebugEnd
関数にデバッグを終了するポイントが定義されている場合、デバッグ開始ポイントは、`SymTagFuncDebugEnd` タグが設定されたシンボルで識別されます。

## <a name="properties"></a>プロパティ
 次の表に、このシンボル型に対して有効なプロパティを示します。

|プロパティ|データ型|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|場所のオフセット部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|場所のセクション部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|関数がカスタム呼び出し規則を使用している場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|関数が far return を実行する場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|関数に割り込みからの戻りが含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|関数が静的である場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|外側の関数のシンボル。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文上の親シンボルの ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|終了ポイントには静的な場所があります。詳細については、「[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」を参照してください。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|関数が [noinline](/cpp/cpp/noinline) 属性を使用して指定されている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|関数が [noreturn](/cpp/cpp/noreturn) 属性を使用して指定されている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|関数が呼び出されることがない場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|メモリ内のシンボルのオフセット。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)の `LocIsRegRel` を参照してください。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|関数に、最適化されたコードのデバッグ情報が含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|モジュール内でのこの関数の末尾の相対位置。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagFuncDebugEnd` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|実行可能イメージ内でのこの関数の位置。|

## <a name="see-also"></a>関連項目
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
- [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)
