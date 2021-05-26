---
title: Folder 要素 (Visual Studio プロジェクト テンプレート) | Microsoft Docs
description: Folder 要素と、プロジェクトに追加されるフォルダーを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 40e1df1d5efeab17adf60a8e1732991cb2cac02a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070129"
---
# <a name="folder-element-visual-studio-project-templates"></a>Folder 要素 (Visual Studio プロジェクト テンプレート)
プロジェクトに追加されるフォルダーを指定します。

 \<VSTemplate> \<TemplateContent>
 \<Project>
 \<Folder>

## <a name="syntax"></a>構文

```
<Folder Name="Project Folder">
    <Folder> ... </Folder>
    <ProjectItem> ... </ProjectItem>
</Folder>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須の属性です。<br /><br /> プロジェクト フォルダーの名前。|
|`TargetFolderName`|省略可能な属性です。<br /><br /> プロジェクトがテンプレートから作成されるときにフォルダーに付ける名前を指定します。 この属性は、パラメーター置換を使用してフォルダー名を作成したり、 *.zip* ファイルで直接使用できない国際文字列を使用してフォルダーに名前を付けたりする場合に便利です。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|`Folder`|プロジェクトに追加するフォルダーを指定します。 `Folder` 要素には子 `Folder` 要素を含めることができます。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|プロジェクトに追加するファイルを指定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|[Templatecontent](../extensibility/templatecontent-element-visual-studio-templates.md) の省略可能な子要素。|

## <a name="remarks"></a>解説
 `Folder` は、`Project` の省略可能な子です。

 次のいずれかの方法を使用して、プロジェクト項目をテンプレート内のフォルダーに整理できます。

- テンプレートの *.zip* ファイルにフォルダーを含め、 *.vstemplate* ファイル内のプロジェクトに追加します。これには、`Folder` 要素を使用せずに、`ProjectItem` 要素内のファイルへのパスを指定します。 これが推奨される方法です。 次に例を示します。

     `...`

     `<ProjectItem>\Folder\item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- テンプレートの *.zip* ファイルにフォルダーを含め、`Folder` 要素を使用して *.vstemplate* ファイル内のプロジェクトに追加します。 次に例を示します。

     `...`

     `<Folder name="Folder">`

     `<ProjectItem>item.cs</ProjectItem>`

     `</Folder>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- テンプレートの *.zip* ファイルにはフォルダーを含めず、`ProjectItem` 要素の `TargetFileName` 属性を使用してフォルダーを追加してください。 次に例を示します。

     `...`

     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

## <a name="example"></a>例
 次の例は、[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] Windows アプリケーションの標準プロジェクト テンプレートのメタデータを示しています。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <Folder Name="Properties">
                <ProjectItem>AssemblyInfo.cs</ProjectItem>
                <ProjectItem>Resources.resx</ProjectItem>
                <ProjectItem>Resources.Designer.cs</ProjectItem>
                <ProjectItem>Settings.settings</ProjectItem>
                <ProjectItem>Settings.Designer.cs</ProjectItem>
            </Folder>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)
