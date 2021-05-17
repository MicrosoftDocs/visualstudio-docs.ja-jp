---
description: コンパイルされたプログラムに関するデバッグ情報は、プログラム データベース (.pdb) ファイルにシンボルとして格納され、Debug Interface Access (DIA) SDK API を使用してアクセスできます。
title: シンボルとシンボル タグ | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK]
ms.assetid: 2ee3a262-cda6-48bf-b799-a37edde6c8b8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 98631149e5a53c13bfc9b12b0d6de165c345e29a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634556"
---
# <a name="symbols-and-symbol-tags"></a>シンボルとシンボル タグ
コンパイルされたプログラムに関するデバッグ情報は、プログラム データベース (.pdb) ファイルにシンボルとして格納され、Debug Interface Access (DIA) SDK API を使用してアクセスできます。 すべてのシンボルには、[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) と [IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md) プロパティがあります。 `symTag` プロパティは、[SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の列挙体によって定義されているシンボルの種類を示します。 `symIndexId` プロパティは、シンボルの各インスタンスの一意識別子を含む `DWORD` 値です。

 シンボルには、シンボルに関する追加情報と他のシンボル への参照を指定できるプロパティもあります (多くの場合、[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md) または [IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md))。 参照が含まれているプロパティを照会すると、参照が [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトとして返されます。 このようなプロパティは、同じ名前の、ただし"Id" というサフィックスが付けられた、別のプロパティと常にペアになります (たとえば、[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md) や [IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md) など)。 「[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)」、「[シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)」、および「[シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)」の表には、さまざまな種類の各シンボルについてプロパティの概要が示されています。 これらのプロパティには、他のシンボルに関する関連情報や他のシンボルへの参照が含まれている場合があります。 `*Id` プロパティは、関連するプロパティの序数識別子にすぎないため、追加の説明は省略されています。 これらは、パラメーターを明確にするために必要な場合にのみ言及されています。

 プロパティへのアクセスを試みたとき、エラーが発生せず、シンボルのプロパティに値が割り当てられている場合、プロパティの "get" メソッドは `S_OK` を返します。 戻り値が `S_FALSE` の場合は、プロパティが現在のシンボルに対して無効であることを示します。

## <a name="in-this-section"></a>このセクションの内容

[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)

シンボルが持つことができるさまざまな種類の場所について説明します。

[シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)

ファイル、モジュール、関数など、構文階層を形成するシンボル型について説明します。

[シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)

クラス、配列、関数の戻り値の型など、さまざまな言語要素に対応するシンボル型について説明します。

## <a name="see-also"></a>関連項目

- [Debug Interface Access SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)
