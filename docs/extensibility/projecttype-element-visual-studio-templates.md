---
title: ProjectType 要素 (Visual Studio テンプレート) | Microsoft Docs
description: ProjectType 要素について説明し、これにより、[新しいプロジェクト] ダイアログ ボックスまたは [新しい項目の追加] ダイアログ ボックスに表示されるようにプロジェクト テンプレートをカテゴリ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d494d27b2a3302d0beff68b770d0172edb520f35
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068688"
---
# <a name="projecttype-element-visual-studio-templates"></a>ProjectType 要素 (Visual Studio テンプレート)
プロジェクト テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスの指定したグループ内にテンプレートを表示するようにします。

> [!WARNING]
> プロジェクト テンプレートは、Visual Studio 2012 以降の C++ でサポートされています。 これらは、Visual Studio 2010 以前のバージョンの C++ ではサポートされていません。

 \<VSTemplate> \<TemplateData>
 \<ProjectType>

## <a name="syntax"></a>構文

```xml
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 この値で、テンプレートから作成されるプロジェクトの種類を指定します。値には、次のいずれかの値を含める必要があります。

- `CSharp` : テンプレートが [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] のプロジェクトまたはアイテムを作成するよう指定します。

- `VisualBasic` : テンプレートが [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] のプロジェクトまたはアイテムを作成するよう指定します。

- `Web`: テンプレートが Web プロジェクトまたは Web アイテムを作成するよう指定します。 `ProjectType` 要素にこの値が含まれている場合、プロジェクトまたは項目の言語は [ProjectSubType 要素 (Visual Studio テンプレート)](../extensibility/projectsubtype-element-visual-studio-templates.md) で定義されます。

## <a name="remarks"></a>解説
 `ProjectType` は `TemplateData` に必須の子要素です。

 `ProjectType` 要素の値は、 **[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスのどの場所にテンプレートを置くかを示します。 たとえば、`CSharp` の `ProjectType` 値を持つテンプレートは、 **[新しいプロジェクト]** ダイアログ ボックスの **[Visual C#]** ノードに表示されます。

 テンプレートのサブタイプは、[ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) 要素を使用して指定できます。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
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
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [ProjectSubType 要素 (Visual Studio テンプレート)](../extensibility/projectsubtype-element-visual-studio-templates.md)
