---
title: 'CA2002: Do not lock on objects with weak identity | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- DoNotLockOnObjectsWithWeakIdentity
- CA2002
helpviewer_keywords:
- CA2002
- DoNotLockOnObjectsWithWeakIdentity
ms.assetid: 16100b39-c6fc-452b-8fca-8b459a26c286
caps.latest.revision: 16
author: stevehoag
ms.author: shoag
manager: wpickett
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: eb5c9550fd29b0e98bf63a7240737da4f13f3249
ms.openlocfilehash: 15e189741636255f83086e1877abad80fb3da57b
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="ca2002-do-not-lock-on-objects-with-weak-identity"></a>CA2002: Do not lock on objects with weak identity
|||  
|-|-|  
|TypeName|DoNotLockOnObjectsWithWeakIdentity|  
|CheckId|CA2002|  
|Category|Microsoft.Reliability|  
|Breaking Change|Non-breaking|  
  
## <a name="cause"></a>Cause  
 A thread attempts to acquire a lock on an object that has a weak identity.  
  
## <a name="rule-description"></a>Rule Description  
 An object is said to have a weak identity when it can be directly accessed across application domain boundaries. A thread that tries to acquire a lock on an object that has a weak identity can be blocked by a second thread in a different application domain that has a lock on the same object. The following types have a weak identity and are flagged by the rule:  
  
-   <xref:System.MarshalByRefObject>  
  
-   <xref:System.ExecutionEngineException>  
  
-   <xref:System.OutOfMemoryException>  
  
-   <xref:System.StackOverflowException>  
  
-   <xref:System.String>  
  
-   <xref:System.Reflection.MemberInfo>  
  
-   <xref:System.Reflection.ParameterInfo>  
  
-   <xref:System.Threading.Thread>  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, use an object from a type that is not in the list in the Description section.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 Do not suppress a warning from this rule.  
  
## <a name="related-rules"></a>Related Rules  
 [CA2213: Disposable fields should be disposed](../code-quality/ca2213-disposable-fields-should-be-disposed.md)  
  
## <a name="example"></a>Example  
 The following example shows some object locks that violate the rule.  
  
 [!code-vb[FxCop.Reliability.LockWeakObjects#1](../code-quality/codesnippet/VisualBasic/ca2002-do-not-lock-on-objects-with-weak-identity_1.vb)] [!code-csharp[FxCop.Reliability.LockWeakObjects#1](../code-quality/codesnippet/CSharp/ca2002-do-not-lock-on-objects-with-weak-identity_1.cs)]  
  
## <a name="see-also"></a>See Also  
 <xref:System.Threading.Monitor>   
 <xref:System.AppDomain>   
 [lock Statement](/dotnet/csharp/language-reference/keywords/lock-statement)   
 [SyncLock Statement](/dotnet/visual-basic/language-reference/statements/synclock-statement)
