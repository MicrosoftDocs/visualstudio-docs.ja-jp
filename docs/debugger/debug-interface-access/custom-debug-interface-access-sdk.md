---
title: カスタム (Debug Interface Access SDK) | Microsoft Docs
description: Visual Studio の Debug Interface Access SDK でカスタム シンボルの種類 (SymTagCustom タグで識別されます) に関する参照情報を検索します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Custom symbol
ms.assetid: a219fc83-d2a8-4bc5-b7e1-bfafeb247f16
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 322619bbfa759d97061aa3b62ddc65fde43db8e4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634197"
---
# <a name="custom-debug-interface-access-sdk"></a>カスタム (Debug Interface Access SDK)
一部のコンパイラでは、標準的な字句シンボルの種類で識別されないシンボルが導入されています。 これらのシンボルは、`SymTagCustom` タグによって識別されます。

## <a name="properties"></a>プロパティ
 次の表に、このシンボルの種類に対して有効なプロパティを示します。

|プロパティ|データ型|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_dataBytes](../../debugger/debug-interface-access/idiasymbol-get-databytes.md)|`BYTE`|シンボルに関連付けられているデータの配列。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagCustom` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|

## <a name="see-also"></a>関連項目
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)