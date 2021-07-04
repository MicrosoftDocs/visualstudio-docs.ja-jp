---
title: Button 要素 | Microsoft Docs
description: Button 要素では、ユーザーが操作できる要素を定義します。 ボタンは、Button、MenuButton、SplitDropDown のいくつかの種類から選択できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 96dccf51-2b00-4700-9d28-924b34c21ecd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 630d848c40b13a929c3dd91b47e1c35529efaa50
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901748"
---
# <a name="button-element"></a>Button 要素
ユーザーが操作できる要素を定義します。 ボタンは、Button、MenuButton、SplitDropDown のいくつかの種類から選択できます。

## <a name="syntax"></a>構文

```
<Button guid="guidMyCommandSet" id="MyCommand" priority="0x102" type="button">
  <Parent>... </Parent>
  <Icon>... </Icon>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Button>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|
|priority|省略可能。 優先順位を指定する数値。|
|型|省略可能。 ボタンの種類を指定する列挙値。<br /><br /> 指定されていない場合は、Button を使用します。<br /><br /> ボタン<br /> ツール バー (通常はアイコン化されたボタンとして)、メニュー、コンテキスト メニューに表示される標準コマンド。<br /><br /> MenuButton<br /> コマンドは実行しないが、別のメニューを生成するメニュー項目。<br /><br /> SplitDropDown<br /> Microsoft Word の標準ツール バーにある [元に戻す] ボタンや [やり直し] ボタンなどのコントロール。|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[親要素](../extensibility/parent-element.md)|省略可能。 ボタンの親要素。|
|[Icon 要素](../extensibility/icon-element.md)|省略可能。 ボタンに関連付けられているアイコン。|
|[コマンド フラグ要素](../extensibility/command-flag-element.md)|必須。 Button の有効な CommandFlag 値は次のとおりです。<br /><br /> - AllowParams<br /><br /> - CommandWellOnly<br /><br /> - DefaultDisabled<br /><br /> - DefaultInvisible<br /><br /> - DontCache<br /><br /> - DynamicItemStart<br /><br /> - DynamicVisibility<br /><br /> - FixMenuController<br /><br /> - IconAndText<br /><br /> - NoButtonCustomize<br /><br /> - NoCustomize<br /><br /> - NoKeyCustomize<br /><br /> - NoShowOnMenuController<br /><br /> - Pict<br /><br /> - PostExec<br /><br /> - ProfferedCmd<br /><br /> - RouteToDocs<br /><br /> - TextCascadeUseBtn<br /><br /> - TextMenuUseButton<br /><br /> - TextChanges<br /><br /> - TextChangesButton<br /><br /> - TextContextUseButton<br /><br /> - TextMenuCtrlUseMenu<br /><br /> - TextMenuUseButton<br /><br /> - TextOnly|
|[Strings 要素](../extensibility/strings-element.md)|必須。 子の [ButtonText 要素](../extensibility/buttontext-element.md)を定義する必要があります。|
|注釈|省略可能なコメント。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Buttons 要素](../extensibility/buttons-element.md)|Button 要素をグループ化します。|

## <a name="example"></a>例
 次の例では、 *.vsct* ファイルでボタンを定義しています。

 ```xml
<Button guid="guidMenuTextCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
    <Parent guid="guidMenuTextCmdSet" id="MyMenuGroup" />
    <Icon guid="guidImages" id="bmpPic1" />
    <CommandFlag>TextChanges</CommandFlag>
    <Strings>
          <CommandName>cmdidMyCommand</CommandName>
          <ButtonText>My Command name</ButtonText>
    </Strings>
</Button>
 ```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
