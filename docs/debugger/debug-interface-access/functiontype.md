---
description: 一意の関数シグネチャはそれぞれ SymTagFunctionType シンボルで識別されます。
title: FunctionType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- function signature
- FunctionType symbol
ms.assetid: 646a07e7-9d4f-4e21-95e3-3e403cdd4843
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2ac1a15528783f21169427a67f47afcb2d64a81e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634515"
---
# <a name="functiontype"></a>FunctionType
一意の関数シグネチャはそれぞれ `SymTagFunctionType` シンボルで識別されます。 各パラメーターは、`SymTagFunctionArgType` タグによって、クラスの子シンボルとして識別されます。

## <a name="properties"></a>プロパティ
 次の表に、このシンボル型に対して有効な追加のプロパティを示します。

|プロパティ|データ型|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)|`DWORD`|[CV_call_e 列挙型](../../debugger/debug-interface-access/cv-call-e.md)の値のいずれか。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|この関数 (またはメソッド) がメンバーであるクラス。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|クラスの親シンボルの ID。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|関数が定数としてマークされている場合は `TRUE`。|
|[IDiaSymbol::get_count](../../debugger/debug-interface-access/idiasymbol-get-count.md)|`DWORD`|関数パラメーターの数。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|外側のコンパイル単位のシンボル。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文上の親シンボルの ID。|
|[IDiaSymbol::get_objectPointerType](../../debugger/debug-interface-access/idiasymbol-get-objectpointertype.md)|`IDiaSymbol*`|メソッドのオブジェクト ポインター ("this") の型。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagFunctionType` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|
|[IDiaSymbol::get_thisAdjust](../../debugger/debug-interface-access/idiasymbol-get-thisadjust.md)|`LONG`|メソッドの論理 "this" adjustor。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|戻り値の型のシンボル。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|型のシンボルの ID。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|関数が整列されていない場合は `TRUE`。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|関数が揮発性としてマークされている場合は `TRUE`。|

## <a name="see-also"></a>関連項目
- [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [CV_access_e 列挙型](../../debugger/debug-interface-access/cv-access-e.md)
- [FunctionArgType](../../debugger/debug-interface-access/functionargtype.md)
