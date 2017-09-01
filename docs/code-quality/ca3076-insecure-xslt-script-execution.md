---
title: 'CA3076: Insecure XSLT Script Execution | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 53cb7a46-c564-488f-bc51-0e210a7853c9
caps.latest.revision: 5
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
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 5203c83fb8d9f4fb1dcc729ff6cd95937da1dead
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="ca3076-insecure-xslt-script-execution"></a>CA3076: Insecure XSLT Script Execution
|||  
|-|-|  
|TypeName|InsecureXSLTScriptExecution|  
|CheckId|CA3076|  
|Category|Microsoft.Security|  
|Breaking Change|Non Breaking|  
  
## <a name="cause"></a>Cause  
 If you execute [Extensible Stylesheets Language Transformations (XSLT)](https://support.microsoft.com/en-us/kb/313997) in .NET applications insecurely, the processor may [resolve untrusted URI references](http://msdn.microsoft.com/en-us/ba3e4d4f-1ee7-4226-a51a-78a1f1b5bd8a) that could disclose sensitive information to attackers, leading to Denial of Service and Cross-Site attacks.  
  
## <a name="rule-description"></a>Rule Description  
 [XSLT](http://msdn.microsoft.com/en-us/6377ce5f-3c45-42a6-b7a9-ec8da588b60c) is a World Wide Web Consortium (W3C) standard for transforming XML data. XSLT is typically used to write style sheets to transform XML data to other formats such as HTML, fixed length text, comma-separated text, or a different XML format. Although prohibited by default, you may choose to enable it for your project.  
  
 To ensure you're not exposing an attack surface, this rule triggers whenever the XslCompiledTransform.<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> receives insecure combination instances of <xref:System.Xml.Xsl.XsltSettings> and <xref:System.Xml.XmlResolver>, which allows malicious script processing.  
  
## <a name="how-to-fix-violations"></a>How to Fix Violations  
  
-   Replace the insecure XsltSettings argument with XsltSettings.<xref:System.Xml.Xsl.XsltSettings.Default%2A> or with an instance that has disabled document function and script execution.  
  
-   Replace the <xref:System.Xml.XmlResolver> argument with null or an <xref:System.Xml.XmlSecureResolver> instance.  
  
## <a name="when-to-suppress-warnings"></a>When to Suppress Warnings  
 Unless you're sure that the input is known to be from a trusted source, do not suppress a rule from this warning.  
  
## <a name="pseudo-code-examples"></a>Pseudo-code Examples  
  
### <a name="violation"></a>Violation  
  
```csharp  
using System.Xml;  
using System.Xml.Xsl;  
  
namespace TestNamespace   
{   
    class TestClass   
    {  
         void TestMethod()   
        {    
             XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();   
             var settings = XsltSettings.TrustedXslt;   
             var resolver = new XmlUrlResolver();   
             xslCompiledTransform.Load("testStylesheet", settings, resolver); // warn   
        }  
    }   
}   
```  
  
### <a name="solution"></a>Solution  
  
```csharp  
using System.Xml;   
using System.Xml.Xsl;   
  
namespace TestNamespace   
{   
    class TestClass   
    {   
        void TestMethod()   
        {   
            XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();   
            var settings = XsltSettings.Default;   
            var resolver = new XmlUrlResolver();   
            xslCompiledTransform.Load("testStylesheet", settings, resolver);   
        }   
    }   
}  
```  
  
### <a name="violation"></a>Violation  
  
```csharp  
using System.Xml;   
using System.Xml.Xsl;   
  
namespace TestNamespace   
{   
    class TestClass   
    {   
        private static void TestMethod(XsltSettings settings)   
        {   
            try   
            {   
                XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();   
                var resolver = new XmlUrlResolver();   
                xslCompiledTransform.Load("testStylesheet", settings, resolver); // warn   
            }   
            catch { throw; }   
            finally { }   
        }   
    }   
}  
```  
  
### <a name="solution"></a>Solution  
  
```csharp  
using System.Xml;   
using System.Xml.Xsl;   
  
namespace TestNamespace   
{   
    class TestClass   
    {   
        private static void TestMethod(XsltSettings settings)   
        {   
            try   
            {   
                XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();   
                settings.EnableDocumentFunction = false;   
                settings.EnableScript = false;   
                var resolver = new XmlUrlResolver();   
                xslCompiledTransform.Load("testStylesheet", settings, resolver);   
            }   
            catch { throw; }   
            finally { }   
        }   
    }   
}  
```
