---
title: Folder 要素 (Visual Studio プロジェクト テンプレート) |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c066bfacea4996ab8d212ac607a3dfa3f3fad36
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342611"
---
# <a name="folder-element-visual-studio-project-templates"></a>Folder 要素 (Visual Studio プロジェクト テンプレート)
プロジェクトに追加されるフォルダーを指定します。

 \<VSTemplate> \<TemplateContent> \<Project> \<Folder>

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
|`TargetFolderName`|省略可能な属性です。<br /><br /> テンプレートからプロジェクトが作成されるフォルダーを指定する名前を指定します。 この属性は、パラメーター置換を使用して、フォルダー名を作成する場合に便利ですか、国際対応の文字列を持つフォルダーを名前付けしで直接使用できません、 *.zip*ファイル。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|`Folder`|プロジェクトに追加するフォルダーを指定します。 `Folder` 要素が子を含めることができます`Folder`要素。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|プロジェクトに追加するファイルを指定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|省略可能な子要素の[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)します。|

## <a name="remarks"></a>Remarks
 `Folder` 省略可能な子の`Project`します。

 テンプレート内のフォルダーにプロジェクト項目を整理するのにには、次の方法のいずれかを使用できます。

- テンプレート フォルダーに含める *.zip*ファイルを開き、プロジェクトに追加、 *.vstemplate*ファイル内のファイルへのパスを指定することによって、`ProjectItem`なしで、要素`Folder`要素。 これは、推奨される方法です。 例:

     `...`

     `<ProjectItem>\Folder\item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- テンプレート フォルダーに含める *.zip*ファイルを開き、プロジェクトに追加、 *.vstemplate*ファイルと`Folder`要素。 例:

     `...`

     `<Folder name="Folder">`

     `<ProjectItem>item.cs</ProjectItem>`

     `</Folder>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- テンプレートのフォルダーを含めないでください *.zip*ファイルしますが、使用してフォルダーを追加、`TargetFileName`の属性、`ProjectItem`要素。 例:

     `...`

     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

## <a name="example"></a>例
 次の例のためのプロジェクト テンプレート メタデータを[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]Windows アプリケーション。

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