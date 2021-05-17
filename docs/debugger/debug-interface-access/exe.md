---
description: Exe は、.exe または .dll ファイルのグローバル スコープを表すため、構文上の親またはクラスの親を持たない唯一のシンボルです。
title: Exe | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- .dll files
- Exe symbol
- .exe files
- executable files, Exe symbol
ms.assetid: a781d2cf-55fe-4373-9cf1-b732864244e0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5394acaa19efed0c882d97f6ee5b633ffe1c68c0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634518"
---
# <a name="exe"></a>Exe
Exe は、.exe または .dll ファイルのグローバル スコープを表すため、構文上の親またはクラスの親を持たない唯一のシンボルです。 `SymTagExe` タグを持つシンボルはファイルごとに 1 つだけ存在します。 [IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md) メソッドは、このシンボルを返します。

## <a name="properties"></a>プロパティ
 次の表に、このシンボルの種類に対して有効なプロパティを示します。

|プロパティ|データ型|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_age](../../debugger/debug-interface-access/idiasymbol-get-age.md)|`DWORD`|この実行可能ファイルの年齢。|
|[IDiaSymbol::get_guid](../../debugger/debug-interface-access/idiasymbol-get-guid.md)|`GUID`|この実行可能ファイルの `GUID`。|
|[IDiaSymbol::get_isCTypes](../../debugger/debug-interface-access/idiasymbol-get-isctypes.md)|`BOOL`|この実行可能ファイルに関連付けられているシンボル ファイルに C の型が含まれている場合は `TRUE` (DIA SDK v8.0 以降のみ)。|
|[IDiaSymbol::get_isStripped](../../debugger/debug-interface-access/idiasymbol-get-isstripped.md)|`BOOL`|この実行可能ファイルに関連付けられているシンボル ファイルからプライベート シンボルが削除されている場合は `TRUE` (DIA SDK v8.0 以降のみ)。|
|[IDiaSymbol::get_machineType](../../debugger/debug-interface-access/idiasymbol-get-machinetype.md)|`DWORD`|ターゲット CPU を示す値 ([CV_CPU_TYPE_e 列挙型](../../debugger/debug-interface-access/cv-cpu-type-e.md)の値の 1 つ)。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|.exe ファイルの名前。|
|[IDiaSymbol::get_signature](../../debugger/debug-interface-access/idiasymbol-get-signature.md)|`DWORD`|実行可能ファイルのシグネチャ。|
|[IDiaSymbol::get_symbolsFileName](../../debugger/debug-interface-access/idiasymbol-get-symbolsfilename.md)|`BSTR`|.exe ファイルの .pdb または .dbg ファイルの完全パス。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagExe` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|

## <a name="see-also"></a>関連項目
- [IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
