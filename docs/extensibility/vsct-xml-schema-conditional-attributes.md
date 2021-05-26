---
title: VSCT XML スキーマの条件付き属性 | Microsoft Docs
description: VSCT XML スキーマのリストと項目に条件付き属性を適用する方法について説明します。 属性が true または false に評価され、結果の出力が制御されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5bc1bcb9d80474b467e90de6262e797087589065
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062357"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>VSCT XML スキーマの条件付き属性
条件付き属性は、すべてのリストと項目に適用できます。 論理演算子と記号の展開式が true または false に評価されます。 true の場合は、関連付けられているリストまたは項目が結果の出力に含まれます。

 トークンの展開を他のトークンの展開または定数に照らしてテストできます。 `Defined()` 関数では、値がない場合も含めて、特定の名前が定義されているかどうかをテストします。

 条件属性がリストに適用されると、リスト内のすべての子要素にその条件が適用されます。 子要素自体に条件属性が含まれている場合、その条件は AND 演算によって親の式と結合されます。

 値 1、'1'、'true' は true と評価され、0、'0'、'false' は false と評価されます。

## <a name="operators"></a>演算子
 条件式を評価するには、次の演算子を使用します。

|演算子|定義|
|--------------|----------------|
|(,)|グループ化|
|!|論理 NOT|
|\<, >, \<=, >=, ==, !=|関係と比較|
|and|ブール型|
|or|ブール型|

## <a name="examples"></a>例

```xml
<Menu Condition="Defined(DEBUG)" ...
</Menu>

<Menu Condition="%(SKU_MODE) = 'Demo'" ...
</Menu>

<Menus Condition="Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>

<Menus Condition="Defined(DEMO_SKU)">
    <Menus Condition="!Defined(DEBUG)">
        <Menu ...
        </Menu>
    </Menus>

    <Menu ...
    </Menu>
</Menus>

<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))
and !Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
