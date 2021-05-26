---
title: ProjectItem 要素 (Visual Studio プロジェクト テンプレート) | Microsoft Docs
description: プロジェクト テンプレートの ProjectItem 要素と、それを使用して、そのテンプレートがプロジェクトまたは項目のどちらのものであるかに応じて異なる属性を受け付ける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- ProjectItem element [Visual Studio project templates]
- <ProjectItem> element [Visual Studio project templates]
ms.assetid: 82879fbe-7756-42cd-9a07-c10edf5b4673
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bb7513a37f73bfd4dfc1cb8060c772d375a57329
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068740"
---
# <a name="projectitem-element-visual-studio-project-templates"></a>ProjectItem 要素 (Visual Studio プロジェクト テンプレート)
プロジェクト テンプレートに含まれているファイルを指定します。

> [!NOTE]
> `ProjectItem` 要素は、そのテンプレートがプロジェクトまたは項目のどちらのものであるかに応じて異なる属性を受け付けます。 このトピックでは、プロジェクト テンプレートの `ProjectItem` 要素について説明します。 項目テンプレートの `ProjectItem` 要素の説明については、「[ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)」を参照してください。

 \<VSTemplate> \<TemplateContent>
 \<Project>
 \<ProjectItem>

## <a name="syntax"></a>構文

```
<ProjectItem
    TargetFileName="TargetFileName.ext"
    ReplaceParameters="true/false"
    OpenInEditor="true/false"
    OpenInWebBrowser="true/false"
    OpenInHelpBrowser="true/false"
    OpenOrder="Value">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|---------------------| - |
| `TargetFileName` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトが作成されるときのプロジェクト項目の名前とパスを指定します。 この属性は、テンプレート *.zip* ファイル内のディレクトリ構造とは異なるディレクトリ構造を作成したり、パラメーター置換を使用して項目名を作成したりするために役立ちます。 |
| `ReplaceParameters` | 省略可能な属性です。<br /><br /> この項目に、テンプレートからプロジェクトが作成されるときに置き換える必要があるパラメーター値が含まれているかどうかを指定するブール値。 既定値は `false` です。 |
| `OpenInEditor` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトが作成されるときに、この項目を [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のそれに対応するエディターで開く必要があるかどうかを指定するブール値。<br /><br /> `true` の `OpenInEditor` 値を持つ項目では、`OpenInWebBrowser` と `OpenInHelpBrowser` の属性は無視されます。<br /><br /> 既定値は `false` です。 |
| `OpenInWebBrowser` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトが作成されるときに、この項目を Web ブラウザーで開く必要があるかどうかを指定するブール値。<br /><br /> Web ブラウザーで開くことができるのは、プロジェクトに対してローカルな HTML ファイルとテキスト ファイルだけです。 この属性で外部 URL を開くことはできません。<br /><br /> 既定値は `false` です。 |
| `OpenInHelpBrowser` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトが作成されるときに、この項目をヘルプ ビューアーで開く必要があるかどうかを指定するブール値。<br /><br /> ヘルプ ブラウザーで開くことができるのは、プロジェクトに対してローカルな HTML ファイルとテキスト ファイルだけです。 この属性で外部 URL を開くことはできません。<br /><br /> 既定値は `false` です。 |
| `OpenOrder` | 省略可能な属性です。<br /><br /> 項目がそれに対応するエディターで開かれる順序を表す数値を指定します。 すべての値が 10 の倍数である必要があります。 より大きな `OpenOrder` 値を持つ項目が最初に開かれます。 |

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|プロジェクトに追加するファイルまたはディレクトリを指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テンプレート *.zip* ファイル内のファイルの名前またはパスを表す `string`。

## <a name="remarks"></a>解説
 `ProjectItem` は、`Project` の省略可能な子です。

 `TargetFileName` 属性を使用すると、テンプレート *.zip* ファイル内のディレクトリ構造とは異なるディレクトリ構造を作成できます。 たとえば、ファイル *MyFile.vb* はテンプレート *.zip* ファイルのルートに存在するが、そのファイルを、テンプレートから作成されたすべてのプロジェクトで *CustomFiles* という名前のディレクトリに配置したい場合は、次の XML を使用します。

```xml
<ProjectItem TargetFileName="CustomFiles\MyFile.vb">MyFile.vb</ProjectItem>
```

 また、`TargetFileName` 属性を使用して、ファイル名に国際文字が含まれているファイルの名前を変更することもできます。 たとえば、テンプレート *.zip* ファイルに Unicode 文字のファイル名を含めることはできないため、 *.zip* ファイルに圧縮するにはファイルの名前を変更しておく必要があります。 `TargetFileName` 属性を使用すると、ファイル名を元の Unicode のファイル名に戻すことができます。

 また、`TargetFileName` 属性を使用して、パラメーターでファイルの名前を変更することもできます。 次の手順では、テンプレート *.zip* ファイルのルート ディレクトリに存在するファイル *MyFile.vb* の名前を、プロジェクト名に基づいたファイル名に変更する方法について説明します。

### <a name="to-rename-files-with-parameters"></a>パラメーターでファイルの名前を変更するには

1. *.vstemplate* ファイルで次の XML を使用します。

   ```xml
   <ProjectItem TargetFileName="$safeprojectname$.vb">MyFile.vb</ProjectItem>
   ```

2. テキスト エディターまたは [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でプロジェクト ファイル ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] プロジェクトの場合は *.vbproj*) を開きます。

3. 次の XML のようなプロジェクト ファイル内の行を見つけます。

   ```xml
   <Compile Include="MyFile.vb">
   ```

4. このコード行を次の XML に置き換えます。

   ```xml
   <Compile Include="$safeprojectname$.vb">
   ```

    このテンプレートからプロジェクトが作成されたとき、そのファイル名は、 **[新しいプロジェクト]** ダイアログ ボックスでユーザーが入力した名前 (安全でない文字とスペースはすべて削除されます) に基づきます。 詳細については、「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
            <ProjectItem ReplaceParameters="true">Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)
