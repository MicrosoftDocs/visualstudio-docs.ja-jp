---
title: TemplateContent 要素 (Visual Studio テンプレート) | Microsoft Docs
description: TemplateContent 要素と、それを使用してテンプレートの内容を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateContent
helpviewer_keywords:
- TemplateContent element [Visual Studio project templates]
ms.assetid: 90ae401c-b294-49ac-98da-e0d274f5bebb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 389f8e0ab6c6c7254b34721d20da40cc2d33df59
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056026"
---
# <a name="templatecontent-element-visual-studio-templates"></a>TemplateContent 要素 (Visual Studio テンプレート)

テンプレートの内容を指定します。

要素の階層:

```xml
<VSTemplate>
  <TemplateContent>
```

## <a name="syntax"></a>構文

```xml
<TemplateContent>
    ...
</TemplateContent>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|[BuildOnLoad](../extensibility/buildonload-visual-studio-templates.md)|テンプレートからプロジェクトを作成するときにソリューションをビルドするかどうかを指定します。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> 複数プロジェクトのテンプレートの構成と内容を指定します。|
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> プロジェクトに追加するファイルまたはディレクトリを指定します。|
|[参照](../extensibility/references-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> 項目テンプレートに必要なアセンブリ参照を指定します。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|省略可能な要素です。<br /><br /> テンプレートに含まれるファイルを指定します。|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> プロジェクトまたは項目をテンプレートから作成するときに使用するカスタム パラメーターを指定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必須の要素です。<br /><br /> プロジェクト テンプレート、項目テンプレート、またはスタート キットのすべてのメタデータが含まれます。|

## <a name="remarks"></a>解説
 `TemplateContent` は必須の要素です。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。

```xml
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
            <ProjectItem>Form1.cs</ProjectItem>
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
