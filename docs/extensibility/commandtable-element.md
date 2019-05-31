---
title: CommandTable 要素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9bb10232c725eb2f538df73f6a7ca98e534a4c14
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341808"
---
# <a name="commandtable-element"></a>CommandTable 要素
CommandTable のルート要素は、 *.vsct*ファイル。 これは、実際のレイアウトと、IDE に VSPackage を提供するコマンドの種類を定義するファイルです。 コマンドは、メニュー項目、メニューのツールバー、およびコンボ ボックスに含めることができます。 詳細については、次を参照してください。 [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)します。

## <a name="syntax"></a>構文

```xml
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema" >
  <Extern>... </Extern>
  <Include>... </Include>
  <Define>... </Define>
  <Commands>... </Commands>
  <CommandPlacements>... </CommandPlacements>
  <VisibilityConstraints>... </VisibilityConstraints>
  <KeyBindings>... </KeyBindings>
  <UsedCommands... </UsedCommands>
  <Symbols>... </Symbols>
</CommandTable>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|-----------| - |
| xmlns | 必須。 XML 名前空間:<br /><br /> xmlns="<http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable>"<br /><br /> xmlns:xs="<http://www.w3.org/2001/XMLSchema>" |
| language | 任意。 言語属性がすべての既定の言語を指定するため\<文字列 > コマンド テーブル内の要素。  言語が指定されていない場合は、現在のプロセスの言語が使用されます。<br /><br /> language="en-us" |

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[Extern 要素](../extensibility/extern-element.md)|任意。 コンパイラのプリプロセッサ ディレクティブが含まれています。|
|[要素を含める](../extensibility/include-element.md)|任意。 コンパイルに含める任意のファイルへのパスが含まれています。|
|[要素を定義します。](../extensibility/define-element.md)|任意。 その名前と値のシンボルを定義します。|
|[Commands 要素](../extensibility/commands-element.md)|任意。 すべての他の要素を含む VSPackage のすべてのコマンドを定義する親要素です。|
|[CommandPlacements 要素](../extensibility/commandplacements-element.md)|任意。 コマンド バーで、コマンドが配置されるかを定義します。|
|[VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)|任意。 コマンドとツールバーの静的な可視性を判断します。|
|[KeyBindings 要素](../extensibility/keybindings-element.md)|任意。 コマンドのショートカット キーの組み合わせを指定します。|
|[UsedCommands 要素](../extensibility/usedcommands-element.md)|任意。 必要に応じてその他の Vspackage で最初にサポートされる機能の独自のバージョンを実装するために VSPackage を使用できます。|
|[Symbols 要素](https://www.microsoft.com/download/details.aspx?id=55984)|任意。 コンパイラのシンボル データ--Guid、Id、およびなど--が含まれています。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|なし||

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)