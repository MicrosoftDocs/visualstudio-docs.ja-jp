---
title: WizardData 要素 (Visual Studio テンプレート) | Microsoft Docs
description: WizardData 要素とカスタム XML の指定方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardData
helpviewer_keywords:
- WizardData element [Visual Studio Templates]
- <WizardData> element [Visual Studio Templates]
ms.assetid: d0403a16-5d07-4fe5-b474-19ae3d9fd3ab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bd7b85433b4e02491852589d32eea9a4f223da14
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061889"
---
# <a name="wizarddata-element-visual-studio-templates"></a>WizardData 要素 (Visual Studio テンプレート)

カスタム XML を指定します

```xml
\<VSTemplate>
\<WizardData>
```

## <a name="syntax"></a>構文

```xml
<WizardData>
    <!-- XML to pass to the custom wizard extension -->
    ...
</WizardData>
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
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必須の要素です。<br /><br /> プロジェクト テンプレート、項目テンプレート、またはスタート キットのすべてのメタデータが含まれます。|

## <a name="text-value"></a>テキスト値

テキスト値は省略可能です。

このテキストを使用すると、[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md) 要素で指定されたカスタム ウィザード拡張機能に渡すカスタム XML を指定できます。

## <a name="remarks"></a>解説

この要素には任意の XML を指定できます。 XML はパラメーターとしてカスタム ウィザード拡張に渡され、この拡張機能からこの要素の内容を使用できるようになります。 このデータに対する検証は行われません。

**WizardData** 要素の内容は、`IWizard.RunStarted` メソッドで、パラメーターの文字列ディクショナリ内のパラメーターとして、変更されずに渡されます。 ディクショナリ キーは `$wizarddata$` という名前です。

## <a name="example"></a>例

次の例は、C# Windows アプリケーションの標準プロジェクト テンプレートのメタデータを示しています。

```xml
<VSTemplate Version="3.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyTemplate</Name>
        <Description>Template using IWizard extension</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
    <WizardData>
        <!-- XML to pass to the custom wizard extension -->
    </WizardData>
</VSTemplate>
```

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [WizardExtension 要素 (Visual Studio テンプレート)](../extensibility/wizardextension-element-visual-studio-templates.md)
- [方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)
