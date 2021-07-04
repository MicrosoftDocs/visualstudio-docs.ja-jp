---
title: Visual Studio テンプレート マニフェスト スキーマ リファレンス | Microsoft Docs
description: このスキーマ リファレンスでは、Visual Studio のプロジェクトまたは項目テンプレートに対して生成される Visual Studio テンプレート マニフェスト ファイルの形式について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 259d2dd050f4681053f331bfd4ec39dd7b214059
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905385"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Visual Studio テンプレート マニフェスト スキーマ リファレンス
このスキーマでは、Visual Studio のプロジェクトまたは項目テンプレートに対して生成される Visual Studio テンプレート マニフェスト ( *.vstman*) ファイルの形式を記述します。 このスキーマでは、テンプレートに関する場所やその他の関連情報も記述します。

 : 項目およびプロジェクト テンプレートのディレクトリは異なるため、マニフェストに項目およびプロジェクト テンプレートを混在させないでください。

> [!IMPORTANT]
> このマニフェストは、Visual Studio 2017 以降で使用できます。

## <a name="vstemplatemanifest-element"></a>VSTemplateManifest 要素
 マニフェストのルート要素。

### <a name="attributes"></a>属性

- **Version**: テンプレート マニフェストのバージョンを表す文字列。 必須。

- **Locale**: テンプレート マニフェストのロケールを表す文字列。 このロケール値はすべてのテンプレートに適用されます。 ロケールごとに別個のマニフェストを使用する必要があります。 省略可能。

### <a name="child-elements"></a>子要素

- **VSTemplateContainer** 省略可能。

- **VSTemplateDir** 省略可能。

### <a name="parent-element"></a>親要素
 なし。

## <a name="vstemplatecontainer"></a>VSTemplateContainer
 テンプレート マニフェスト要素のコンテナー。 マニフェストには、定義するテンプレートごとに 1 つのテンプレート コンテナーが含まれています。

### <a name="attributes"></a>属性
 **VSTemplateType**: テンプレートの種類 (`"Project"`、`"Item"`、または `"ProjectGroup"`) を指定する文字列値。 必須

### <a name="child-elements"></a>子要素

- **RelativePathOnDisk**: ディスク上のテンプレート ファイルの相対パス。 この場所では、 **[新しいプロジェクト]** または **[新しい項目]** ダイアログに表示されるテンプレート ツリー内のテンプレートの配置も定義されます。 ディレクトリと個々のファイルとして配置されるテンプレートの場合、このパスはテンプレート ファイルを含むディレクトリを参照します。 *.zip* ファイルとして配置されるテンプレートの場合、このパスは *.zip* ファイルへのパスである必要があります。

- **VSTemplateHeader: ヘッダーを記述する [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) 要素。

### <a name="parent-element"></a>親要素
 **VSTemplateManifest**

## <a name="vstemplatedir"></a>VSTemplateDir
 テンプレートが配置されているディレクトリを記述します。 マニフェストに複数の **VSTemplateDir** エントリを含めると、ディレクトリのローカライズされた名前と並べ替え順序を提供し、テンプレート カテゴリ ツリーでの表示を制御することができます。

 このような設計のため、**VSTemplateDir** エントリはロケールが指定されていないマニフェストにのみ含めることができます。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

- **RelativePath**: テンプレートのパス。 パスごとに 1 つのエントリしか指定できないため、最初のものがすべてのマニフェストで使用されます。

- **LocalizedName**: ローカライズされた名前を指定する **NameDescriptionIcon** 要素。 省略可能。

- **SortOrder**: 並べ替え順序を指定する文字列。 省略可能。

- **ParentFolderOverrideName**: 親フォルダーのオーバーライドされた名前。 省略可能。 この要素には、名前を指定する文字列値である **Name** 属性が含まれています。

### <a name="parent-element"></a>親要素
 **VSTemplateManifest**

## <a name="namedescriptionicon"></a>NameDescriptionIcon
 ローカライズされたテンプレートなどの名前と説明を指定します。 上記の「**LocalizedName**」を参照してください。

### <a name="attributes"></a>属性

- **Package**: パッケージを指定する文字列値。 省略可能。

- **ID**: ID を指定する文字列値。 省略可能。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-element"></a>親要素
 **LocalizedName**

## <a name="examples"></a>例
 次のコードは、プロジェクト テンプレートの *.vstman* ファイルの例です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\TestProjectTemplate</RelativePathOnDisk>
    <TemplateFileName>TestProjectTemplate.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>TestProjectTemplate</Name>
        <Description>TestProjectTemplate</Description>
        <Icon>TestProjectTemplate.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>aac0aeea-7883-4003-992f-937d53d70ab1</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>TestProjectTemplate</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 次のコードは、項目テンプレートの *.vstman* ファイルの例です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```
