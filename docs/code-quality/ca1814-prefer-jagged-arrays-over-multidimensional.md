---
title: 'CA1814: Prefer jagged arrays over multidimensional | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
helpviewer_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
ms.assetid: b1ccf563-2ec8-42e5-b89c-731a9de1ea1d
caps.latest.revision: 14
author: stevehoag
ms.author: shoag
manager: wpickett
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 6c9dc51ba44251c765243c55b62fdab77a446aa3
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="ca1814-prefer-jagged-arrays-over-multidimensional"></a>CA1814: Prefer jagged arrays over multidimensional
|||  
|-|-|  
|TypeName|PreferJaggedArraysOverMultidimensional|  
|CheckId|CA1814|  
|Category|Microsoft.Performance|  
|Breaking Change|Breaking|  
  
## <a name="cause"></a>Cause  
 A member is declared as a multidimensional array.  
  
## <a name="rule-description"></a>Rule Description  
 A jagged array is an array whose elements are arrays. The arrays that make up the elements can be of different sizes, leading to less wasted space for some sets of data.  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, change the multidimensional array to a jagged array.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 Suppress a warning from this rule if the multidimensional array does not waste space.  
  
## <a name="example"></a>Example  
 The following example shows declarations for jagged and multidimensional arrays.  
  
 [!code-vb[FxCop.Performance.JaggedArrays#1](../code-quality/codesnippet/VisualBasic/ca1814-prefer-jagged-arrays-over-multidimensional_1.vb)] [!code-csharp[FxCop.Performance.JaggedArrays#1](../code-quality/codesnippet/CSharp/ca1814-prefer-jagged-arrays-over-multidimensional_1.cs)]
