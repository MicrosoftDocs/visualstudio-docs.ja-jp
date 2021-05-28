---
title: CommandPlacements 要素 | Microsoft Docs
description: CommandPlacements 要素では、CommandPlacement 要素とその他の CommandPlacements グループをグループ化します。 CommandPlacements 要素は省略可能です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CommandPlacements
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 78a5724a-3b9f-4c78-9c0d-8faa3924f81c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3547d1c5b94285ce113b3a3c112568aa5a9a5f65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089603"
---
# <a name="commandplacements-element"></a>CommandPlacements 要素
CommandPlacements 要素では、CommandPlacement 要素とその他の CommandPlacements グループをグループ化します。

 CommandPlacements 要素は省略可能です。 コマンド、グループ、メニューをセカンダリの場所に含める必要がない場合は、このセクションを *vsct* ファイルに含める必要はありません。

## <a name="syntax"></a>構文

```xml
<CommandPlacements>
  <CommandPlacement>... </CommandPlacement>
  <CommandPlacement>... </CommandPlacement>
</CommandPlacements>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|CommandPlacements|CommandPlacement 要素とその他の CommandPlacements をグループ化します。|
|[CommandPlacement 要素](../extensibility/commandplacement-element.md)|ボタン、グループ、およびメニューを複数のグループまたはメニューに含められるようにします。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|コマンドを表すすべての要素を定義します。|

## <a name="example"></a>例

```xml
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>関連項目
- [CommandPlacement 要素](../extensibility/commandplacement-element.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
