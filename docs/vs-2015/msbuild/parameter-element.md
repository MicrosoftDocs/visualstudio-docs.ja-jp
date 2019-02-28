---
title: Parameter 要素 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Parameter element [MSBuild]
- <Parameter> element [MSBuild]
ms.assetid: b273afff-b500-4e97-8cfd-31f39fa64a51
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4c53528159d2950378c56e1da22d81393235f716
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54803383"
---
# <a name="parameter-element"></a>Parameter 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
`UsingTask``TaskFactory` によって生成されるタスクの固有のパラメーターについての情報が格納されます。  要素の名前はパラメーターの名前です。  詳しくは、「[UsingTask 要素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)」をご覧ください。  
  
 \<Project>  
 \<UsingTask>  
 \<ParameterGroup>  
 \<Parameter>  
  
## <a name="syntax"></a>構文  
  
```  
<ParameterGroup ParameterType="SystemType"  
    Output="true/false"  
    Required="true/false" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`ParameterType`|省略可能な属性です。<br /><br /> パラメーターの .NET 型です ("System.String" など)。|  
|`Output`|省略可能な Boolean 属性です。<br /><br /> `true` の場合、このパラメーターはタスクの出力パラメーターです。 既定では、値は `false` です。|  
|`Required`|省略可能な Boolean 属性です。<br /><br /> `true` の場合、このパラメーターはタスクの必須パラメーターです。 既定では、値は `false` です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[ParameterGroup](../msbuild/parametergroup-element.md)|`UsingTask``TaskFactory` によって生成されるタスクで使用される省略可能なパラメーターのリストが格納されます。|  
  
## <a name="example"></a>例  
 `Parameter` 要素を使用する方法を次の例に示します。  
  
```  
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">  
       <ParameterGroup>  
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>  
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>  
             ...  
</ParameterGroup>  
       <TaskBody Evaluate="true">  
      ... Task factory-specific data ...  
       </TaskBody>  
</UsingTask>  
```  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
