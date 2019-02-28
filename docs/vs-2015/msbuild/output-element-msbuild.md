---
title: Output 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Output
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Output> Element [MSBuild]
- Output Element [MSBuild]
ms.assetid: 34bc7cd1-efd3-4b57-b691-4584eeb6a0e9
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 327f65ef6639f444326d59d6db990e9c732a760f
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54790285"
---
# <a name="output-element-msbuild"></a>Output 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
タスクの出力値をアイテムとプロパティに格納します。  
  
 \<Project>  
 \<Target>  
 \<Task>  
 \<Output>  
  
## <a name="syntax"></a>構文  
  
```  
<Output TaskParameter="Parameter"  
    PropertyName="PropertyName"   
    Condition = "'String A' == 'String B'" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`TaskParameter`|必須の属性です。<br /><br /> タスクの出力パラメーターの名前です。|  
|`PropertyName`|`PropertyName` 属性と `ItemName` 属性のどちらかが必要です。<br /><br /> タスクの出力パラメーターの値を受け取るプロパティです。 プロジェクトは、`$(`*PropertyName*`)` 構文でプロパティを参照できます。 このプロパティ名は、新しいプロパティ名でも、プロジェクトで既に定義されている名前でもかまいません。<br /><br /> `ItemName` が使われている場合、この属性を使うことはできません。|  
|`ItemName`|`PropertyName` 属性と `ItemName` 属性のどちらかが必要です。<br /><br /> タスクの出力パラメーターの値を受け取るアイテムです。 プロジェクトは、`@(`*ItemName*`)` 構文でアイテムを参照できます。 アイテム名は、新しいアイテム名でも、プロジェクトで既に定義されている名前でもかまいません。<br /><br /> `PropertyName` が使われている場合、この属性を使うことはできません。|  
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Task](../msbuild/task-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクのインスタンスを作成し、実行します。|  
  
## <a name="example"></a>例  
 次のコード例では、`Target` タスクが `Csc` 要素の内部で実行されています。 タスクのパラメーターに渡されるアイテムとプロパティは、この例のスコープ外で宣言されています。 出力パラメーター `OutputAssembly` からの値は `FinalAssemblyName` アイテムに格納され、出力パラメーター `BuildSucceeded` からの値は `BuildWorked` プロパティに格納されます。 詳細については、[タスク](../msbuild/msbuild-tasks.md)に関する記事を参照してください。  
  
```  
<Target Name="Compile" DependsOnTargets="Resources">  
    <Csc  Sources="@(CSFile)"  
            TargetType="library"  
            Resources="@(CompiledResources)"  
            EmitDebugInformation="$(includeDebugInformation)"  
            References="@(Reference)"  
            DebugType="$(debuggingType)"  
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).dll" >  
        <Output TaskParameter="OutputAssembly"  
                  ItemName="FinalAssemblyName" />  
        <Output TaskParameter="BuildSucceeded"  
                  PropertyName="BuildWorked" />  
    </Csc>  
</Target>  
```  
  
## <a name="see-also"></a>関連項目
 [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)   
 [タスク](../msbuild/msbuild-tasks.md)
