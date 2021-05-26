---
title: '新しいプロジェクトの生成: 内部的な処理、パート 2 | Microsoft Docs'
description: 独自のプロジェクトの種類を作成したとき、Visual Studio 統合開発環境 (IDE) 内で何が起こるかを詳しく見てみましょう (パート 2/2)。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e391ad66c9925dc68997ff610dc5d1556ddf09b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063085"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>新しいプロジェクトの生成: 内部的な処理、パート 2

「[新しいプロジェクトの生成: 内部的な処理、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)」では、 **[新しいプロジェクト]** ダイアログボックスの設定方法について考慮しました。 **Visual C# Windows アプリケーション** を選択し、 **[名前]** および **[場所]** テキストボックスに入力して、[OK] をクリックしたという前提で話を進めます。

## <a name="generating-the-solution-files"></a>ソリューション ファイルの生成
 アプリケーション テンプレートを選択すると、対応する .vstemplate ファイルを解凍して開き、このファイル内の XML コマンドを解釈するためのテンプレートを起動するように [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に指示が出されます。 これらのコマンドによって、新規または既存のソリューションにプロジェクトとプロジェクト項目が作成されます。

 このテンプレートは、.vstemplate ファイルを保持する同じ .zip フォルダーから、項目テンプレートと呼ばれるソース ファイルをアンパックします。 テンプレートは、これらのファイルを新しいプロジェクトにコピーし、適宜カスタマイズします。

### <a name="template-parameter-replacement"></a>テンプレート パラメーターの置換
 テンプレートによって項目テンプレートが新しいプロジェクトにコピーされると、テンプレート パラメーターが、ファイルをカスタマイズする文字列に置き換えられます。 テンプレート パラメーターは、ドル記号が前後に挿入された (例: $date $) 特殊なトークンです。

 一般的なプロジェクト項目テンプレートを見てみましょう。 Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip フォルダーにある Program.cs を抽出して調べてみます。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace $safeprojectname$
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

Simple という名前の新しい Windows アプリケーション プロジェクトを作成した場合、テンプレートは `$safeprojectname$` パラメーターをプロジェクトの名前に置き換えます。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace Simple
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

 テンプレート パラメーターの完全な一覧については、「[テンプレート パラメーター](../../ide/template-parameters.md)」をご覧ください。

## <a name="a-look-inside-a-vstemplate-file"></a>.Vstemplate ファイルの内容
 ベーシックな .vstemplate ファイルの形式は次のようになります。

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 「[新しいプロジェクトの生成: 内部的な処理、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)」では \<TemplateData> セクションに注目しました。 このセクションのタグは、 **[新しいプロジェクト]** ダイアログ ボックスの外観を制御するために使用されます。

 \<TemplateContent> セクションのタグは、新しいプロジェクトとプロジェクト項目の生成を制御します。 次に示すのは、\Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip フォルダーにある cswindowsapplication.vstemplate ファイルの \<TemplateContent> セクションです。

```xml
<TemplateContent>
  <Project File="WindowsApplication.csproj" ReplaceParameters="true">
    <ProjectItem ReplaceParameters="true"
      TargetFileName="Properties\AssemblyInfo.cs">
      AssemblyInfo.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Resources.resx">
      Resources.resx
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Resources.Designer.cs">
      Resources.Designer.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Settings.settings">
      Settings.settings
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Settings.Designer.cs">
      Settings.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true" OpenInEditor="true">
      Form1.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Form1.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Program.cs
    </ProjectItem>
  </Project>
</TemplateContent>
```

 \<Project> タグはプロジェクトの生成を制御し、\<ProjectItem> タグはプロジェクト項目の生成を制御します。 パラメーター ReplaceParameters が true の場合、テンプレートはプロジェクト ファイルまたは項目内のすべてのテンプレート パラメーターをカスタマイズします。 この場合、Settings.settings 以外のすべてのプロジェクト項目がカスタマイズされます。

 TargetFileName パラメーターは、結果として得られるプロジェクト ファイルまたは項目の名前と相対パスを指定します。 これにより、プロジェクトのフォルダー構造を作成できます。 この引数を指定しない場合、プロジェクト項目の名前はプロジェクト項目テンプレートと同じになります。

 生成される Windows アプリケーションのフォルダー構造は次のようになります。

 ![Visual Studio ソリューション エクスプローラーの "Simple" ソリューションの Windows アプリケーション フォルダー構造のスクリーンショット。](../../extensibility/internals/media/simplesolution.png)

 テンプレートの最初と \<Project> タグのみが読み取られます。

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 これにより、新しいプロジェクト テンプレートは、テンプレート項目 windowsapplication.csproj をコピーおよびカスタマイズすることによって、単純な Simple.csproj プロジェクト ファイルを作成するように指示します。

### <a name="designers-and-references"></a>デザイナーと参照
 ソリューション エクスプローラーに、Properties フォルダーが存在し、期待されるファイルが含まれていることを確認できます。 しかし、プロジェクト参照とデザイナー ファイルの依存関係 (たとえば、Resources.Designer.cs から Resources.resx や Form1.Designer.cs から Form1.cs) についてはどうでしょうか。  これらは、Simple.csproj ファイルの生成時に設定されます。

 プロジェクト参照を作成する Simple.csproj の\<ItemGroup> を次に示します。

```xml
<ItemGroup>
    <Reference Include="System" />
    <Reference Include="System.Data" />
    <Reference Include="System.Deployment" />
    <Reference Include="System.Drawing" />
    <Reference Include="System.Windows.Forms" />
    <Reference Include="System.Xml" />
</ItemGroup>
```

 ソリューション エクスプローラーに表示される 6 つのプロジェクト参照があることがわかります。 以下に、別の \<ItemGroup> のセクションを示します。 わかりやすくするために、多くのコードの行が削除されています。 このセクションでは、Settings.settings に依存する Settings.Designer.cs を作成します。

```xml
<ItemGroup>
    <Compile Include="Properties\Settings.Designer.cs">
        <DependentUpon>Settings.settings</DependentUpon>
    </Compile>
</ItemGroup>
```

## <a name="see-also"></a>関連項目

- [新しいプロジェクトの生成: 内部的な処理、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)
- [MSBuild](../../msbuild/msbuild.md)
