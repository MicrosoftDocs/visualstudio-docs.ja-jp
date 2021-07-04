---
title: T4 パラメーター ディレクティブ
description: Visual Studio では、パラメーター ディレクティブは、外部コンテキストから渡された値から初期化されるテンプレート コード内のプロパティを宣言します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8ef80179d43996669b9d883fd2ca9163208d18d7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386099"
---
# <a name="t4-parameter-directive"></a>T4 パラメーター ディレクティブ

Visual Studio テキスト テンプレートでは、`parameter` ディレクティブは、外部コンテキストから渡された値から初期化されるテンプレート コード内のプロパティを宣言します。 テキスト変換を呼び出すコードを記述する場合は、これらの値を設定できます。

## <a name="using-the-parameter-directive"></a>パラメーター ディレクティブを使用する

```
<#@ parameter type="Full.TypeName" name="ParameterName" #>
```

 `parameter` ディレクティブでは、外部コンテキストから渡された値から初期化されるテンプレート コード内のプロパティを宣言します。 テキスト変換を呼び出すコードを記述する場合は、これらの値を設定できます。 値は、`Session` ディクショナリまたは <xref:System.Runtime.Remoting.Messaging.CallContext> で渡すことができます。

 任意のリモート処理が可能な型のパラメーターを宣言できます。 つまり、<xref:System.SerializableAttribute> を使用して型を宣言するか、<xref:System.MarshalByRefObject> から型を派生する必要があります。 これにより、テンプレートが処理される AppDomain にパラメーター値を渡すことができます。

 たとえば、次の内容を含むテキスト テンプレートを作成できます。

```
<#@ template language="C#" #>

<#@ parameter type="System.Int32" name="TimesToRepeat" #>

<# for (int i = 0; i < TimesToRepeat; i++) { #>
Line <#= i #>
<# } #>
```

## <a name="passing-parameter-values-to-a-template"></a>テンプレートにパラメーター値を渡す
 メニュー コマンドやイベント ハンドラーなどの Visual Studio 拡張機能を作成する場合は、テキスト テンプレート サービスを使用してテンプレートを処理できます。

```csharp
// Get a service provider - how you do this depends on the context:
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

## <a name="passing-values-in-the-call-context"></a>呼び出しコンテキスト内の値を渡す
 別の方法として、<xref:System.Runtime.Remoting.Messaging.CallContext> の論理データとして値を渡すこともできます。

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

## <a name="passing-values-to-a-run-time-preprocessed-text-template"></a>実行時 (前処理された) テキスト テンプレートに値を渡す
 通常、実行時 (前処理された) テキスト テンプレートでは、`<#@parameter#>` ディレクティブを使用する必要はありません。 代わりに、生成されたコードの追加のコンストラクターまたは設定可能なプロパティを定義して、パラメーター値を渡すことができます。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

 ただし、`<#@parameter>` を実行時テンプレートで使用する場合は、Session ディクショナリを使用して値を渡すことができます。 例として、`PreTextTemplate1` という前処理されたテンプレートとしてファイルを作成したとします。 次のコードを使用して、プログラムでテンプレートを呼び出すことができます。

```csharp
PreTextTemplate1 t = new PreTextTemplate1();
t.Session = new Microsoft.VisualStudio.TextTemplating.TextTemplatingSession();
t.Session["TimesToRepeat"] = 5;
// Add other parameter values to t.Session here.
t.Initialize(); // Must call this to transfer values.
string resultText = t.TransformText();
```

## <a name="obtaining-arguments-from-texttemplateexe"></a>TextTemplate.exe から引数を取得する

> [!IMPORTANT]
> `parameter` ディレクティブでは、`TextTransform.exe` ユーティリティの `-a` パラメーターに設定された値は取得されません。 これらの値を取得するには、`template` ディレクティブで `hostSpecific="true"` を設定し、`this.Host.ResolveParameterValue("","","argName")` を使用します。
