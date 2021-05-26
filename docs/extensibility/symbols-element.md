---
title: Symbols 要素 | Microsoft Docs
description: Symbols 要素では、他の VSCT 要素によって使用される GUID と ID を定義します。 この記事には例が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9a013bbe438d1e4dd1f6b5149dcb7da78835fd09
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056052"
---
# <a name="symbols-element"></a>Symbols 要素
他の VSCT 要素によって使用される GUID と ID を定義します。 アンマネージド コードの場合、この情報は通常、[Extern 要素](../extensibility/extern-element.md)によって指定されるヘッダー ファイルから取得されます。 マネージド コードでは、Symbols 要素の子要素を使用して、この情報を定義します。

 既存の .cto ファイルから .vsct ファイルを作成した場合、シンボルは Symbols 要素の子として生成されます。 詳細については、「[方法: 既存の .cto ファイルから .vsct ファイルを作成する](../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)」をご覧ください。

 Symbols 要素は、プリプロセッサによって使用される名前と値のペアを定義する [Define 要素](../extensibility/define-element.md)と混同しないようにしてください。

## <a name="syntax"></a>構文

```
<Symbols>
  <GuidSymbol>... </GuidSymbol>
  <GuidSymbol>... </GuidSymbol>
</Symbols>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|なし||

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|GuidSymbol|GUID シンボルを定義します。 GuidSymbol には、name と value の 2 つの必須の属性があります。 name はシンボルの名前で、value は文字列としての GUID の値です。<br /><br /> 例:\<GuidSymbol name="guidVsPackage1Pkg"   value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />|
|IDSymbol|シンボルを定義します。 IDSymbol には、name と value の 2 つの必須の属性があります。 name はシンボルの名前で、value は文字列としてのシンボルの値です。<br /><br /> 例:\<IDSymbol name="MyMenuGroup" value="0x1020" />|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|.vsct ファイルのルート要素。|

## <a name="example"></a>例

```
<Symbols>
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
    <IDSymbol name="cmdidMyTool" value="0x0101" />
  </GuidSymbol>
</Symbols>
```

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
