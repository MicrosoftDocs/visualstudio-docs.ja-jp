---
title: Commands 要素 | Microsoft Docs
description: Commands 要素は、VSPackage ツールバー上のコマンドのコレクションを表し、メニュー、グループ、ボタン、コンボ ボックス、ビットマップのセクションを含むことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element (VSCT XML schema)
- VSCT XML schema elements, Commands
ms.assetid: 47cf16a5-d78b-452e-86f6-b5893856dddf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 671e855a31af17310fdab58689d8775b490cb93a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089590"
---
# <a name="commands-element"></a>Commands 要素
VSPackage ツール バー上のコマンドのコレクションを表します。 コレクションには、メニュー、グループ、ボタン、コンボ ボックス、ビットマップの 5 つのサブセクションを含めることができます。

 たとえば、各サブセクションの子要素 \<Menu> は、GUID と数値識別子のペアである一意のコマンド ID によって識別されます。 GUID は "コマンド セット" を識別し、論理的に関連するコマンドをグループ化するために使用されます。 VSPackage は、他の VSPackage で定義されているコマンド ID との競合を避けるために、独自のコマンド セットを定義する必要があります。

## <a name="syntax"></a>構文

```xml
<Commands package="GuidMyPackage" >
  <Menus>... </Menus>
  <Groups>... </Groups>
  <Buttons>... </Buttons>
  <Combos>... </Combos>
  <Bitmaps>... </Bitmaps>
</Commands>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|パッケージ|コマンドを提供する VSPackage を識別する GUID。<br /><br /> たとえば、package= "guidVsPackage1Pkg" です。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[Menus 要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|
|[Groups 要素](../extensibility/groups-element.md)|VSPackage のコマンド グループを定義するエントリが含まれます。|
|[Buttons 要素](../extensibility/buttons-element.md)|Button 要素をグループ化します。|
|[Bitmaps 要素](../extensibility/bitmaps-element.md)|Bitmap 要素をグループ化します。|
|[Combos 要素](../extensibility/combos-element.md)|コンボ ボックス要素をグループ化します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が IDE に提供するコマンドを表すすべての要素を定義します。 定義できる要素は、メニュー項目、メニュー、ツール バー、およびコンボ ボックスです。|

## <a name="example"></a>例
 次の例は、[Commands 要素](../extensibility/commands-element.md)を使用する方法を示します。

```
<Commands package="guidMyPackage">
    <Menus>
      <Menu Condition="'%(DEBUG)' != 'true'"
        guid="cmdSetGuidMyProductCommands" id="menuIDMainMenu"
        priority="0x0000" type="Menu">
        <Annotation>
          <Documentation>this is an annotation</Documentation>
          <AppInfo>
            <CustomData>
              <CustomSubElement>Some data</CustomSubElement>
            </CustomData>
          </AppInfo>
        </Annotation>
        <CommandFlag>AlwaysCreate</CommandFlag>
        <Strings>
          <ButtonText>MainMenu</ButtonText>
        </Strings>
      </Menu>
  </Menus>
<Commands>
```

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
