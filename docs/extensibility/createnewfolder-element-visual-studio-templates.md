---
title: CreateNewFolder 要素 (Visual Studio テンプレート) | Microsoft Docs
description: CreateNewFolder 要素について、およびプロジェクトの作成先となるターゲット ディレクトリの有無をチェックするかどうかを決定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CreateNewFolder
helpviewer_keywords:
- CreateNewFolder element [Visual Studio project templates]
ms.assetid: acef2016-4140-45d6-ace8-b8160eabd676
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3c2d8da615c350fc53b81532972cef65f6cd6ed7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089473"
---
# <a name="createnewfolder-element-visual-studio-templates"></a>CreateNewFolder 要素 (Visual Studio テンプレート)
プロジェクトの作成先となるターゲット ディレクトリの有無をチェックするかどうかを指定します。 ディレクトリが存在する場合は、プロジェクト用の新規ディレクトリを作成できます。 通常は、この設定は `NewProjectRequiresNewFolder(VsTemplate)` レジストリ フラグ (`HKEY_LOCAL_MACHINE/SOFTWARE(/Wow6432Node)/Microsoft/VisualStudio/<version number>/Projects/<project GUID>`) をオーバーライドします。このフラグは、一般的なあらゆる種類のプロジェクトにおいて、新規ディレクトリに新規プロジェクトを作成するかどうかを指定するためのものです。

 \<VSTemplate> \<TemplateData>
 \<CreateNewFolder>

## <a name="syntax"></a>構文

```
<CreateNewFolder>
    true/false
</CreateNewFolder>
```

## <a name="type"></a>種類
 `Boolean`

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

 `true` または `false` のいずれかを設定する必要があります。これは、テンプレートからプロジェクトを作成するときに新規のコンテナー フォルダーを作成するかどうかを示します。

## <a name="remarks"></a>解説
 `CreateNewFolder` は省略可能な要素です。 既定値は `true` です。

 `CreateNewFolder` は、基になるプロジェクト システムによってサポートされている場合のみ、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 要素に指定されている値に従います。

## <a name="example"></a>例
 次のコード例では、テンプレートからプロジェクトを作成するときに新規フォルダーを作成しないように指定しています。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <CreateNewFolder>false</CreateNewFolder>
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
