---
title: LocationField 要素 (Visual Studio プロジェクト テンプレート)
titleSuffix: ''
description: LocationField 要素について、および [新しいプロジェクト] ダイアログ ボックスの [場所] テキスト ボックスがプロジェクト テンプレートに対して有効、無効、または非表示である場合の要素の指定方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#LocationField
helpviewer_keywords:
- LocationField element [Visual Studio project templates]
ms.assetid: 6aaaa155-6ce0-4f7f-aa50-8d63d7a7c992
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f1ad5263f11cd7e940b641959de1dea393eb98ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073236"
---
# <a name="locationfield-element-visual-studio-project-templates"></a>LocationField 要素 (Visual Studio プロジェクト テンプレート)
**[新しいプロジェクト]** ダイアログ ボックスの **[場所]** テキスト ボックスが、プロジェクト テンプレートに対して有効、無効、または非表示のいずれであるかを指定します。

 \<VSTemplate> \<TemplateData>
 \<LocationField>

## <a name="syntax"></a>構文

```
<LocationField> Enabled/Disabled/Hidden </LocationField>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** でどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 有効なテキスト値は次のとおりです。

- `Enabled`。 **[新しいプロジェクト]** ダイアログ ボックスの **[場所]** ボックスが有効になっていることを指定します。

- `Disabled`。 **[新しいプロジェクト]** ダイアログ ボックスの **[場所]** ボックスが無効になっていることを指定します。

- `Hidden`。 **[新しいプロジェクト]** ダイアログ ボックスの **[場所]** ボックスが非表示になっていることを指定します。

## <a name="remarks"></a>解説
 既定値は `Enabled` です。

 **[新しいプロジェクト]** ダイアログ ボックスの **[場所]** テキスト ボックスを使用すると、ユーザーは新しいプロジェクトを保存する既定のディレクトリを変更できます。

 `Location` 要素に指定されている値は、基になるプロジェクト システムによってサポートされている場合のみダイアログ ボックスで受け入れられます。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] テンプレートのメタデータの例を次に示します。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <LocationField>Disabled</LocationField>
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
