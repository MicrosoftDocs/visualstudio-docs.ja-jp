---
title: Project 要素 (Visual Studio テンプレート) | Microsoft Docs
description: Project 要素と、それを使用して、プロジェクトに追加するファイルまたはディレクトリを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Project
helpviewer_keywords:
- Project element [Visual Studio Templates]
- <Project> element [Visual Studio Templates]
ms.assetid: 1da15ea6-26e2-462b-a03e-584ef4996579
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 52bfb5f65aa9d42c46eece619a21152c51e8fa28
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068805"
---
# <a name="project-element-visual-studio-templates"></a>Project 要素 (Visual Studio テンプレート)
プロジェクトに追加するファイルまたはディレクトリを指定します。

 \<VSTemplate> \<TemplateContent>
 \<Project>

## <a name="syntax"></a>構文

```
<Project
    File="MyProject.proj"
    TargetFileName="MyTargetProject.proj"
    ReplaceParameters="true/false">
    IgnoreProjectParameter="$myCustomParameter$"
        ...
</Project>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`File`|必須の属性です。<br /><br /> テンプレート *.zip* ファイル内のプロジェクト ファイルの名前を指定します。|
|`ReplaceParameters`|省略可能な属性です。<br /><br /> このプロジェクト ファイルに、テンプレートからプロジェクトが作成されるときに置き換える必要があるパラメーター値が含まれているかどうかを指定するブール値。 既定値は `false` です。|
|`TargetFileName`|省略可能な属性です。<br /><br /> テンプレートからプロジェクトが作成されるときのプロジェクト ファイルの名前を指定します。|
|`IgnoreProjectParameter`|省略可能な属性です。<br /><br /> このプロジェクトを現在のソリューションに追加する必要があるかどうかを指定します。 パラメーター置換ファイル内にカスタム パラメーター "$*myCustomParameter*$" の値が存在する場合、プロジェクトは作成されますが、現在開いているソリューションの一部としては追加されません。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[フォルダー](../extensibility/folder-element-visual-studio-project-templates.md)|省略可能な要素です。<br /><br /> プロジェクトに追加するフォルダーを指定します。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)|省略可能な要素です。<br /><br /> プロジェクトに追加するファイルを指定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必須の要素です。|

## <a name="remarks"></a>解説
 `Project` は、`TemplateContent` の子要素で、省略可能な要素です。

 `Project` 要素は、プロジェクトを指定するために使用されるため、プロジェクト テンプレート内でのみ有効です。

 `Project` 要素には [Folder](../extensibility/folder-element-visual-studio-project-templates.md) 子要素または [ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md) 子要素を含めることができますが、`Folder` と `ProjectItem` の両方の子要素を混在させることはできません。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、ユーザーが **[新しいプロジェクト]** ダイアログ ボックスで入力した名前に基づいて、プロジェクト ファイルの名前を自動的に変更します。 テンプレートで作成されたプロジェクト ファイルの代替ファイル名を指定する場合は、`TargetFileName` 属性を使用します。

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
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [ProjectItem 要素 (Visual Studio プロジェクト テンプレート)](../extensibility/projectitem-element-visual-studio-project-templates.md)
- [Folder 要素 (Visual Studio プロジェクト テンプレート)](../extensibility/folder-element-visual-studio-project-templates.md)
