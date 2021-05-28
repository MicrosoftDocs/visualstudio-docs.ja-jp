---
description: 各関数は SymTagFunction シンボルによって識別されます。
title: 関数 (Debug Interface Access SDK) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Function symbol
ms.assetid: 458dc91c-b78b-4427-84f4-615d89e26760
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 850ecedbdacb8349dc8ff6450c79dee219b61418
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634516"
---
# <a name="function-debug-interface-access-sdk"></a>関数 (Debug Interface Access SDK)
各関数は `SymTagFunction` シンボルによって識別されます。

## <a name="properties"></a>Properties
 次の表に、このシンボル型に対して有効なプロパティを示します。

|プロパティ|データ型|説明|
|--------------|-----------------|-----------------|
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|`DWORD`|[CV_access_e 列挙型](../../debugger/debug-interface-access/cv-access-e.md)の値の 1 つ (関数がメンバー関数の場合)。|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|場所のオフセット部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|場所のセクション部分。詳細については、[LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)を参照してください。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|クラスのシンボル (関数がメンバー関数の場合)。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|クラスの親シンボルの ID。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|関数が定数としてマークされている場合は `TRUE`。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|関数がカスタム呼び出し規則を使用している場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|関数が far return を実行する場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasAlloca](../../debugger/debug-interface-access/idiasymbol-get-hasalloca.md)|`BOOL`|関数が割り当てられたメモリ関数を使用する場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasEH](../../debugger/debug-interface-access/idiasymbol-get-haseh.md)|`BOOL`|関数に C++ スタイルの例外処理が含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasEHa](../../debugger/debug-interface-access/idiasymbol-get-haseha.md)|`BOOL`|関数に非同期例外処理が含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasInlAsm](../../debugger/debug-interface-access/idiasymbol-get-hasinlasm.md)|`BOOL`|関数にインライン アセンブリが含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasLongJump](../../debugger/debug-interface-access/idiasymbol-get-haslongjump.md)|`BOOL`|関数に [longjmp](/cpp/c-runtime-library/reference/longjmp) の呼び出しが含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|関数にセキュリティ チェックが含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasSEH](../../debugger/debug-interface-access/idiasymbol-get-hasseh.md)|`BOOL`|関数に Win32 スタイルの構造化例外処理が含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)|`BOOL`|関数に [setjmp](/cpp/c-runtime-library/reference/setjmp) の呼び出しが含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|関数に割り込みからの戻りがある場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|`BOOL`|関数が導入仮想関数の場合は `TRUE`。|
|[IDiaSymbol::get_InlSpec](../../debugger/debug-interface-access/idiasymbol-get-inlspec.md)|`BOOL`|関数が [inline、__inline、\__forceinline](/cpp/cpp/inline-functions-cpp) のいずれかの属性でマークされている場合は `TRUE`。|
|[IDiaSymbol::get_isNaked](../../debugger/debug-interface-access/idiasymbol-get-isnaked.md)|`BOOL`|関数が [naked](/cpp/cpp/naked-cpp) 属性でマークされている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|関数が静的である場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|位置から開始する関数コードのバイト数。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|外側のコンパイル単位のシンボル。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文上の親シンボルの ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|関数には静的な場所またはメタデータの場所を指定できます。詳細については、「[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」を参照してください。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|関数の名前です。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|関数がインライン関数でない場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|関数に到達できない場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|関数から値が返されない場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_noStackOrdering](../../debugger/debug-interface-access/idiasymbol-get-nostackordering.md)|`BOOL`|関数がバッファーのセキュリティ チェックを使用してコンパイルされ、スタックの順序付けを実行できなかった場合は `TRUE`。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|コードに最適化されたコードのデバッグ情報がある場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|`BOOL`|関数が純粋仮想関数の場合は `TRUE`。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|モジュール内でのこの関数の相対位置。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagFunction` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|
|[IDiaSymbol::get_token](../../debugger/debug-interface-access/idiasymbol-get-token.md)|`DWORD`|関数のメタデータ トークン。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|関数シグネチャのシンボル。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|型のシンボルの ID。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|関数が整列されていない場合は `TRUE`。|
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|`BSTR`|非装飾形式の関数名 (DIA SDK v8.0 以降のみ)。|
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|`BSTR`|非装飾形式の関数名の一部またはすべて (DIA SDK v8.0 以降のみ)。|
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|`BOOL`|仮想関数の場合は `TRUE`。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|実行可能イメージ内でのこの関数の位置。|
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|`DWORD`|仮想関数の場合は、仮想関数テーブル内のオフセット。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|関数が揮発性としてマークされている場合は `TRUE`。|

## <a name="see-also"></a>こちらもご覧ください
- [CV_access_e 列挙型](../../debugger/debug-interface-access/cv-access-e.md)
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
- [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)
