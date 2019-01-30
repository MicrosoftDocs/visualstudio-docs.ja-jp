---
title: ImportGroup 要素 | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <ImportGroup> element [MSBuild]
- ImportGroup element [MSBuild]
ms.assetid: dac3fa2d-6678-4017-af35-93686f53f302
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 97d5aeac5115dfa251b42c824b88a779e22ad6a4
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54978335"
---
# <a name="importgroup-element"></a>ImportGroup 要素
オプションの条件下でグループ化された `Import` 要素のコレクションが格納されます。 詳しくは、「[Import 要素 (MSBuild)](../msbuild/import-element-msbuild.md)」をご覧ください。  

 \<Project>  
 \<ImportGroup>  

## <a name="syntax"></a>構文  

```xml  
<ImportGroup Condition="'String A' == 'String B'">  
    <Import ... />  
    <Import ... />  
</ImportGroup>  
```  

## <a name="attributes-and-elements"></a>属性と要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  

### <a name="attributes"></a>属性  

|属性|説明|  
|---------------|-----------------|  
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|  

### <a name="child-elements"></a>子要素  

|要素|説明|  
|-------------|-----------------|  
|[Import](../msbuild/import-element-msbuild.md)|1 つのプロジェクト ファイルの内容を別のプロジェクト ファイルにインポートします。|  

### <a name="parent-elements"></a>親要素  

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクト ファイルの必須のルート要素です。 |

## <a name="example"></a>例  
 次に示すのは、`ImportGroup` 要素のコード例です。  

```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ImportGroup>  
        <Import Project="$(Targets1.targets)" />  
        <Import Project="$(Targets2.targets)" />  
    </ImportGroup>  
...  
</Project>  
```  

## <a name="see-also"></a>関連項目  
 [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)   
 [項目](../msbuild/msbuild-items.md)
