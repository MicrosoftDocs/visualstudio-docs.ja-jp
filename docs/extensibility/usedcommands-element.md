---
title: UsedCommands 要素 | Microsoft Docs
description: UsedCommands 要素は、UsedCommand 要素と他の UsedCommands グループをグループ化します。 UsedCommands 要素は省略可能です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UsedCommands
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 5e000ee0-a919-46e9-9277-2a0659f1eb78
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 21233527c9fcfb97fd45a8eeed60c04927df8ba1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903035"
---
# <a name="usedcommands-element"></a>UsedCommands 要素
UsedCommands 要素は、UsedCommand 要素と他の UsedCommands グループをグループ化します。

 UsedCommands 要素は省略可能です。 パッケージの外部で定義されたコマンドを呼び出さない場合は、このセクションを .vsct ファイルに含める必要はありません。

## <a name="syntax"></a>構文

```
<UsedCommands condition="Defined(DEBUG)">
  <UsedCommand ... />
</UsedCommands>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[UsedCommand 要素](../extensibility/usedcommand-element.md)|他のコードによって実装されるコマンド。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage で統合開発環境 (IDE) に提供されるコマンド (メニュー項目、メニュー、ツールバー、コンボ ボックスなど) を表すすべての要素を定義します。|

## <a name="example"></a>例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>関連項目
- [UsedCommand 要素](../extensibility/usedcommand-element.md)
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
