---
title: Extern 要素 | Microsoft Docs
description: Extern 要素は、コンパイル時に、.vsct ファイルとマージする外部ヘッダー (.h) ファイルを参照します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5771dbc1c6b17b0f488d42c30a036ff1d90a5a18
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074991"
---
# <a name="extern-element"></a>Extern 要素
Extern 要素は、コンパイル時に、 *.vsct* ファイルとマージする外部ヘッダー ( *.h*) ファイルを参照します。 マージするファイルは、VSCT コンパイラに提供されるインクルード パスに存在するか、[Include 要素](../extensibility/include-element.md)によって参照されている必要があります。 ファイルは、他の *.vsct* ファイルや C++ ヘッダー ファイルなどになります。

 ヘッダー ファイル内の定義は、"#define [Symbol] [Value]" の形式にする必要があります。値は以前に定義されている場合、別のシンボルになることがあります。 定義は、コマンド項目の条件付きステートメントで使用できます。 実際に使用されていないシンボルはすべて破棄されます。

 CommandTable 要素 Extern 要素

## <a name="syntax"></a>構文

```xml
<Extern href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|href|必須。 ヘッダー ファイルのパス:<br /><br /> href="stdidcmd.h"|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|
|language|省略可能。 コマンド テーブル内のすべての [\<Strings>](../extensibility/strings-element.md) 要素の既定の言語:<br /><br /> language="en-us"|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[なし] :|なし。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage によって IDE に提供されるコマンドを表すすべての要素 (つまり、メニュー項目、メニュー、ツールバー、およびコンボ ボックス) を定義します。|

## <a name="example"></a>例

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-
  18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <Extern href="C:\VSCore\vscommon\inc\vsshlids.h"/>
    ...
  <Commands package="guidMyPackage">
</CommandTable>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
