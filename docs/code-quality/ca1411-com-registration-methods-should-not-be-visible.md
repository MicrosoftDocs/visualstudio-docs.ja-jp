---
title: 'CA1411: COM registration methods should not be visible | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA1411
- ComRegistrationMethodsShouldNotBeVisible
helpviewer_keywords:
- ComRegistrationMethodsShouldNotBeVisible
- CA1411
ms.assetid: a59f96f1-1f38-4596-b656-947df5c55311
caps.latest.revision: 13
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
ms.openlocfilehash: 258ba05d74c41a43e5968b10867b38b982859e94
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="ca1411-com-registration-methods-should-not-be-visible"></a>CA1411: COM registration methods should not be visible
|||  
|-|-|  
|TypeName|ComRegistrationMethodsShouldNotBeVisible|  
|CheckId|CA1411|  
|Category|Microsoft.Interoperability|  
|Breaking Change|Breaking|  
  
## <a name="cause"></a>Cause  
 A method that is marked with the <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> or the <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> attribute is externally visible.  
  
## <a name="rule-description"></a>Rule Description  
 When an assembly is registered with Component Object Model (COM), entries are added to the registry for each COM-visible type in the assembly. Methods that are marked with the <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> and <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> attributes are called during the registration and unregistration processes, respectively, to run user code that is specific to the registration/unregistration of these types. This code should not be called outside these processes.  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, change the accessibility of the method to `private` or `internal` (`Friend` in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]).  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 Do not suppress a warning from this rule.  
  
## <a name="example"></a>Example  
 The following example shows two methods that violate the rule.  
  
 [!code-csharp[FxCop.Interoperability.ComRegistration2#1](../code-quality/codesnippet/CSharp/ca1411-com-registration-methods-should-not-be-visible_1.cs)] [!code-vb[FxCop.Interoperability.ComRegistration2#1](../code-quality/codesnippet/VisualBasic/ca1411-com-registration-methods-should-not-be-visible_1.vb)]  
  
## <a name="related-rules"></a>Related Rules  
 [CA1410: COM registration methods should be matched](../code-quality/ca1410-com-registration-methods-should-be-matched.md)  
  
## <a name="see-also"></a>See Also  
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>   
 [Registering Assemblies with COM](/dotnet/framework/interop/registering-assemblies-with-com)   
 [Regasm.exe (Assembly Registration Tool)](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)
