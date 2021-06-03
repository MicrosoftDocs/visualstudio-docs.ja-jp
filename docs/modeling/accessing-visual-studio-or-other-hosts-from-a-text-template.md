---
title: テキスト テンプレートから Visual Studio またはその他のホストへのアクセス
description: テンプレートを実行するホストによって公開されているテキスト テンプレートで、メソッドとプロパティを使用する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ce008d0a14cbd75cf8a46599ff67bd9e799ee8ce
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908875"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>テキスト テンプレートから Visual Studio またはその他のホストにアクセスする

テキスト テンプレートでは、テンプレートを実行するホストによって公開されているメソッドとプロパティを使用できます。 ホストの 1 つの例が、Visual Studio です。

> [!NOTE]
> ホスト メソッドとプロパティは、通常のテキスト テンプレートでは使用できますが、*前処理された* テキスト テンプレートでは使用できません。

## <a name="obtain-access-to-the-host"></a>ホストへのアクセスを取得する

ホストにアクセスするには、`template` ディレクティブで `hostspecific="true"` を設定します。 これで、型 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) を持つ `this.Host` を使用できるようになりました。 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) 型には、たとえばファイル名を解決し、エラーをログするために使用できるメンバーがあります。

### <a name="resolve-file-names"></a>ファイル名を解決する

テキスト テンプレートを基準としたファイルの完全なパスを検索するには、`this.Host.ResolvePath()` を使用します。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>
```

### <a name="display-error-messages"></a>エラー メッセージを表示する

この例では、テンプレートを変換するときにメッセージをログします。 ホストが Visual Studio の場合は、エラーが **エラー一覧** に追加されます。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.CodeDom.Compiler" #>
<#
  string message = "test message";
  this.Host.LogErrors(new CompilerErrorCollection()
    { new CompilerError(
       this.Host.TemplateFile, // Identify the source of the error.
       0, 0, "0",   // Line, column, error ID.
       message) }); // Message displayed in error window.
#>
```

## <a name="use-the-visual-studio-api"></a>Visual Studio API を使用する

Visual Studio でテキスト テンプレートを実行している場合は、`this.Host` を使用して、Visual studio によって提供されるサービスと読み込まれたあらゆるパッケージまたは拡張機能にアクセスできます。

hostspecific="true" に設定し、`this.Host` を <xref:System.IServiceProvider> にキャストします。

この例では、Visual Studio API、<xref:EnvDTE.DTE> をサービスとして取得します。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#
 IServiceProvider serviceProvider = (IServiceProvider)this.Host;
 DTE dte = serviceProvider.GetService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>
```

## <a name="use-hostspecific-with-template-inheritance"></a>テンプレートの継承で hostSpecific を使用する

`inherits` 属性も使用し、`hostspecific="true"` を指定するテンプレートから継承する場合は `hostspecific="trueFromBase"` を指定します。 そうしないと、プロパティ `Host` が 2 回宣言されていることを示すコンパイラの警告が表示されることがあります。
