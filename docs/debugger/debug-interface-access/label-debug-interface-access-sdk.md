---
title: ラベル (Debug Interface Access SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- locations, in program code
- Label symbol
ms.assetid: 8cef7620-5bc8-4500-8bd0-e9e638bccb24
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b445c5f8be55d5290feb1318a3b937980a3e5c06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834342"
---
# <a name="label-debug-interface-access-sdk"></a>ラベル (Debug Interface Access SDK)
プログラム コード内の場所がで識別される、`SymTagLabel`シンボル。

## <a name="properties"></a>プロパティ
 次の表では、この記号の型の有効なプロパティを示します。

|プロパティ|データの種類|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|場所のオフセットの部分詳細については、次を参照してください。、 [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)します。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|場所のセクションの一部詳細については、次を参照してください。、 [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)します。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|`TRUE` 場合は、ラベルは、カスタム呼び出し規約を使用します。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|`TRUE` 場合まで戻り値のラベルを実行します。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|`TRUE` ラベルには、割り込みの戻り値が含まれています。 場合、|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|外側のコンパイル単位、ブロック、または関数の記号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文の親のシンボルの ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|ラベルがある静的な場所です。詳細については、次を参照してください。、[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)列挙体。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|ラベルの名前。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|`TRUE` ラベルが指定した場合、 [noinline](/cpp/cpp/noinline)属性。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|`TRUE` ラベルが指定した場合、 [noreturn](/cpp/cpp/noreturn)属性。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|`TRUE` 場合は、ラベルは呼び出されません。|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|メモリ内でシンボルをオフセットします。詳細については、次を参照してください。、 [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)、`LocIsRegRel`します。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|`TRUE` 場合は、コードでは、最適化されたコードのデバッグ情報を持っています。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|そのモジュール内でこのラベルの相対位置。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返します`SymTagFuncDebugLabel`(の 1 つ、 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)値)。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|実行可能イメージ内でこのラベルの位置。|

## <a name="see-also"></a>関連項目
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
- [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)