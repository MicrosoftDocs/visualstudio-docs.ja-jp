---
title: ProvideDefaultName 要素 (Visual Studio テンプレート) | Microsoft Docs
description: ProvideDefaultName 要素と、それを使用して、Visual Studio で [新しい項目の追加] または [新しいプロジェクト] ダイアログ ボックス内に既定の Visual Studio 名を生成するかどうかを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProvideDefaultName
helpviewer_keywords:
- ProvideDefaultName element [Visual Studio project templates]
ms.assetid: 7b0e7b20-fd6b-42e2-81d0-e5100cea0528
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d29ca3075ee6e5ef031bb360ecfd10d6cb341c26
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068636"
---
# <a name="providedefaultname-element-visual-studio-templates"></a>ProvideDefaultName 要素 (Visual Studio テンプレート)
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクト システムで **[新しい項目の追加]** または **[新しいプロジェクト]** ダイアログ ボックス内にテンプレートの既定の名前を生成するかどうかを指定します。

 \<VSTemplate> \<TemplateData>
 \<ProvideDefaultName>

## <a name="syntax"></a>構文

```xml
<ProvideDefaultName> true/false </ProvideDefaultName>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、 **[新しい項目の追加]** または **[新しいプロジェクト]** ダイアログ ボックス内にテンプレートの既定の名前を生成するかどうかを示す `true` または `false` のどちらかである必要があります。

## <a name="remarks"></a>解説
 `ProvideDefaultName` は省略可能な要素です。 既定値は `true` です。

 `ProvideDefaultName` 要素が `false` である場合、 **[新しい項目の追加]** および **[新しいプロジェクト]** ダイアログ ボックスの **[名前]** ボックスには値 `<Enter_name>` が含まれます。

 **[新しい項目の追加]** および **[新しいプロジェクト]** ダイアログ ボックス内のプロジェクトまたは項目の既定の名前を指定するには、[DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) 要素を使用します。 `ProvideDefaultName` 要素の値が `true` である場合は、プロジェクトの `DefaultName` 要素を省略すると、ダイアログ ボックスにはそのテンプレートの名前 (つまり、[Name](../extensibility/name-element-visual-studio-templates.md) 要素の値) が設定されます。

## <a name="example"></a>例
 次のコード例では、`ProvideDefaultName` 要素を `false` に設定します。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProvideDefaultName>false</ProvideDefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
