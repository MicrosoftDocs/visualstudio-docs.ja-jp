---
title: T4 アセンブリ ディレクティブ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 44949749-ce3c-4fb5-8690-a17f1564ac2f
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9fa00e8b5aafa131a9ca64b6fdaa7cba79fcb3b2
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60074217"
---
# <a name="t4-assembly-directive"></a>T4 アセンブリ ディレクティブ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のデザイン時テキスト テンプレートでは、テンプレート コードでアセンブリの型を使用できるように、`assembly` ディレクティブによってアセンブリが読み込まれます。 結果は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトでアセンブリ参照を追加した場合と同様です。  
  
 テキスト テンプレートの作成方法の一般的な概要については、次を参照してください。 [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)  
  
> [!NOTE]
>  実行時 (前処理された) テキスト テンプレートでは、`assembly` ディレクティブは不要です。 代わりに必要なアセンブリを追加、**参照**の[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プロジェクト。  
  
## <a name="using-the-assembly-directive"></a>assembly ディレクティブの使用  
 ディレクティブの構文は次のとおりです。  
  
```  
<#@ assembly name="[assembly strong name|assembly file name]" #>  
```  
  
 アセンブリ名は、次のいずれかであることが必要です。  
  
- GAC のアセンブリの厳密な名前 (`System.Xml.dll` など)。 `name="System.Xml, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"` のような長い形式を使用することもできます。 詳細については、「 <xref:System.Reflection.AssemblyName> 」を参照してください。  
  
- アセンブリの絶対パス。  
  
  `$(variableName)` 構文を使用して、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の変数 (`$(SolutionDir)` など) を参照し、`%VariableName%` を使用して環境変数を参照できます。 例えば:  
  
```  
<#@ assembly name="$(SolutionDir)\MyProject\bin\Debug\SomeLibrary.Dll" #>  
```  
  
 assembly ディレクティブは、前処理されたテキスト テンプレートでは無効です。 代わりで必要な参照を含める、**参照**のセクション、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プロジェクト。 詳細については、次を参照してください。 [T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)  
  
## <a name="standard-assemblies"></a>標準アセンブリ  
 次のアセンブリは自動的に読み込まれるので、これらのアセンブリのアセンブリ ディレクティブを記述する必要はありません。  
  
- `Microsoft.VisualStudio.TextTemplating.1*.dll`  
  
- `System.dll`  
  
- `WindowsBase.dll`  
  
  カスタム ディレクティブを使用する場合は、ディレクティブ プロセッサによって追加のアセンブリが読み込まれます。 たとえば、ドメイン固有言語 (DSL) のテンプレートを作成した場合、次のアセンブリのアセンブリ ディレクティブを記述する必要はありません。  
  
- `Microsoft.VisualStudio.Modeling.Sdk.1*.dll`  
  
- `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.1*.dsl`  
  
- `Microsoft.VisualStudio.TextTemplating.Modeling.1*.dll`  
  
- DSL を含むアセンブリ  
  
## <a name="msbuild"></a> MSBuild および Visual Studio の両方でのプロジェクト プロパティの使用  
 $(SolutionDir) などの Visual Studio のマクロは、MSBuild では動作しません。 ビルド コンピューターでテンプレートを変換する場合、代わりにプロジェクトのプロパティを使用する必要があります。  
  
 .csproj ファイルまたは .vbproj ファイルを編集してプロジェクトのプロパティを定義します。 この例では、`myLibFolder` という名前のプロパティを定義します。  
  
```xml  
<!-- Define a project property, myLibFolder: -->  
<PropertyGroup>  
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>  
</PropertyGroup>  
  
<!-- Tell the MSBuild T4 task to make the property available: -->  
<ItemGroup>  
    <T4ParameterValues Include="myLibFolder">  
      <Value>$(myLibFolder)</Value>  
    </T4ParameterValues>  
  </ItemGroup>  
  
```  
  
 これで、Visual Studio および MSBuild の両方で正しく変換できるテキスト テンプレートでプロジェクトのプロパティを使用できます。  
  
```  
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>  
```  
  
## <a name="see-also"></a>関連項目  
 [T4 インクルード ディレクティブ](../modeling/t4-include-directive.md)
