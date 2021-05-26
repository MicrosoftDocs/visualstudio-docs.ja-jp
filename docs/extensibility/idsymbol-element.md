---
title: IDSymbol 要素 | Microsoft Docs
description: IDSymbol 要素には、メニュー、グループ、またはコマンドを表す GUID:ID ペアの ID が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f59089ab981bc97100386b3e1907ef903ede3bd0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069843"
---
# <a name="idsymbol-element"></a>IDSymbol 要素
`IDSymbol` 要素には、メニュー、グループ、またはコマンドを表す GUID:ID ペアの ID が含まれています。 GUID は親 `GuidSymbol` 要素から取得されます。 `IDSymbol` 要素には、`value` 属性に含まれている ID のフレンドリ名を提供する `name` 属性があります。

## <a name="syntax"></a>構文

```xml
<IDSymbol name=ElementName value="0x0010" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|name|必須。 ID シンボルの名前。|
|value|必須。 ID シンボルの数値 ID 値。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[GuidSymbol 要素](../extensibility/guidsymbol-element.md)|メニュー、グループ、またはコマンドを表す GUID:ID ペアの GUID が含まれています。 複数の `IDSymbol` 要素をグループ化します。|

## <a name="remarks"></a>解説
 指定された `GuidSymbol` 要素内のすべての `IDSymbol` 要素は、一意の `value` である必要があります。 ただし、同一の値を持つ `IDSymbol` 要素は、異なる親を持つ限り 1 つのパッケージ内に存在できます。

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
