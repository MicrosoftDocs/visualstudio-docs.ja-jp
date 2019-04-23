---
title: MSBuild の特殊文字 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- escape characters
- escape
- MSBuild Escape Characters
ms.assetid: 545e6a59-1093-4514-935e-78679a46fb3c
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a54f446cb82b3181ee057d4887b37940868a5920
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59650799"
---
# <a name="msbuild-special-characters"></a>MSBuild の特殊文字
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、特定の文脈で特別な使い方をするためにいくつかの文字が予約されています。 予約されている文脈でそのような文字を文字通り使用するには、エスケープする必要があります。 たとえば、アスタリスクは、項目定義の `Include` 属性と `Exclude` 属性、ならびに `CreateItem` の呼び出しで特別な意味を持ちます。 このような文脈でアスタリスクをアスタリスクとして表示するには、エスケープする必要があります。 その他の文脈では、アスタリスクを使う場所でそれを入力できます。  
  
 特殊文字をエスケープするには、構文 %*xx* を使用します。*xx* は、文字の ASCII 16 進数値を表します。 詳細については、「[方法 :MSBuild で特殊文字をエスケープ](../msbuild/how-to-escape-special-characters-in-msbuild.md)します。  
  
## <a name="special-characters"></a>特殊文字  
 次の表は、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] の特殊文字をまとめたものです。  
  
|**文字**|**ASCII**|**予約されている使用方法**|  
|-------------------|---------------|------------------------|  
|%|%25|メタデータを参照する|  
|$|%24|プロパティを参照する|  
|@|%40|項目一覧を参照する|  
|'|%27|条件とその他の式|  
|;|%3B|一覧の区切り記号|  
|?|%3F|`Include` 属性と `Exclude` 属性のファイル名のワイルドカード文字|  
|*|%2A|`Include` 属性と `Exclude` 属性のファイル名で使用するワイルドカード文字|  
  
## <a name="see-also"></a>関連項目  
 [詳細な概念](../msbuild/msbuild-advanced-concepts.md)   
 [項目](../msbuild/msbuild-items.md)
