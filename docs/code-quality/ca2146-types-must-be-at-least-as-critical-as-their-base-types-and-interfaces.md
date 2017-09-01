---
title: 'CA2146: Types must be at least as critical as their base types and interfaces | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA2146
ms.assetid: 241fb784-1f6b-46e5-8ceb-c438e341d38e
caps.latest.revision: 11
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
ms.openlocfilehash: ee68c96bff15b6abb238221d43e6c0dfdff32c4f
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces"></a>CA2146: Types must be at least as critical as their base types and interfaces
|||  
|-|-|  
|TypeName|TypesMustBeAtLeastAsCriticalAsBaseTypes|  
|CheckId|CA2146|  
|Category|Microsoft.Security|  
|Breaking Change|Breaking|  
  
## <a name="cause"></a>Cause  
 A transparent type is derived from a type that is marked with the <xref:System.Security.SecuritySafeCriticalAttribute> or the <xref:System.Security.SecurityCriticalAttribute>, or a type that is marked with the <xref:System.Security.SecuritySafeCriticalAttribute> attribute is derived from a type that is marked with the <xref:System.Security.SecurityCriticalAttribute> attribute.  
  
## <a name="rule-description"></a>Rule Description  
 This rule fires when a derived type has a security transparency attribute that is not as critical as its base type or implemented interface. Only critical types can derive from critical base types or implement critical interfaces, and only critical or safe-critical types can derive from safe-critical base types or implement safe-critical interfaces. Violations of this rule in level 2 transparency result in a <xref:System.TypeLoadException> for the derived type.  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix this violation, mark the derived or implementing type with a transparency attribute that is at least as critical as the base type or interface.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 Do not suppress a warning from this rule.  
  
## <a name="example"></a>Example  
 [!code-csharp[FxCop.Security.CA2146.TypesMustBeAtLeastAsCriticalAsBaseTypes#1](../code-quality/codesnippet/CSharp/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces_1.cs)]
