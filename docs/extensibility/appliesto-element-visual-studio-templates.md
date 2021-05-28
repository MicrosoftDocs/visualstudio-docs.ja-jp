---
title: AppliesTo 要素 (Visual Studio テンプレート) | Microsoft Docs
description: AppliesTo 要素と、1 つ以上の機能に一致する省略可能な式を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 8fb1334b-d78c-405f-98b4-786e9f6b58d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 340ac4db04b62abade9c6572335e28c9fb27b495
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097475"
---
# <a name="appliesto-element-visual-studio-templates"></a>AppliesTo 要素 (Visual Studio テンプレート)

省略可能な式を 1 つ以上の機能と一致するように指定します (<xref:Microsoft.VisualStudio.Shell.Interop.VsProjectCapabilityExpressionMatcher> を参照)。 機能は、プロジェクト タイプによって、階層を介して、プロパティ [__VSHPROPID5.VSHPROPID_ProjectCapabilities](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID5.VSHPROPID_ProjectCapabilities>) として公開されます。 このようにすると、共通の適用可能な機能を持つ複数のプロジェクトの種類によってテンプレートを共有できます。

この要素は省略可能です。 テンプレート ファイルには、最大で 1 つのインスタンスがあります。 この要素は、現在選択されているアクティブなプロジェクトの機能に基づいて、項目テンプレートを適用可能として利用できるようにするだけです。 項目テンプレートを適用不可にするためには使用できません。 `AppliesTo` が存在しない場合、または式を正常に利用できない場合は、製品の以前のバージョンの場合と同様に、テンプレートを適用可能にするために `TemplateID` または `TemplateGroupID` が使用されます。

Visual Studio 2013 更新プログラム 2 で導入されました。 適切なバージョンを参照するには、[Visual Studio 2013 SDK Update 2 で配信されるアセンブリの参照](/previous-versions/dn632168(v=vs.120))に関するページを参照してください。

```xml
<VSTemplate>
   <TemplateData>
      <AppliesTo>
```

## <a name="syntax"></a>構文

```xml
<AppliesTo>Capability1</AppliesTo>
```

## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

なし。

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類します。|

## <a name="text-value"></a>テキスト値

テキスト値が必要です。 このテキストでプロジェクトの機能を指定します。

有効な式の構文は次のように定義されます。

- "(VisualC &#124; CSharp) + (MSTest &#124; NUnit)" などの機能の式。

- "&#124;" は OR 演算子です。

- "&" および "+" 文字は、どちらも AND 演算子です。

- "!" 文字は NOT 演算子です。

- かっこで囲むことで、評価の優先順位が強制的に設定されます。

- Null または空の式は、一致として評価されます。

- プロジェクトの機能には、予約文字 "'`:;,+-*/\\!~&#124;&%$@^()={}[]<>? を除く文字を使用できます。 を除く文字を使用できます。

## <a name="example"></a>例

次の例に、3 種類のテンプレートを示します。 `Template1` は、C# のすべてのプロジェクト タイプ、または `WindowsAppContainer` 機能をサポートする他のプロジェクト タイプに適用されます。 `Template2` は、任意の種類のすべての C# プロジェクトに適用されます。 `Template3` は、`WindowsAppContainer` プロジェクトではない C# プロジェクトに適用されます。

```xml
<!--  Template 1 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp | WindowsAppContainer</AppliesTo>
    </TemplateData>
</VSTemplate>

<!--  Template 2 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp</AppliesTo>
    </TemplateData>
</VSTemplate>

<!--  Template 1 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp_Class + (!WindowsAppContainer)</AppliesTo>
    </TemplateData>
</VSTemplate>
```

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
