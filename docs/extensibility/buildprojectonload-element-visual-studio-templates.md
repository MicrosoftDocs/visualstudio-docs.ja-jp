---
title: BuildProjectOnload 要素 (Visual Studio テンプレート) | Microsoft Docs
description: BuildProjectOnload 要素について、また、それによって、プロジェクトを作成してソリューションに追加するときに、新しいプロジェクトのみがビルドされるしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: b07d3074-0fc9-45e1-baf5-da6bd4f3f1c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f9d50d33824be70a7df09cee878d516ddaaf9f8d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068168"
---
# <a name="buildprojectonload-element-visual-studio-templates"></a>BuildProjectOnload 要素 (Visual Studio テンプレート)
プロジェクトを作成してソリューションに追加するときに新しいプロジェクトのみをビルドします。 ソリューション全体がビルドされるのではありません。

要素の階層:

```xml
<VSTemplate>
  <TemplateData>
    <BuildProjectOnLoad>
```

## <a name="syntax"></a>構文

```vb
<BuildProjectOnLoad> true/false </BuildProjectOnLoad>
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
|`TemplateData`|テンプレートを分類し、 **[新しいプロジェクト]** および **[新しい項目の追加]** の両方のダイアログ ボックスにどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テキストは `true` または `false` のいずれかで、テンプレートから作成されるときに新しいプロジェクトのみをビルドするかどうかを示します。

## <a name="remarks"></a>解説
 `BuildProjectOnLoad` は省略可能な要素です。 既定値は `false` です。

## <a name="example"></a>例
 次の例は、Visual C# テンプレートのメタデータの例を示しています。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <BuildProjectOnload>true</BuildProjectOnLoad>
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

- [BuildOnLoad 属性および要素](buildonload-visual-studio-templates.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
