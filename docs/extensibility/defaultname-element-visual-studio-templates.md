---
title: DefaultName 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#DefaultName
helpviewer_keywords:
- DefaultName element [Visual Studio project templates]
ms.assetid: 0ff056c8-b9d2-4747-9308-92adf1811491
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1dbb720bf04c36b2d9f018be5418a25088e259f4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348150"
---
# <a name="defaultname-element-visual-studio-templates"></a>DefaultName 要素 (Visual Studio テンプレート)
作成時にそのプロジェクトまたは項目の Visual Studio プロジェクト システムにより生成される名前を指定します。

 \<VSTemplate> \<TemplateData> \<DefaultName>

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

 このテキストは、プロジェクトまたは項目の既定の名前を指定します。

## <a name="remarks"></a>Remarks
 `DefaultName` は、省略可能な要素です。

 プロジェクトの場合は、この要素は、ディスク上、プロジェクトを格納するディレクトリの名前を指定します。 項目については、ソース ファイルのファイル名を指定します。

 使用して、既定の名前を変更するにはプロジェクトまたは項目を作成するときに、**名前**はいずれかから使用可能なオプション、**新しいプロジェクト** ダイアログ ボックスまたは**新しい項目の追加**ダイアログ ボックス。

 プロジェクトまたは項目の既定の名前を生成するプロジェクト システムしたくない場合は、設定、 [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md)要素`False`します。

## <a name="example"></a>例
 次の例では、用の標準的な項目テンプレートのメタデータを[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]クラス。

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