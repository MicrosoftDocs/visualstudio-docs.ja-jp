---
title: Combo 要素 | Microsoft Docs
description: Combo 要素は、コンボ ボックスに表示されるコマンドを定義します。 DropDownCombo、DynamicCombo、IndexCombo、MRUCombo の 4 種類があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 431d68b6e545506f5fc90cc5a98a52dd4f1c33ad
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904956"
---
# <a name="combo-element"></a>Combo 要素
コンボ ボックスに表示されるコマンドを定義します。 次に示すように、DropDownCombo、DynamicCombo、IndexCombo、MRUCombo の 4 種類のコンボ ボックスがあります。

## <a name="syntax"></a>構文

```xml
<combo guid="guidMyCommandSet" id="MyCommand" defaultWidth="20" idCommandList="MyCommandListID" priority="0x102" type="DropDownCombo">
  <Parent>... </Parent
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</combo>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|
|defaultWidth|必須。 コンボ ボックスのピクセル幅を指定する整数。|
|idCommandList|必須。 コンボ ボックスに表示される項目の一覧を取得するために、アクティブなコマンド ターゲットに送信される ID。 ID は、コントロールと同じ GUID スコープにあります。|
|priority|省略可能。 優先順位を指定する数値。|
|型|省略可能。 ボタンの型を指定する列挙値。<br /><br /> 指定されていない場合は、Button を使用します。<br /><br /> DropDownCombo<br /> このコンボ ボックスの内容は、VSPackage によって入力されます。 ユーザーは、このドロップダウンのテキスト ボックスには何も入力できません。<br /><br /> DynamicCombo<br /> このコンボ ボックスの内容は、VSPackage によって入力されます。 ユーザーは、このコンボ ボックスを編集することも、その中の項目を選択することもできます。<br /><br /> IndexCombo<br /> テキストではなく、項目のインデックスを生成する点を除いて、DynamicCombo と同じです。<br /><br /> MRUCombo<br /> VSPackage の代わりに統合開発環境 (IDE) によって入力されます。  ユーザーは、このコンボ ボックス内で編集できます。 IDE では、コンボ ボックスごとに最後の 16 個までのエントリが記憶されます。<br /><br /> ユーザーがコンボ ボックスで何かを選択するか、新規入力を行うと、IDE によって、適切な VSPackage に通知されます。|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent|省略可能。 ボタンの親要素。|
|CommandFlag|必須。 「[コマンド フラグ要素](../extensibility/command-flag-element.md)」を参照してください。 Button の有効な CommandFlag 値は次のとおりです。<br /><br /> - CaseSensitive<br /><br /> - CommandWellOnly<br /><br /> - DefaultDisabled<br /><br /> - DefaultInvisible<br /><br /> - DynamicVisibility<br /><br /> - FilterKeys<br /><br /> - IconAndText<br /><br /> - NoAutoComplete<br /><br /> - NoButtonCustomize<br /><br /> - NoCustomize<br /><br /> - NoKeyCustomize<br /><br /> - StretchHorizontally|
|文字列|必須。 「[Strings 要素](../extensibility/strings-element.md)」を参照してください。 子 ButtonText 要素を定義する必要があります。|
|注釈|省略可能なコメント。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Commands 要素](../extensibility/commands-element.md)|VSPackage ツール バー上のコマンドのコレクションを表します。|

## <a name="example"></a>例

```xml
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>

<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  priority="0x0500" type="DropDownCombo" defaultWidth="100"
  idCommandList="cmdidGetInsertOptionsList">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
