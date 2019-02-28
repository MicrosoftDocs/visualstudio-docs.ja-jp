---
title: PropertyGroup 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#PropertyGroup
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <PropertyGroup> element [MSBuild]
- PropertyGroup element [MSBuild]
ms.assetid: ff1e6c68-b9a1-4263-a1ce-dc3b829a64d4
caps.latest.revision: 24
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fb3ae2ba566c42ef1cde10e4a758fe8f9698ed13
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54772528"
---
# <a name="propertygroup-element-msbuild"></a>PropertyGroup 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
ユーザー定義の [Property](../msbuild/property-element-msbuild.md) 要素のセットを格納します。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトで使用される各 `Property` 要素は、`PropertyGroup` 要素の子である必要があります。  
  
 \<Project>  
 \<PropertyGroup >  
  
## <a name="syntax"></a>構文  
  
```  
<PropertyGroup Condition="'String A' == 'String B'">  
    <Property1>...</Property1>  
    <Property2>...</Property2>  
</PropertyGroup>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|条件|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Property](../msbuild/property-element-msbuild.md)|省略可能な要素です。<br /><br /> プロパティ値を格納する、ユーザー定義のプロパティ名。 1 つの `PropertyGroup` 要素に 0 個以上の *Property* 要素を含めることができます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[プロジェクト](../msbuild/project-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルの必須のルート要素です。|  
  
## <a name="example"></a>例  
 条件に基づいてプロパティを設定する方法を次のコード例に示します。 この例では、`CompileConfig` プロパティの値が `DEBUG` の場合に、`PropertyGroup` 要素内の `Optimization` プロパティ、`Obfuscate` プロパティ、`OutputPath` プロパティが設定されます。  
  
```  
<PropertyGroup Condition="'$(CompileConfig)' == 'DEBUG'" >  
    <Optimization>false</Optimization>  
    <Obfuscate>false</Obfuscate>  
    <OutputPath>$(OutputPath)\debug</OutputPath>  
</PropertyGroup>  
```  
  
## <a name="see-also"></a>関連項目
 [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)  
 [MSBuild プロパティ](msbuild-properties1.md)
