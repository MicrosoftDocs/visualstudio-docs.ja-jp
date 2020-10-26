---
title: '方法: MSBuild で特殊文字をエスケープする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- special characters, escaping
- characters, escapes
- escape characters
- MSBuild, escaping special characters
ms.assetid: 1aa3669c-1647-4960-b770-752e2532102f
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 94fc8d858e2db9bd1e00bb8770cf52672a900ab0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178349"
---
# <a name="how-to-escape-special-characters-in-msbuild"></a>方法 : MSBuild で特殊文字をエスケープする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルでは、特定の文字が特殊な意味を持ちます。 そのような文字の例として、セミコロン (;) およびアスタリスク (*) があります。 特殊文字の完全な一覧については、「[MSBuild の特殊文字](../msbuild/msbuild-special-characters.md)」をご覧ください。  
  
 これらの特殊文字をプロジェクトファイル内でリテラルとして使用するには、構文%*xx*を使用して指定する必要があります。 *xx* は文字の ASCII 16 進値を表します。  
  
## <a name="msbuild-special-characters"></a>MSBuild の特殊文字  
 特殊文字が使用される場所の 1 つの例として、アイテム一覧の `Include` 属性が挙げられます。 たとえば、次のアイテム一覧では、`MyFile.cs` および `MyClass.cs` の 2 つのアイテムを宣言しています。  
  
```  
<Compile Include="MyFile.cs;MyClass.cs"/>  
```  
  
 名前にセミコロンを含むアイテムを宣言する場合は、構文 %*xx* を使用してセミコロンをエスケープし、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] によって 2 つの別々のアイテムが宣言されることを防ぐ必要があります。 たとえば、次のアイテムではセミコロンをエスケープして、`MyFile.cs;MyClass.cs` という名前の 1 つのアイテムを宣言しています。  
  
```  
<Compile Include="MyFile.cs%3BMyClass.cs"/>  
```  
  
#### <a name="to-use-an-msbuild-special-character-as-a-literal-character"></a>MSBuild の特殊文字をリテラル文字として使用するには  
  
- 特殊文字の代わりに % *xx* という表記を使用します。ここで、*xx* は ASCII 文字の 16 進値を表します。 たとえば、アスタリスク (*) をリテラル文字として使用するには、値 `%2A` を使用します。  
  
## <a name="see-also"></a>参照  
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [MSBuild](msbuild.md) [項目](../msbuild/msbuild-items.md)
