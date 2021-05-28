---
title: ProjectItem 要素 (Visual Studio 項目テンプレート) | Microsoft Docs
description: 項目テンプレートの ProjectItem 要素と、それを使用して、そのテンプレートがプロジェクトまたは項目のどちらのものであるかに応じて異なる属性を受け付ける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- <ProjectItem> element [Visual Studio item templates]
- ProjectItem element [Visual Studio item templates]
ms.assetid: 9ed94112-0c38-49df-b728-0dd2d0d1eb47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0910486202bca781ec19b6d5895e68ed93f8c3d5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068727"
---
# <a name="projectitem-element-visual-studio-item-templates"></a>ProjectItem 要素 (Visual Studio 項目テンプレート)
項目テンプレートに含まれているファイルを指定します。

> [!NOTE]
> `ProjectItem` 要素は、そのテンプレートがプロジェクトまたは項目のどちらのものであるかに応じて異なる属性を受け付けます。 このトピックでは、項目の `ProjectItem` 要素について説明します。 プロジェクト テンプレートの `ProjectItem` 要素の説明については、「[ProjectItem 要素 (Visual Studio プロジェクト テンプレート)](../extensibility/projectitem-element-visual-studio-project-templates.md)」を参照してください。

 \<VSTemplate> \<TemplateContent>
 \<ProjectItem>

## <a name="syntax"></a>構文

```
<ProjectItem
    SubType="Form/Component/CustomControl/UserControl"
    CustomTool="string"
    ItemType="string"
    ReplaceParameters="true/false"
    TargetFileName="TargetFileName.ext">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|---------------------| - |
| `SubType` | 省略可能な属性です。<br /><br /> 複数ファイルの項目テンプレート内の項目のサブタイプを指定します。 この値は、項目を開くために [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に使用されるエディターを決定するために使用されます。 |
| `CustomTool` | 省略可能な属性です。<br /><br /> プロジェクト ファイル内の項目の CustomTool を設定します。 |
| `ItemType` | 省略可能な属性です。<br /><br /> プロジェクト ファイル内の項目の ItemType を設定します。 |
| `ReplaceParameters` | 省略可能な属性です。<br /><br /> この項目に、テンプレートからプロジェクトが作成されるときに置き換える必要があるパラメーター値が含まれているかどうかを指定するブール値。 既定値は `false` です。 |
| `TargetFileName` | 省略可能な属性です。<br /><br /> テンプレートから作成された項目の名前を指定します。 この属性は、パラメーター置換を使用して項目名を作成する場合に役立ちます。 |

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テンプレート *.zip* ファイル内のファイルの名前を表す `string`。

## <a name="remarks"></a>解説
 `ProjectItem` は、`TemplateContent` の省略可能な子です。

 `TargetFileName` 属性を使用して、パラメーターでファイルの名前を変更することができます。 たとえば、ファイル *MyFile.vb* がテンプレート *.zip* ファイルのルート ディレクトリに存在していても、 **[新しい項目の追加]** ダイアログ ボックスでユーザーが入力したファイル名に基づいてファイル名を付けたい場合は、次のような XML を使用します。

```xml
<ProjectItem TargetFileName="$fileinputname$.vb">MyFile.vb</ProjectItem>
```

 このテンプレートから項目を作成すると、ユーザーが **[新しい項目を追加]** ダイアログ ボックスに入力した名前に基づいたファイル名になります。 これは、複数ファイルの項目テンプレートを作成するときに役立ちます。 詳細については、「[方法: 複数ファイルの項目テンプレートを作成する](../ide/how-to-create-multi-file-item-templates.md)」と「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

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
- [方法: 複数ファイルの項目テンプレートを作成する](../ide/how-to-create-multi-file-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
