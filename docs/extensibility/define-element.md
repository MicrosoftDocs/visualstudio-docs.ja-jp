---
title: Define 要素 | Microsoft Docs
description: Define 要素は、シンボルの名前と値のペアを定義します。 このシンボルは、条件付き属性によって評価できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Define
- Define element (VSCT XML schema)
ms.assetid: 5aee74e3-de41-4dc6-9618-93e158af56dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 409621410db727f933e41bae894f125dc877b4c2
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898046"
---
# <a name="define-element"></a>Define 要素
シンボルの名前と値のペアを定義します。 このシンボルは、条件付き属性によって評価できます。 詳細については、[条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。 また、「[Symbols 要素](../extensibility/symbols-element.md)」も参照してください。

## <a name="syntax"></a>構文

```
<Define name="Mode" value="Standard" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|name|必須。 シンボルの名前:<br /><br /> name="Mode"|
|value|必須。 シンボルの値:<br /><br /> value="Standard"|
|条件|省略可能。 詳細については、[条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が統合開発環境 (IDE) に提供するコマンドを表すすべての要素を定義します。 たとえば、メニュー項目、メニュー、ツール バー、コンボ ボックスなどがあります。|

## <a name="example"></a>例

```
<Define name="DEMO_UI"/>
<Define name="MODE" value="Standard"/>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
