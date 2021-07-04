---
title: Strings 要素 | Microsoft Docs
description: Strings 要素には、ButtonText 子要素と、その他の省略可能な子要素が含まれます。 テキスト文字列内のアンパサンドは、キーボード ショートカットを指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27a649c7d3a8bb808153c280921d2304de59c379
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899408"
---
# <a name="strings-element"></a>文字列要素
Strings 要素には、少なくとも **Buttontext** 子要素が含まれていることが必要です。 その以外の子要素はすべて、省略可能です。 "&" や "<" など、無効な XML 文字は、エンティティ ("&amp;" や "&lt;" など) としてコーディングする必要があります。

 テキスト文字列内のアンパサンドは、コマンドのキーボード ショートカットを指定します。

## <a name="syntax"></a>構文

```
<Strings>
  <ButtonText>... </ButtonText>
  <CommandName>... </CommandName>
</Strings>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|language|省略可能。 Language=".".|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|ButtonText|コマンド定義で、このフィールドと次の 5 つのテキスト フィールドを使用して、さまざまなメニューに表示されるテキストを指定できます。 既定では、メニュー コントローラーに `ButtonText` 要素が表示されます。 `ButtonText` 要素は、他のテキスト フィールドが空白である場合も既定値となります。 他のテキスト フィールドが指定されている場合でも、`ButtonText` 要素を空白にすることはできません。|
|ToolTipText|`ToolTipText` フィールドは、メニュー項目のツール ヒントに表示されるテキストを指定します。<br /><br /> `ToolTipText` フィールドが空白の場合は、`ButtonText` フィールドが使用されます。|
|MenuText|`MenuText` フィールドは、メイン メニュー、ツール バー、ショートカット メニュー、またはサブメニュー上にコマンドがある場合にコマンドとして表示されるテキストを指定します。 `MenuText` フィールドが空白の場合は、統合開発環境 (IDE) によって `ButtonText` フィールドが使用されます。 `MenuText` フィールドはローカライズにも使用できます。<br /><br /> ショートカット メニューの場合、`MenuText` フィールドは、ショートカット メニューのツール バーに表示される名前です。このため、IDE でショートカット メニューをカスタマイズできます。 したがって、ショートカット メニューには、具体的な名前を指定してください。たとえば、"ショートカット" ではなく、"ウィジェット パッケージのショートカット メニュー" を使用します。<br /><br /> `MenuText` フィールドが指定されていない場合は、`ButtonText` フィールドが使用されます。|
|CommandName|`CommandName` フィールドは、 **[カスタマイズ]** ダイアログ ボックス ( **[ツール]** メニューの **[カスタマイズ]** をクリックすると表示される) の **[コマンド]** タブのキーボード カテゴリに表示されるテキストを指定します。|
|CanonicalName|英語の `CanonicalName` フィールドは、コマンドの名前を英語のテキストで指定します。これを、 **[コマンド]** ウィンドウに入力してメニュー項目を実行できます。 文字、数字、アンダースコア、および埋め込まれたピリオド以外の文字は IDE により削除されます。 そして、このテキストが `ButtonText` フィールドに連結されてコマンドが定義されます。 たとえば、 **[ファイル]** メニューの **[新しいプロジェクト]** が、NewProject というコマンドになります。<br /><br /> 英語の `CanonicalName` フィールドが指定されていない場合は、IDE によって `ButtonText` フィールドが使用され、文字、数字、アンダースコア、および埋め込まれたピリオド以外はすべて削除されます。 たとえば、ボタン テキスト "&Define Commands..." は、アンパサンド、スペース、および省略記号が削除され、"DefineCommands" になります。<br /><br /> `TextChanges` フラグが指定されており、コマンドのテキストが変更された場合、 **[コマンド]** ウィンドウによって認識される、対応するコマンドは変更されません。元の `ButtonText` フィールド、または英語の `CanonicalName` フィールドの正規の形式のままです。|
|LocCanonicalName|`LocCanonicalName` フィールドは、英語の `CanonicalName` フィールドと同様に動作しますが、ローカライズされたコマンド テキストの指定が可能です。 両方の正規フィールドを指定できます。 IDE では、 **[コマンド]** ウィンドウに入力されたテキストが解析され、コマンドに関連付けられるだけであるため、英語と英語以外の両方のテキストを、同じコマンドに関連付けることができます。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Button 要素](../extensibility/button-element.md)|ユーザーが操作できる要素を定義します。|
|[Menu 要素](../extensibility/menu-element.md)|1 つのメニュー項目を定義します。|
|[Combo 要素](../extensibility/combo-element.md)|コンボ ボックスに表示されるコマンドを定義します。|

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
