---
title: DefaultName 要素 (Visual Studio テンプレート) | Microsoft Docs
description: DefaultName 要素について、およびプロジェクトまたは項目の作成時にこれらに対して Visual Studio プロジェクト システムで生成される名前を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#DefaultName
helpviewer_keywords:
- DefaultName element [Visual Studio project templates]
ms.assetid: 0ff056c8-b9d2-4747-9308-92adf1811491
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c8b11655424086b65a1b4e2089e245f1e389b611
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091384"
---
# <a name="defaultname-element-visual-studio-templates"></a>DefaultName 要素 (Visual Studio テンプレート)
プロジェクトまたは項目の作成時にこれらに対して Visual Studio プロジェクト システムで生成される名前を指定します。

 \<VSTemplate> \<TemplateData>
 \<DefaultName>

## <a name="syntax"></a>構文

```
<DefaultName>
    Default Project Name
</DefaultName>
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

 このテキストによって、プロジェクトまたは項目の既定の名前が指定されます。

## <a name="remarks"></a>解説
 `DefaultName` は省略可能な要素です。

 プロジェクトの場合、この要素によって、ディスク上でプロジェクトを格納するディレクトリの名前が指定されます。 項目の場合、ソース ファイルのファイル名が指定されます。

 プロジェクトまたは項目を作成するときに、 **[名前]** オプションを使用して既定の名前を変更できます。このオプションは、 **[新しいプロジェクト]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスのどちらかから利用できます。

 プロジェクト システムでプロジェクトまたは項目既定の名前を生成させない場合は、[ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) 要素を `False` に設定します。

## <a name="example"></a>例
 次の例では、[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] クラスの標準的な項目テンプレートのメタデータを示します。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <DefaultName>MyClass.cs</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
