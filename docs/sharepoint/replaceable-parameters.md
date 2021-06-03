---
title: 置き換え可能パラメーター | Microsoft Docs
description: これは、デザイン時に実際の値がわからない SharePoint ソリューション項目のプロジェクト ファイル内の値を指定する置き換え可能パラメーター (トークン) について確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, tokens
- tokens [SharePoint development in Visual Studio]
- replaceable parameters [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, replaceable parameters
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload: office
ms.openlocfilehash: 3eb6e737a1f939e05e6a6be7f2c9ba950fc411d6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889500"
---
# <a name="replaceable-parameters"></a>置き換え可能パラメーター
  置き換え可能パラメーター (*トークン*) プロジェクト ファイル内で使用すると、デザイン時に実際の値がわからない SharePoint ソリューション項目の値を指定できます。 これらは、標準の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] テンプレート トークンに似ています。 詳細については、「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

## <a name="token-format"></a>トークンの形式
 トークンの先頭と末尾にはドル記号 ($) が付きます。 使用されたすべてのトークンは、配置時にプロジェクトが SharePoint ソリューション パッケージ ( *.wsp* ファイル) にパッケージ化されるときに、実際の値に置き換えられます。 たとえば、トークン **$SharePoint.Package.Name$** が文字列 "Test SharePoint Package" に解決されます。

## <a name="token-rules"></a>トークンの規則
 トークンには次の規則が適用されます。

- トークンは、行内の任意の場所で指定できます。

- 複数の行にまたがるトークンは指定できません。

- 同じ行および同じファイルに同じトークンを複数回指定することもできます。

- 同じ行に複数の異なるトークンを指定することもできます。

  これらの規則に従わないトークンは無視され、警告やエラーは発生しません。

  文字列値によるトークンの置換は、マニフェスト変換の直後に行われます。 この置換により、ユーザーはトークンを使用してマニフェスト テンプレートを編集できます。

### <a name="token-name-resolution"></a>トークン名の解決
 ほとんどの場合、トークンは、含まれている場所に関係なく、特定の値に解決されます。 ただし、トークンがパッケージまたはフィーチャーに関連付けられている場合、トークンの値はそれが含まれている場所によって異なります。 たとえば、あるフィーチャーが Package A に含まれている場合、トークン `$SharePoint.Package.Name$` は値 "Package A" に解決されます。 同じフィーチャーが Package B に含まれている場合、`$SharePoint.Package.Name$` は "Package B" に解決されます。

## <a name="tokens-list"></a>トークンの一覧
 次の表に、使用可能なトークンを示します。

