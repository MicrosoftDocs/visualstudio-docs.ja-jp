---
title: MaxFrameworkVersion 要素 (Visual Studio テンプレート) | Microsoft Docs
description: MaxFrameworkVersion 要素と、テンプレートで必要な .NET Framework の最大バージョンがどのように指定されるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 05d61e298c666d22df1af8d426cb0671feb8b9c5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090617"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>MaxFrameworkVersion 要素 (Visual Studio テンプレート)

テンプレートで必要な .NET Framework の最大バージョンを指定します。 **[新しいプロジェクト]** ダイアログの **[ターゲット フレームワーク バージョン]** ドロップダウンで使用できる最大値が決定されます。 ユーザーがフレームワーク バージョンを選択できるようにするには、[RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) にテンプレートの最小 .NET Framework バージョンを指定する必要もあります。

> [!IMPORTANT]
> Visual Studio 2017 バージョン 15.6 以降、 **[新しいプロジェクト]** ダイアログの **[テンプレート]** セクションでは、 **[ターゲット フレームワーク バージョン]** ドロップダウンは表示されるテンプレートのフィルターではなくなりました。 代わりに、 **[ターゲット フレームワーク バージョン]** ドロップダウンは、選択したテンプレートのフレームワーク ピッカーとして機能します。

 \<VSTemplate> \<TemplateData>
 \<MaxFrameworkVersion>

## <a name="syntax"></a>構文

```xml
<MaxFrameworkVersion> ... </MaxFrameworkVersion>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、それが **[新しいプロジェクト]** または **[新しい項目の追加]**  ダイアログ ボックスのどちらかにどのように表示されるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、テンプレートで許可されている .NET Framework の最大バージョン番号である必要があります。

## <a name="remarks"></a>解説

`MaxFrameworkVersion` は省略可能な要素です。 テンプレートに対してサポートされている .NET Framework バージョンの範囲を誤って制限しないように、必要な場合を除き、`MaxFrameworkVersion` 要素を省略する必要があります。 .NET Framework がテンプレートに適用されない場合も、省略する必要があります。

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

この例では、テンプレートで必要な .NET Framework の最大バージョン (`MaxFrameworkVersion` で表されます) は 4.7.1 です。 このテンプレートを使用して作成されたプロジェクトは、4.7.1 までの .NET Framework バージョンを対象にすることができます。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
