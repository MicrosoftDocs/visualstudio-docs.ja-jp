---
title: 'CA1300: Specify MessageBoxOptions | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SpecifyMessageBoxOptions
- CA1300
helpviewer_keywords:
- SpecifyMessageBoxOptions
- CA1300
ms.assetid: 9357a724-026e-4a3d-a03a-f14635064ec6
caps.latest.revision: 19
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
ms.openlocfilehash: 7d4799fa48ea21c98603ce9aee5de1353618960c
ms.contentlocale: ja-jp
ms.lasthandoff: 08/30/2017

---
# <a name="ca1300-specify-messageboxoptions"></a>CA1300: Specify MessageBoxOptions
|||  
|-|-|  
|TypeName|SpecifyMessageBoxOptions|  
|CheckId|CA1300|  
|Category|Microsoft.Globalization|  
|Breaking Change|Non-breaking|  
  
## <a name="cause"></a>Cause  
 A method calls an overload of the <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> method that does not take a <xref:System.Windows.Forms.MessageBoxOptions?displayProperty=fullName> argument.  
  
## <a name="rule-description"></a>Rule Description  
 To display a message box correctly for cultures that use a right-to-left reading order, the <xref:System.Windows.Forms.MessageBoxOptions> and <xref:System.Windows.Forms.MessageBoxOptions> members of the <xref:System.Windows.Forms.MessageBoxOptions> enumeration must be passed to the <xref:System.Windows.Forms.MessageBox.Show%2A> method. Examine the <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName> property of the containing control to determine whether to use a right-to-left reading order.  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
 To fix a violation of this rule, call an overload of the <xref:System.Windows.Forms.MessageBox.Show%2A> method that takes a <xref:System.Windows.Forms.MessageBoxOptions> argument.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 It is safe to suppress a warning from this rule when the code library will not be localized for a culture that uses a right-to-left reading order.  
  
## <a name="example"></a>Example  
 The following example shows a method that displays a message box that has options that are appropriate for the reading order of the culture. A resource file, which is not shown, is required to build the example. Follow the comments in the example to build the example without a resource file and to test the right-to-left feature.  
  
 [!code-vb[FxCop.Globalization.SpecifyMBOptions#1](../code-quality/codesnippet/VisualBasic/ca1300-specify-messageboxoptions_1.vb)] [!code-csharp[FxCop.Globalization.SpecifyMBOptions#1](../code-quality/codesnippet/CSharp/ca1300-specify-messageboxoptions_1.cs)]  
  
## <a name="see-also"></a>See Also  
 <xref:System.Resources.ResourceManager?displayProperty=fullName>   
 [Resources in Desktop Apps](/dotnet/framework/resources/index)
