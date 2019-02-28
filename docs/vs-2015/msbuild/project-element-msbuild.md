---
title: Project 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Project
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ToolsVersion attribute [MSBuild]
- <Project> element [MSBuild]
- Project element [MSBuild]
ms.assetid: d1cda56a-dbef-4109-9201-39e962e3f653
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b26bd7d5f65122695a96dc5339e39044ff93a924
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54752835"
---
# <a name="project-element-msbuild"></a>Project 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルの必須のルート要素です。  
  
## <a name="syntax"></a>構文  
  
```  
<Project InitialTargets="TargetA;TargetB"  
         DefaultTargets="TargetC;TargetD"  
         TreatAsLocalProperty="PropertyA;PropertyB"  
         ToolsVersion=<version number>  
         xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Choose>... </Choose>  
    <PropertyGroup>... </PropertyGroup>  
    <ItemGroup>... </ItemGroup>  
    <Target>... </Target>  
    <UsingTask.../>  
    <ProjectExtensions>... </ProjectExtensions>  
    <Import... />  
</Project>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|       属性        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `DefaultTargets`    |                                                                                                                                                                                                                                                                                                 省略可能な属性です。<br /><br /> ターゲットが指定されていない場合にビルドのエントリ ポイントとなる 1 つまたは複数の既定のターゲット。 複数のターゲットはセミコロン (;) で区切られます。<br /><br /> `DefaultTargets` 属性または [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] コマンド ラインのいずれかで既定のターゲットが指定されていない場合、[Import](../msbuild/import-element-msbuild.md) 要素の評価後、エンジンはプロジェクト ファイルの最初のターゲットを実行します。                                                                                                                                                                                                                                                                                                  |
|    `InitialTargets`    |                                                                                                                                                                                                                                                                                                                                                                                                                                             省略可能な属性です。<br /><br /> `DefaultTargets` 属性またはコマンド ラインで指定されたターゲットの前に実行される 1 つまたは複数の初期ターゲット。 複数のターゲットはセミコロン (;) で区切られます。                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|     `ToolsVersion`     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             省略可能な属性です。<br /><br /> MSBuild が $(MSBuildBinPath) と $(MSBuildToolsPath) の値を決定するために使用するツールセットのバージョン。                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `TreatAsLocalProperty` | 省略可能な属性です。<br /><br /> グローバルとは見なされないプロパティ名。 この属性は、プロジェクトまたはターゲット ファイル、および後続のすべてのインポートに設定されているプロパティ値が特定のコマンド ライン プロパティによってオーバーライドされることを防ぎます。 複数のプロパティはセミコロン (;) で区切られます。<br /><br /> 通常、グローバル プロパティは、プロジェクト ファイルまたはターゲット ファイルで設定されたプロパティ値をオーバーライドします。 プロパティが `TreatAsLocalProperty` 値に一覧表示されている場合、グローバル プロパティ値は、そのファイルと後続のインポートに設定されているプロパティ値をオーバーライドしません。 詳細については、「[方法 : 同じソース ファイルを異なるオプションでビルドする](../msbuild/how-to-build-the-same-source-files-with-different-options.md)」を参照してください。 **注:**  グローバル プロパティは、コマンド プロンプトで **/property** (または **/p**) スイッチを使用して設定します。 また、複数プロジェクト ビルドの子プロジェクトのグローバル プロパティは、MSBuild タスクの `Properties` 属性を使用して設定または変更することもできます。 詳細については、「[MSBuild タスク](../msbuild/msbuild-task.md)」を参照してください。 |
|        `Xmlns`         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 必須の属性です。<br /><br /> `xmlns`属性の値が必要"<http://schemas.microsoft.com/developer/msbuild/2003>"。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Choose](../msbuild/choose-element-msbuild.md)|省略可能な要素です。<br /><br /> 子要素を評価して、`ItemGroup` 要素および/または `PropertyGroup` 要素の 1 つのセットを評価対象に選択します。|  
|[Import](../msbuild/import-element-msbuild.md)|省略可能な要素です。<br /><br /> プロジェクト ファイルが別のプロジェクト ファイルをインポートできるようにします。 1 つのプロジェクトに 0 個以上の `Import` 要素を含めることができます。|  
|[ItemGroup](../msbuild/itemgroup-element-msbuild.md)|省略可能な要素です。<br /><br /> 個々の項目の grouping 要素。 項目は [Item](../msbuild/item-element-msbuild.md) 要素を使用して指定されます。 1 つのプロジェクトに 0 個以上の `ItemGroup` 要素を含めることができます。|  
|[ProjectExtensions](../msbuild/projectextensions-element-msbuild.md)|省略可能な要素です。<br /><br /> [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルに [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 以外の情報を保持する方法を提供します。 1 つのプロジェクトに 0 個または 1 個の `ProjectExtensions` 要素を含めることができます。|  
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|省略可能な要素です。<br /><br /> 個々のプロパティの grouping 要素。 プロパティは [Property](../msbuild/property-element-msbuild.md) 要素を使用して指定されます。 1 つのプロジェクトに 0 個以上の `PropertyGroup` 要素を含めることができます。|  
|[Target](../msbuild/target-element-msbuild.md)|省略可能な要素です。<br /><br /> [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] が順次実行するタスクのセットを格納します。 タスクは [Task](../msbuild/task-element-msbuild.md) 要素を使用して指定されます。 1 つのプロジェクトに 0 個以上の `Target` 要素を含めることができます。|  
|[UsingTask](../msbuild/usingtask-element-msbuild.md)|省略可能な要素です。<br /><br /> [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] にタスクを登録する方法を提供します。 1 つのプロジェクトに 0 個以上の `UsingTask` 要素を含めることができます。|  
  
### <a name="parent-elements"></a>親要素  
 なし。  
  
## <a name="see-also"></a>関連項目
 [方法 : 最初にビルドするターゲットを指定する](../msbuild/how-to-specify-which-target-to-build-first.md)   
 [Command-Line Reference (コマンド ライン リファレンス)](../msbuild/msbuild-command-line-reference.md)   
 [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)   
 [MSBuild](msbuild.md)