|名前|説明|
|----------|-----------------|
|$SharePoint.Project.FileName$|格納先のプロジェクト ファイルの名前 (*NewProj.csproj* など)。|
|$SharePoint.Project.FileNameWithoutExtension$|格納しているプロジェクト ファイルのファイル名拡張子を除く名前。 たとえば、"NewProj" のようになります。|
|$SharePoint.Project.AssemblyFullName$|格納しているプロジェクトの出力アセンブリの表示名 (厳密な名前)。|
|$SharePoint.Project.AssemblyFileName$|格納しているプロジェクトの出力アセンブリの名前。|
|$SharePoint.Project.AssemblyFileNameWithoutExtension$|格納しているプロジェクトの出力アセンブリのファイル名拡張子を除く名前。|
|$SharePoint.Project.AssemblyPublicKeyToken$|格納しているプロジェクトの出力アセンブリの公開キー トークンを文字列に変換したもの。 ("x2" 16 進数形式の 16 文字。)|
|$SharePoint.Package.Name$|格納しているパッケージの名前。|
|$SharePoint.Package.FileName$|格納しているパッケージの定義ファイルの名前。|
|$SharePoint.Package.FileNameWithoutExtension$|格納しているパッケージの定義ファイルの名前 (拡張子を除く)。|
|$SharePoint.Package.Id$|格納しているパッケージの SharePoint ID。 フィーチャーが複数のパッケージで使用されている場合、この値は変更されます。|
|$SharePoint.Feature.FileName$|格納しているフィーチャーの定義ファイルの名前 (*Feature1.feature* など)。|
|$SharePoint.Feature.FileNameWithoutExtension$|フィーチャー定義ファイルのファイル名拡張子を除く名前。|
|$SharePoint.Feature.DeploymentPath$|パッケージ内のフィーチャーを含むフォルダーの名前。 このトークンは、フィーチャー デザイナーの "配置パス" プロパティに相当します。 値の例は "Project1_Feature1" です。|
|$SharePoint.Feature.Id$|格納しているフィーチャーの SharePoint ID。 このトークンは、すべてのフィーチャー レベルのトークンと同様に、フィーチャーの外部のパッケージに直接追加されたファイルではなく、フィーチャーを介してパッケージに含まれるファイルでのみ使用できます。|
|$SharePoint.ProjectItem.Name$|**ISharePointProjectItem.Name** から取得したプロジェクト項目の名前 (ファイル名ではありません)。|
|$SharePoint.Type.\<GUID>.AssemblyQualifiedName$|トークンの [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] と一致する型のアセンブリ修飾名。 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] の形式は、小文字で、Guid.ToString("D") 形式 (つまり、xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) に対応しています。|
|$SharePoint.Type.\<GUID>.FullName$|トークン内の GUID と一致する型の完全名。 GUID の形式は、小文字で、Guid.ToString("D") 形式 (つまり、xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) に対応しています。|

## <a name="add-extensions-to-the-token-replacement-file-extensions-list"></a>トークン置換ファイル拡張子の一覧に拡張子を追加する
 理論的には、パッケージに含まれる SharePoint プロジェクト項目に属する任意のファイルでトークンを使用できますが、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、既定でパッケージ ファイル、マニフェスト ファイル、および次の拡張子を持つファイルでのみトークンを検索します。

- [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]

- ASCX

- ASPX

- Webpart

- DWP

  これらの拡張子は、...\\<program files\>\MSBuild\Microsoft\VisualStudio\v11.0\SharePointTools にある Microsoft.VisualStudio.SharePoint.targets ファイル内の `<TokenReplacementFileExtensions>` 要素によって定義されます。

  ただし、一覧にファイル拡張子を追加することもできます。 SharePoint ターゲット ファイルの `<TokenReplacementFileExtensions>` の前に定義されている SharePoint プロジェクト ファイル内の任意の PropertyGroup に \<Import> 要素を追加します。

> [!NOTE]
> トークン置換はプロジェクトのコンパイル後に行われるため、 *.cs*、 *.vb*、 *.resx* など、コンパイルされるファイルの種類のファイル拡張子を追加しないでください。 トークンは、コンパイルされていないファイルでのみ置き換えられます。

 たとえば、ファイル名拡張子 ( *.myextension* と *.yourextension*) をトークン置換ファイル名拡張子の一覧に追加するには、プロジェクト ( *.csproj*) ファイルに以下を追加します。

```xml
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
.
.
.
    <!-- Define the following property to add your extension to the list of token replacement file extensions.  -->
<TokenReplacementFileExtensions>myextension;yourextension</TokenReplacementFileExtensions>
</PropertyGroup>
```

 ターゲット ( *.targets*) ファイルに拡張子を直接追加できます。 ただし、拡張子を追加すると、独自のものだけではなく、ローカル システムでパッケージ化されたすべての SharePoint プロジェクトの拡張子の一覧が変更されます。 この拡張子は、システムに自分以外の開発者がいない場合や、ほとんどのプロジェクトでそれが必要とされる場合に便利です。 ただし、この方法はシステム固有であり、移植性がないため、代わりにプロジェクト ファイルに拡張子を追加することをお勧めします。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
