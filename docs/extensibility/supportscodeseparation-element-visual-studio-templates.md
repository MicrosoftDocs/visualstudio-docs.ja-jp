---
title: SupportsCodeSeparation 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsCodeSeparation
helpviewer_keywords:
- SupportsCodeSeparation element [Visual Studio Templates]
- <SupportsCodeSeparation> element [Visual Studio Templates]
ms.assetid: 8112aac8-a269-40e5-b92b-9b9a6ff5a542
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a4a9e7ba92b9f48cf22999d53ecf6c7b7d832ab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66316948"
---
# <a name="supportscodeseparation-element-visual-studio-templates"></a>SupportsCodeSeparation 要素 (Visual Studio テンプレート)
指定するかどうか、**別のファイルにコードを配置**チェック ボックスをオンになって、**新しい項目の追加** ダイアログ ボックス。

 \<VSTemplate > \<TemplateData > \<SupportsCodeSeparation >

## <a name="syntax"></a>構文

```
<SupportsCodeSeparation> true/false </SupportsCodeSeparation>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、いずれかでどのように表示を定義、**新しいプロジェクト**または**新しい項目の** ダイアログ ボックス。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テキストがいずれかにする必要があります`true`または`false`ことを示すかどうか、**別のファイルにコードを配置**チェック ボックスをオンになって、**新しい項目の追加** ダイアログ ボックス。

## <a name="remarks"></a>Remarks
 `SupportsCodeSeparation` は、省略可能な要素です。 既定値は `false` です。

 `SupportsCodeSeparation`要素は、Web 項目テンプレートの使用のみ。

 コードの分離、または分離コード ページ モデルでは、1 つのファイルと、別のファイルのプログラミング コードにマークアップを格納することができます。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 他の .NET 言語は、このモデルを使用します。

## <a name="example"></a>例
 次の例を表示するように指定します、**別のファイルにコードを配置**オプション。

```
<VSTemplate Version="3.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple Web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
        <SupportsCodeSeparation>true</SupportsCodeSeparation>
    </TemplateData>
    <TemplateContent>
        <Project File="WebApplication.webproj">
            <ProjectItem>icon.ico</ProjectItem>
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>
            <ProjectItem>Default.aspx.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)