---
title: 'CA1038: Enumerators should be strongly typed | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
helpviewer_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
ms.assetid: 8919f526-d487-42a4-87dc-2b2ee25260c4
caps.latest.revision: 16
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
ms.openlocfilehash: 5ba630f68e9c49c755ab047a14a907822bee42e5
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="ca1038-enumerators-should-be-strongly-typed"></a>CA1038: Enumerators should be strongly typed
|||  
|-|-|  
|TypeName|EnumeratorsShouldBeStronglyTyped|  
|CheckId|CA1038|  
|Category|Microsoft.Design|  
|Breaking Change|Breaking|  
  
## <a name="cause"></a>Cause  
 A public or protected type implements <xref:System.Collections.IEnumerator?displayProperty=fullName> but does not provide a strongly typed version of the <xref:System.Collections.IEnumerator.Current%2A?displayProperty=fullName> property. Types that are derived from the following types are exempt from this rule:  
  
-   <xref:System.Collections.CollectionBase?displayProperty=fullName>  
  
-   <xref:System.Collections.DictionaryBase?displayProperty=fullName>  
  
-   <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>  
  
## <a name="rule-description"></a>Rule Description  
 This rule requires <xref:System.Collections.IEnumerator> implementations to also provide a strongly typed version of the <xref:System.Collections.IEnumerator.Current%2A> property so that users are not required to cast the return value to the strong type when they use the functionality that is provided by the interface. This rule assumes that the type that implements <xref:System.Collections.IEnumerator> contains a collection of instances of a type that is stronger than <xref:System.Object>.  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, implement the interface property explicitly (declare it as `IEnumerator.Current`). Add a public strongly typed version of the property, declared as `Current`, and have it return a strongly typed object.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 Suppress a warning from this rule when you implement an object-based enumerator for use with an object-based collection, such as a binary tree. Types that extend the new collection will define the strongly typed enumerator and expose the strongly typed property.  
  
## <a name="example"></a>Example  
 The following example demonstrates the correct way to implement a strongly typed <xref:System.Collections.IEnumerator> type.  
  
 [!code-csharp[FxCop.Design.IEnumeratorStrongTypes#1](../code-quality/codesnippet/CSharp/ca1038-enumerators-should-be-strongly-typed_1.cs)]  
  
## <a name="related-rules"></a>Related Rules  
 [CA1035: ICollection implementations have strongly typed members](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)  
  
 [CA1039: Lists are strongly typed](../code-quality/ca1039-lists-are-strongly-typed.md)  
  
## <a name="see-also"></a>See Also  
 <xref:System.Collections.IEnumerator?displayProperty=fullName>   
 <xref:System.Collections.CollectionBase?displayProperty=fullName>   
 <xref:System.Collections.DictionaryBase?displayProperty=fullName>   
 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
