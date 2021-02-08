---
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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 211393ea65f7ca31f80134c48863b0092478b3f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99836983"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>RequiredFrameworkVersion 要素 (Visual Studio テンプレート)

テンプレートに必要な .NET Framework の最小バージョンを指定します。 これにより、[**新しいプロジェクト**] ダイアログに [**ターゲットフレームワークのバージョン**] ドロップダウンが表示されます。 また、要素は、 `RequiredFrameworkVersion` ドロップダウンリストで使用できる最小値を決定します。

> [!IMPORTANT]
> Visual Studio 2017 バージョン15.6 以降では、[**新しいプロジェクト**] ダイアログの [**テンプレート**] セクションに表示されるテンプレートの [**ターゲットフレームワークのバージョン**] ボックスの一覧が表示されなくなりました。 代わりに、ドロップダウンリストは、選択したテンプレートのフレームワークの選択として機能します。

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、 **新しいプロジェクト** または [ **新しい項目の追加** ] ダイアログボックスでの表示方法を定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、テンプレートに必要な .NET Framework の最小バージョン番号である必要があります。

## <a name="remarks"></a>解説

`RequiredFrameworkVersion` は省略可能な要素です。 この要素は、テンプレートが .NET Framework の特定の最小バージョン (およびそれ以降のバージョン) をサポートしている場合にのみ使用します。 要素を指定し、 `RequiredFrameworkVersion` テンプレートが特定の最小バージョンの .NET Framework をサポートしていない場合、[ **ターゲットフレームワークのバージョン** ] ドロップダウンは適用できないときに表示されます。

## <a name="example"></a>例

次の例は、標準クラステンプレートのメタデータを示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

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

この例では、テンプレートで必要とされる .NET Framework の最小バージョン `RequiredFrameworkVersion` は3.0 です。 このテンプレートを使用して作成されたプロジェクトは、3.0 以降のバージョンを対象に .NET Framework ことができます。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [フレームワーク対象設定機能の概要](../ide/visual-studio-multi-targeting-overview.md)
