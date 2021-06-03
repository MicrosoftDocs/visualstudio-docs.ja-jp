---
title: TemplateData 要素 (Visual Studio テンプレート) | Microsoft Docs
description: TemplateData 要素について、およびテンプレートをカテゴリに分類し、[新しいプロジェクト] または [新しい項目の追加] ダイアログ ボックスでそれがどのように表示されるかを定義する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateData
helpviewer_keywords:
- TemplateData element [Visual Studio project templates]
ms.assetid: db17ec9b-bfdf-46b1-bbe7-5ccc140056e2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b5bc7f9b94553bda2bd2fcf020264ddb0d850c32
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085573"
---
# <a name="templatedata-element-visual-studio-templates"></a>TemplateData 要素 (Visual Studio テンプレート)
テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。

 \<VSTemplate> \<TemplateData>

## <a name="syntax"></a>構文

```
<TemplateData>
    <Name> ... </Name>
    <Description> ... </Description>
    <Icon> ... </Icon>
    <ProjectType> ... </ProjectType>
    ...
</TemplateData>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

| 要素 | 説明 |
| - | - |
| [名前](../extensibility/name-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> **[新しいプロジェクト]** または **[新しい項目の追加]** ダイアログ ボックスに表示されるテンプレートの名前を指定します。 |
| [説明](../extensibility/description-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> **[新しいプロジェクト]** または **[新しい項目の追加]** ダイアログ ボックスに表示されるテンプレートの説明を指定します。 |
| [アイコン](../extensibility/icon-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> アイコンとして機能する画像ファイルのパスとファイル名を指定します。これは、 **[新しいプロジェクト]** または **[新しい項目の追加]** ダイアログ ボックスで、テンプレートに対して表示されます。 |
| [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> プロジェクト テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックスの指定されたグループに表示されるようにします。 |
| [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクト テンプレートを分類し、 **[新しいプロジェクト]** ダイアログ ボックスの指定されたサブカテゴリに表示されるようにします。 |
| [TemplateID](../extensibility/templateid-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートの ID を指定します。 |
| [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレート グループの ID を指定します。 |
| [SortOrder](../extensibility/sortorder-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> **[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスに表示されるテンプレートを同じカテゴリの他のテンプレートの中に配置するために使用される値を指定します。 |
| [CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトをインスタンス化するときに、格納フォルダーを作成するかどうかを指定します。 |
| [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトまたは項目の作成時にこれらに対して Visual Studio プロジェクト システムで生成される名前を指定します。 |
| [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトまたは項目の作成時にこれらに対して Visual Studio プロジェクト システムで既定の名前を生成するかどうかを指定します。 |
| [PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトを一時プロジェクトとして作成できるかどうかを指定します (Visual Studio 2017 のみ)。 |
| [EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> **[新しいプロジェクト]** ダイアログ ボックスで **[参照]** ボタンを使用できるかどうかを指定します。これにより、新しいプロジェクトを保存する既定のディレクトリをユーザーが簡単に変更できるようになります。 |
| [[非表示]](../extensibility/hidden-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> **[新しいプロジェクト]** と **[新しい項目の追加]** のどちらのダイアログ ボックスにテンプレートを表示するかを指定します。 |
| [NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> **[新しいプロジェクト]** ダイアログ ボックスにテンプレートが表示される親カテゴリの数を指定します。 |
| [LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md) | 省略可能な要素です。 |
| [LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md) | 省略可能な要素です。<br /><br /> **[新しいプロジェクト]** ダイアログ ボックスの **[場所]** テキスト ボックスが、プロジェクト テンプレートに対して有効、無効、または非表示のいずれであるかを指定します。 |
| [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> この要素は、テンプレートで .NET Framework の特定の最小バージョン (および、存在する場合はそれ以降のバージョン) のみがサポートされる場合に使用します。 |
| [SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートで Web プロジェクトのマスター ページがサポートされるかどうかを指定します。 |
| [SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートで Web プロジェクトのコード分離 (分離コード ページ モデル) がサポートされるかどうかを指定します。 |
| [SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが複数の言語で同一であるかどうか、および **[新しいプロジェクト]** ダイアログ ボックスから **[言語]** オプションを使用できるかどうかを指定します。 |
| [TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクト テンプレートの対象となるプラットフォームを指定します。 この要素では、[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリを作成するためにプロジェクト テンプレートを使用することを指定します。 |

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必須の要素です。<br /><br /> プロジェクト テンプレート、項目テンプレート、またはスタート キットのすべてのメタデータが含まれています。|

## <a name="remarks"></a>解説
 `TemplateData` は必須の要素です。

 オプションの要素を含めない場合は、その要素の既定値が使用されます。

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
