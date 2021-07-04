---
title: プロジェクト テンプレート上でタグを追加または編集する
description: Visual Studio のプロジェクト テンプレート上でタグを追加または更新する方法について説明します。
ms.date: 04/30/2019
author: minsa110
ms.author: somin
manager: jmartens
ms.topic: reference
helpviewer_keywords:
- item templates, updating
- Visual Studio templates, updating
- project templates, updating
- updating templates [Visual Studio]
- template tagging, updating
- template tags, updating
ms.openlocfilehash: ac4757464d720ca50632833b3911f0d594e1becb
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222982"
---
# <a name="add-tags-to-project-templates"></a>プロジェクト テンプレートにタグを追加する

[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) バージョン 16.1 Preview 2 以降では、言語、プラットフォーム、プロジェクト タイプのタグを自分のプロジェクト テンプレートに追加できます。 

タグは、 **[新しいプロジェクト]** ダイアログ ボックスの 2 つの場所で使用されます。

- テンプレートの説明の下にタグが表示されます。

   ![[新しいプロジェクト] ダイアログでのタグを含むプロジェクト テンプレート](media/npd-item-with-template-tags.png)

- タグを使って、テンプレートを検索およびフィルター処理できます。

   ![[新しいプロジェクト] ダイアログ ボックスでの検索とフィルター処理](media/npd-search-and-filter.png)

タグを追加するには、 *.vstemplate* XML ファイルを更新します。 Visual Studio に組み込まれているテンプレート タグを使用するか、カスタム テンプレート タグを作成することができます。 テンプレート タグは、Visual Studio 2019 の **[新しいプロジェクト]** ダイアログ ボックスでのみ表示されます。 以前のバージョンの Visual Studio では、テンプレート タグがテンプレートの表示方法に影響することはありません。

## <a name="add-or-edit-tags"></a>タグを追加または編集する

次のいずれかの操作を行うときに、プロジェクト テンプレートの *.vstemplate* XML でタグを追加または編集できます。

* [テンプレートのエクスポート] ウィザードを使って[新しいプロジェクト テンプレートを作成する](how-to-create-project-templates.md)。
* [既存のプロジェクト テンプレートを更新する](how-to-update-existing-templates.md)。
* [新しい VSIX プロジェクト テンプレートを作成する](../extensibility/getting-started-with-the-vsix-project-template.md)。

## <a name="syntax"></a>構文

```xml
<LanguageTag> Language Name </LanguageTag>
<PlatformTag> Platform Name </PlatformTag>
<ProjectTypeTag> Project Type </ProjectTypeTag>
```

## <a name="attributes"></a>属性

高度なユーザー シナリオでは、次の省略可能な属性を使用できます。

|属性|説明|
|---------------|-----------------|
|`Package`|Visual Studio のパッケージ ID を指定する GUID です。|
|`ID`|Visual Studio のリソース ID を指定します。|

構文:

```xml
<LanguageTag Package="{PackageID}" ID="ResourceID" />
<PlatformTag Package="{PackageID}" ID="ResourceID" />
<ProjectTypeTag Package="{PackageID}" ID="ResourceID" />
```

## <a name="elements"></a>Elements

### <a name="child-elements"></a>子要素

なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|(必須) テンプレートをカテゴリに分類し、その **[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスでの表示方法を定義します。|

## <a name="text-value"></a>テキスト値

`Package` と `ID` 属性を使わない限り、テキスト値が必要です。

テキストによってテンプレートの名前を指定します。

## <a name="built-in-tags"></a>組み込みのタグ

Visual Studio には、組み込みのタグのリストが用意されています。 組み込みのタグを追加すると、そのタグによりローカライズされたリソースが表示されます。 

Visual Studio で利用できる組み込みのタグの一覧を次に示します。 対応する値をかっこ内に表示します。

| 言語タグ | プラットフォーム タグ | プロジェクト タイプ タグ |
| -- | -- | -- |
| C++ (`cpp`) | Android (`android`) | クラウド (`cloud`) |
| C# (`csharp`) | Azure (`azure`) | コンソール (`console`) |
| F# (`fsharp`) | iOS (`ios`) | デスクトップ (`desktop`) |
| Java (`java`) | Linux (`linux`) | 拡張機能 (`extension`) |
| JavaScript (`javascript`) | macOS (`macos`) | ゲーム (`games`) |
| Python (`python`) | tvOS (`tvos`) | IoT (`iot`) |
| クエリ言語 (`querylanguage`) | Windows (`windows`) | ライブラリ (`library`) |
| TypeScript (`typescript`) | Xbox (`xbox`) | 機械学習 (`machinelearning`) |
| Visual Basic (`visualbasic`) | | モバイル (`mobile`) |
| | | Office (`office`) |
| | | その他 (`other`) |
| | | サービス (`service`) |
| | | テスト (`test`) |
| | | UWP (`uwp`) |
| | | Web (`web`) |

## <a name="example"></a>例

Visual C# アプリケーションのプロジェクト テンプレートのメタデータの例を次に示します。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>csharp</ProjectType>
        <LanguageTag>csharp</LanguageTag>
        <PlatformTag>windows</PlatformTag>
        <PlatformTag>linux</PlatformTag>
        <PlatformTag>My Platform</PlatformTag>
        <ProjectTypeTag>console</ProjectTypeTag>
        <ProjectTypeTag>desktop</ProjectTypeTag>
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
- [プロジェクト テンプレートと項目テンプレートを作成する](creating-project-and-item-templates.md)
- [プロジェクト テンプレートと項目テンプレートのカスタマイズ](customizing-project-and-item-templates.md)
- [VSIX プロジェクト テンプレートの概要](../extensibility/getting-started-with-the-vsix-project-template.md)
