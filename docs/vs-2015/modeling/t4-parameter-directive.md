---
title: T4 パラメーター ディレクティブ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 1d590387-1d9d-40a5-a72c-65fae7a8bdf3
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c7971dc3402a344a5318fd8415404e7a45ae8485
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58978234"
---
# <a name="t4-parameter-directive"></a>T4 パラメーター ディレクティブ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]テキスト テンプレートで、`parameter`ディレクティブがテンプレート コードの外部のコンテキストから渡された値から初期化されるプロパティを宣言します。 テキスト変換を呼び出すコードを記述する場合は、これらの値を設定できます。  
  
## <a name="using-the-parameter-directive"></a>パラメーター ディレクティブの使用  
  
```  
<#@ parameter type="Full.TypeName" name="ParameterName" #>  
```  
  
 `parameter`ディレクティブは、テンプレート コードの外部のコンテキストから渡された値により初期化されるプロパティを宣言します。 テキスト変換を呼び出すコードを記述する場合は、これらの値を設定できます。 値としては`Session`ディクショナリ、または <xref:System.Runtime.Remoting.Messaging.CallContext> のいずれかを渡すことができます。  
  
 任意のリモート処理可能な型のパラメーターを宣言することができます。 すなわち、型は <xref:System.SerializableAttribute> をもって宣言されるか、<xref:System.MarshalByRefObject> から派生する必要があります。 これにより、テンプレートを処理する AppDomain にパラメーターの値を渡すことが許されます。  
  
 たとえば、次の内容のテキスト テンプレートを記述できます。  
  
```  
<#@ template language="C#" #>  
  
<#@ parameter type="System.Int32" name="TimesToRepeat" #>  
  
<# for (int i = 0; i < TimesToRepeat; i++) { #>  
Line <#= i #>  
<# } #>  
  
```  
  
## <a name="passing-parameter-values-to-a-template"></a>テンプレートにパラメーター値を渡す  
 作成する場合、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]メニュー コマンドやイベント ハンドラーなどの拡張機能は、テキスト テンプレート サービスを使用してテンプレートを処理できます。  
  
```csharp  
// Get a service provider – how you do this depends on the context:  
IServiceProvider serviceProvider = dte; // or dslDiagram.Store, for example   
// Get the text template service:  
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;  
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;  
// Create a Session in which to pass parameters:  
host.Session = host.CreateSession();  
// Add parameter values to the Session:  
session["TimesToRepeat"] = 5;  
// Process a text template:  
string result = t4.ProcessTemplate("MyTemplateFile.t4",  
  System.IO.File.ReadAllText("MyTemplateFile.t4"));  
  
```  
  
## <a name="passing-values-in-the-call-context"></a>呼び出しコンテキストで値を渡す  
 <xref:System.Runtime.Remoting.Messaging.CallContext> 中で論理データとして値を渡すこともできます。  
  
 次の例では、両方のメソッドを使用して値を渡します。  
  
```csharp  
ITextTemplating t4 = this.Store.GetService(typeof(STextTemplating)) as ITextTemplating;  
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;  
host.Session = host.CreateSession();  
// Pass a value in Session:  
host.Session["p1"] = 32;  
// Pass another value in CallContext:  
System.Runtime.Remoting.Messaging.CallContext.LogicalSetData("p2", "test");  
  
// Process a small template inline:  
string result = t4.ProcessTemplate("",   
   "<#@parameter type=\"System.Int32\" name=\"p1\"#>"  
 + "<#@parameter type=\"System.String\" name=\"p2\"#>"  
 + "Test <#=p1#> <#=p2#>");  
  
// Result value is:  
//     Test 32 test  
  
```  
  
## <a name="passing-values-to-a-run-time-preprocessed-text-template"></a>ランタイム (前処理された) テキスト テンプレートに値を渡す  
 通常、ランタイム (前処理された) テキスト テンプレートで `<#@parameter#>`ディレクティブを使用する必要はありません。 代わりに、生成されたコードに対して追加のコンストラクターや設定可能なプロパティを定義し、パラメーターの値を渡すことができます。 詳細については、次を参照してください。 [T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)  
  
 ただし、ランタイムテンプレートで `<#@parameter>` を使用する場合、`Session`ディクショナリを使用して渡すこともできます。 例として、 `PreTextTemplate1` という名前の前処理済みテンプレートとしてファイルを作成したとします。 テンプレートは、次のコードを使用して、プログラムで呼び出すことができます。  
  
```csharp  
PreTextTemplate1 t = new PreTextTemplate1();  
t.Session = new Microsoft.VisualStudio.TextTemplating.TextTemplatingSession();  
t.Session["TimesToRepeat"] = 5;  
// Add other parameter values to t.Session here.  
t.Initialize(); // Must call this to transfer values.  
string resultText = t.TransformText();  
  
```  
  
## <a name="obtaining-arguments-from-texttemplateexe"></a>TextTemplate.exe から引数を取得します。  
  
> [!IMPORTANT]
>  `parameter`ディレクティブは、`TextTransform.exe`ユーティリティの`–a`のパラメーターで設定された値を取得できません。 これらの値を取得するには、`template`ディレクティブで、`hostSpecific="true"` を設定し、`this.Host.ResolveParameterValue("","","argName")` を使用します。
