---
title: KeyBinding 要素 | Microsoft Docs
description: KeyBinding 要素では、コマンドのキーボード ショートカットを指定します。 コマンドでは、単一キー バインドとデュアル キー バインドの両方を関連付けることができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9162d9b21c54577e48f4dced6ddddd7138c9de66
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074094"
---
# <a name="keybinding-element"></a>KeyBinding 要素
KeyBinding 要素では、コマンドのキーボード ショートカットを指定します。

 コマンドでは、単一キー バインドとデュアル キー バインドの両方を関連付けることができます。 単一キー バインドの例は、 **[保存]** コマンドの **Ctrl**+**S** です。 デュアル キー バインドでは、コマンドをトリガーするために 2 つの連続するキーの組み合わせが必要です。 デュアル キー バインドの例は、ブックマークを設定するための <strong>Ctrl *+</strong>K<strong>、</strong>Ctrl<strong>+</strong>K** です。

## <a name="syntax"></a>構文

```
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。|
|id|必須。|
|エディター|必須。 エディター GUID は、このキーボード ショートカットがアクティブになる編集コンテキストを示します。 グローバル バインド スコープ値は "guidVSStd97" です。|
|key1|必須。 有効な値には、すべての入力可能な英数字に加え、先頭に 0x を付けた 2 桁の 16 進数値、[VK_constants](/windows/desktop/inputdev/virtual-key-codes) が含まれます。|
|mod1|省略可能。 スペースで区切られた **Ctrl**、**Alt**、および **Shift** の任意の組み合わせ。|
|key2|省略可能。 有効な値には、すべての入力可能な英数字に加え、先頭に 0x を付けた 2 桁の 16 進数値、[VK_constants](/windows/desktop/inputdev/virtual-key-codes) が含まれます。|
|mod2|省略可能。 スペースで区切られた **Ctrl**、**Alt**、および **Shift** の任意の組み合わせ。|
|エミュレーター|省略可能。|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent||
|注釈||

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[KeyBindings 要素](../extensibility/keybindings-element.md)|KeyBinding 要素とその他の KeyBinding グループをグループ化します。|

## <a name="example"></a>例

```
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>関連項目
- [KeyBindings 要素](../extensibility/keybindings-element.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
