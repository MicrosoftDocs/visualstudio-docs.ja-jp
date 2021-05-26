---
title: ProjectSubType 要素 (Visual Studio テンプレート) | Microsoft Docs
description: ProjectSubType 要素と、それを使用して、テンプレートを ProjectType 要素で指定されている値のサブカテゴリに分類する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectSubType
helpviewer_keywords:
- ProjectSubType element [Visual Studio Templates]
- <ProjectSubType> element [Visual Studio Templates]
ms.assetid: f6895cd4-3e95-4f0e-aa9e-8c7750f46ed4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 02dd5573de12e4626c267fa014f6c7fc8f243b72
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068677"
---
# <a name="projectsubtype-element-visual-studio-templates"></a>ProjectSubType 要素 (Visual Studio テンプレート)
テンプレートを `ProjectType` 要素で指定されている値のサブカテゴリに分類します。

 \<VSTemplate> \<TemplateData>
 \<ProjectSubType>

## <a name="syntax"></a>構文

```xml
<ProjectSubType> SubType </ProjectSubType>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 この値は、テンプレートのサブカテゴリを指定します。

## <a name="remarks"></a>解説
 `ProjectSubType` は、`TemplateData` の子要素で、省略可能な要素です。

 `ProjectSubType` 要素は、[ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) 要素のサブカテゴリを提供します。 この値には、次のものを含めることができます。

- `SmartDevice-NETCFv1`: このテンプレートが [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] バージョン 1.0 を対象とすることを指定します。

- `SmartDevice-NETCFv2`: このテンプレートが [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] バージョン 2.0 を対象とすることを指定します。

  テンプレートに `Web` の値を持つ `ProjectType` 要素が含まれている場合、`ProjectSubType` 要素は、そのテンプレートのプログラミング言語を指定します。 この要素には、次の値を含めることができます。

- `CSharp`: このテンプレートで [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] Web プロジェクトまたは項目を作成することを指定します。

- `VisualBasic`: このテンプレートで [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] Web プロジェクトまたは項目を作成することを指定します。

## <a name="example"></a>例
 次の例は、[!INCLUDE[Compact](../extensibility/includes/compact_md.md)] バージョン 2.0 を対象とする [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] デバイス アプリケーションのプロジェクト テンプレートのメタデータを示しています。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic device template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProjectSubType>SmartDevice-NETCFv2</ProjectSubType>
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
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [ProjectType 要素 (Visual Studio テンプレート)](../extensibility/projecttype-element-visual-studio-templates.md)
