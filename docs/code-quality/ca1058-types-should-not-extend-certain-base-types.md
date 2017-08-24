---
title: 'CA1058: Types should not extend certain base types | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TypesShouldNotExtendCertainBaseTypes
- CA1058
helpviewer_keywords:
- CA1058
- TypesShouldNotExtendCertainBaseTypes
ms.assetid: 8446ee40-beb1-49fa-8733-4d8e813471c0
caps.latest.revision: 24
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
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: a2c632656683e36329eda655da2b018020aa3c82
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="ca1058-types-should-not-extend-certain-base-types"></a>CA1058: Types should not extend certain base types
|||  
|-|-|  
|TypeName|TypesShouldNotExtendCertainBaseTypes|  
|CheckId|CA1058|  
|Category|Microsoft.Design|  
|Breaking Change|Breaking|  
  
## <a name="cause"></a>Cause  
 An externally visible type extends certain base types. Currently, this rule reports types that derive from the following types:  
  
-   <xref:System.ApplicationException?displayProperty=fullName>  
  
-   <xref:System.Xml.XmlDocument?displayProperty=fullName>  
  
-   <xref:System.Collections.CollectionBase?displayProperty=fullName>  
  
-   <xref:System.Collections.DictionaryBase?displayProperty=fullName>  
  
-   <xref:System.Collections.Queue?displayProperty=fullName>  
  
-   <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>  
  
-   <xref:System.Collections.SortedList?displayProperty=fullName>  
  
-   <xref:System.Collections.Stack?displayProperty=fullName>  
  
## <a name="rule-description"></a>Rule Description  
 For [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] version 1, it was recommended to derive new exceptions from <xref:System.ApplicationException>. The recommendation has changed and new exceptions should derive from <xref:System.Exception?displayProperty=fullName> or one of its subclasses in the <xref:System> namespace.  
  
 Do not create a subclass of <xref:System.Xml.XmlDocument> if you want to create an XML view of an underlying object model or data source.  
  
### <a name="non-generic-collections"></a>Non-generic Collections  
 Use and/or extend generic collections whenever possible. Do not extend non-generic collections in your code, unless you shipped it previously.  
  
 **Examples of Incorrect Usage**  
  
```cs  
public class MyCollection : CollectionBase  
{  
}  
  
public class MyReadOnlyCollection : ReadOnlyCollectionBase  
{  
}  
```  
  
 **Examples of Correct Usage**  
  
```cs  
public class MyCollection : Collection<T>  
{  
}  
  
public class MyReadOnlyCollection : ReadOnlyCollection<T>  
{  
}  
```  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, derive the type from a different base type or a generic collection.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 Do not suppress a warning from this rule for violations about <xref:System.ApplicationException>. It is safe to suppress a warning from this rule for violations about <xref:System.Xml.XmlDocument>. It is safe to suppress a warning about a non-generic collection if the code was released previously.
