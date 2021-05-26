---
description: テンプレートに必要な .NET Framework の最小バージョンを指定します。
title: RequiredFrameworkVersion 要素 (Visual Studio テンプレート)
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 661e4067ac0191444be8ec7f1136f805ea8b39b5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068454"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>RequiredFrameworkVersion 要素 (Visual Studio テンプレート)

テンプレートに必要な .NET Framework の最小バージョンを指定します。 これにより、 **[新しいプロジェクト]** ダイアログに **[ターゲット フレームワーク バージョン]** ドロップダウンが表示されます。 また、`RequiredFrameworkVersion` 要素によって、このドロップダウンで使用可能な最小値も決定されます。

> [!IMPORTANT]
> Visual Studio 2017 バージョン 15.6 から、 **[ターゲット フレームワーク バージョン]** ドロップダウンは、 **[新しいプロジェクト]** ダイアログの **[テンプレート]** セクションに表示されているテンプレートのためのフィルターではなくなりました。 代わりに、このドロップダウンは、選択されているテンプレートのフレームワーク ピッカーとして機能します。

 \<VSTemplate> \<TemplateData>
 \<RequiredFrameworkVersion>

## <a name="syntax"></a>構文

```xml
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、それが **[新しいプロジェクト]** または **[新しい項目の追加]** ダイアログ ボックスのどちらかにどのように表示されるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、テンプレートに必要な .NET Framework の最小バージョン番号である必要があります。

## <a name="remarks"></a>解説

`RequiredFrameworkVersion` は省略可能な要素です。 この要素は、テンプレートで .NET Framework の特定の最小バージョン (および、存在する場合はそれ以降のバージョン) をサポートしている場合にのみ使用します。 `RequiredFrameworkVersion` 要素を指定しても、テンプレートで .NET Framework の特定の最小バージョンをサポートしていない場合、 **[ターゲット フレームワーク バージョン]** ドロップダウンには、それがいつ適用不可であるかが表示されます。

## <a name="example"></a>例

標準の [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] クラス テンプレートのメタデータの例を次に示します。

```xml
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>3.0</RequiredFrameworkVersion>
        <MaxFrameworkVersion>4.7.1</MaxFrameworkVersion>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

この例では、テンプレートに必要な .NET Framework の最小バージョン (`RequiredFrameworkVersion` で表されます) は 3.0 です。 このテンプレートで作成されたプロジェクトは、3.0 以降の .NET Framework バージョンを対象とすることができます。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [フレームワーク対象設定機能の概要](../ide/visual-studio-multi-targeting-overview.md)
