---
title: ShowByDefault 要素 (Visual Studio テンプレート)
description: ShowByDefault 要素と、それが false に設定されているとき、指定の TemplateGroupID の下でのみテンプレートが表示されるように指定されるしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ShowByDefault
helpviewer_keywords:
- <ShowByDefault> element [Visual Studio Templates]
- ShowByDefault element [Visual Studio Templates]
ms.assetid: 7be783f6-0ef6-42bc-924a-df9a2eba7781
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 25ba91a6276615929fed9494000abbfde07ef2b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056429"
---
# <a name="showbydefault-element-visual-studio-templates"></a>ShowByDefault 要素 (Visual Studio テンプレート)
`false` の場合、指定された [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) にのみテンプレートが表示されることを指定します。

 \<VSTemplate> \<TemplateData>
 \<ShowByDefault>

## <a name="syntax"></a>構文

```
<ShowByDefault> true/false </ShowByDefault>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テキストは、`true` または `false` である必要があります。 true の場合、すべてのプロジェクトの種類のテンプレートが表示されることを指定します。 false の場合、指定された `TemplateGroupID` にのみテンプレートが表示されます。

## <a name="remarks"></a>解説
 `ShowByDefault` は省略可能な要素です。 既定値は `true` です。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] テンプレートのメタデータの例を次に示します。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ShowByDefault>false</ShowByDefault>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [TemplateGroupID 要素 (Visual Studio テンプレート)](../extensibility/templategroupid-element-visual-studio-templates.md)
