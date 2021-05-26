---
title: SortOrder 要素 (Visual Studio テンプレート) | Microsoft Docs
description: SortOrder 要素と、[新しいプロジェクト] ダイアログ ボックスまたは [新しい項目の追加] ダイアログ ボックスに表示されるテンプレートの配置に使用される値を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SortOrder
helpviewer_keywords:
- SortOrder element [Visual Studio Templates]
- <SortOrder> element [Visual Studio Templates]
ms.assetid: 151932c1-f08a-4f78-a8d0-bd2f32211a9c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a195e3801ce505d2c1f069c07ff4457e1c1042b3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073795"
---
# <a name="sortorder-element-visual-studio-templates"></a>SortOrder 要素 (Visual Studio テンプレート)
**[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスに表示されるテンプレートを、同じカテゴリの他のテンプレートの中に配置するために使用される値を指定します。

 \<VSTemplate> \<TemplateData>
 \<SortOrder>

## <a name="syntax"></a>構文

```
<SortOrder> ... </SortOrder>
```

## <a name="attributes-and-elements"></a>属性および要素
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

 並べ替え順序の値を表す `integer`。

## <a name="remarks"></a>解説
 `SortOrder` は省略可能な要素です。 既定値は 100 で、すべての値は 10 の倍数である必要があります。

 ユーザーが作成したテンプレートでは `SortOrder` 要素は無視されます。 ユーザーが作成したテンプレートはすべて、アルファベット順に並べ替えられます。

 並べ替え順序の値が低いテンプレートは、 **[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスで、並べ替え順序の値が高いテンプレートよりも前に表示されます。

## <a name="example"></a>例
 標準の [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] クラス テンプレートのメタデータの例を次に示します。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <SortOrder>290</SortOrder>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

 この例では、`SortOrder` 要素は比較的高くなっています。 他の [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 項目テンプレートの `SortOrder` 値は `290` よりも低く、 **[新しい項目]** ダイアログ ボックスでこのテンプレートよりも前に表示される可能性があります。

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
