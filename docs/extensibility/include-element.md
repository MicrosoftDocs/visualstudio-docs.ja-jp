---
title: 要素を含める |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Include
helpviewer_keywords:
- Include element (VSCT XML schema)
- VSCT XML schema elements, Include
ms.assetid: c923dfe6-084a-4105-aec1-f0a3f8399c54
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d77cca0b197f939170fc92f4d7d07bcadae8b53d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861802"
---
# <a name="include-element"></a>要素を含める
Include 要素に存在するファイルの指定で指定された現在のファイルに挿入するためのパスを含めます。  すべてのシンボルよぶ型が定義されているコンパイルの結果の一部になります。

## <a name="syntax"></a>構文

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|href|必須。 ヘッダー ファイルへのパス:<br /><br /> href="stdidcmd.h"|
|条件|任意。 参照してください[条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)します。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|なし。|なし。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|すべてのコマンドを表す要素の定義: メニュー項目、メニューのツールバー、およびコンボ ボックスは、-、IDE に VSPackage を提供します。|

## <a name="example"></a>例

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)