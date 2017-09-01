---
title: 'CA2213: Disposable fields should be disposed | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- DisposableFieldsShouldBeDisposed
- CA2213
helpviewer_keywords:
- CA2213
- DisposableFieldsShouldBeDisposed
ms.assetid: e99442c9-70e2-47f3-b61a-d8ac003bc6e5
caps.latest.revision: 15
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
ms.openlocfilehash: 538f013849b8e3391fdc3cdad7fee707e9cbb072
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213: Disposable fields should be disposed
|||  
|-|-|  
|TypeName|DisposableFieldsShouldBeDisposed|  
|CheckId|CA2213|  
|Category|Microsoft.Usage|  
|Breaking Change|Non Breaking|  
  
## <a name="cause"></a>Cause  
 A type that implements <xref:System.IDisposable?displayProperty=fullName> declares fields that are of types that also implement <xref:System.IDisposable>. The <xref:System.IDisposable.Dispose%2A> method of the field is not called by the <xref:System.IDisposable.Dispose%2A> method of the declaring type.  
  
## <a name="rule-description"></a>Rule Description  
 A type is responsible for disposing of all its unmanaged resources; this is accomplished by implementing <xref:System.IDisposable>. This rule checks to see whether a disposable type `T` declares a field `F` that is an instance of a disposable type `FT`. For each field `F`, the rule attempts to locate a call to `FT.Dispose`. The rule searches the methods called by `T.Dispose`, and one level lower (the methods called by the methods called by `FT.Dispose`).  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, call <xref:System.IDisposable.Dispose%2A> on fields that are of types that implement <xref:System.IDisposable> if you are responsible for allocating and releasing the unmanaged resources held by the field.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 It is safe to suppress a warning from this rule if you are not responsible for releasing the resource held by the field, or if the call to <xref:System.IDisposable.Dispose%2A> occurs at a deeper calling level than the rule checks.  
  
## <a name="example"></a>Example  
 The following example shows a type `TypeA` that implements <xref:System.IDisposable> (`FT` in the previosu discussion).  
  
 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../code-quality/codesnippet/CSharp/ca2213-disposable-fields-should-be-disposed_1.cs)]  
  
## <a name="example"></a>Example  
 The following example shows a type `TypeB` that violates this rule by declaring a field `aFieldOfADisposableType` (`F` in the previous discussion) as a disposable type (`TypeA`) and not calling <xref:System.IDisposable.Dispose%2A> on the field. `TypeB` corresponds to `T` in the previous discussion.  
  
 [!code-csharp[FxCop.Usage.IDisposableFields#1](../code-quality/codesnippet/CSharp/ca2213-disposable-fields-should-be-disposed_2.cs)]  
  
## <a name="see-also"></a>See Also  
 <xref:System.IDisposable?displayProperty=fullName>   
 [Dispose Pattern](/dotnet/standard/design-guidelines/dispose-pattern)
