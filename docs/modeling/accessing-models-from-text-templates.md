---
title: テキスト テンプレートからモデルへのアクセス
description: テキスト テンプレートを使用して、ドメイン固有の言語モデルに基づくレポート ファイル、ソース コード ファイル、およびその他のテキスト ファイルを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, accessing models
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 05e21dacfe56f41f1d2c0da51659ab55203db1a0
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389164"
---
# <a name="access-models-from-text-templates"></a>テキスト テンプレートからモデルにアクセスする

テキスト テンプレートを使用して、ドメイン固有の言語モデルに基づくレポート ファイル、ソース コード ファイル、およびその他のテキスト ファイルを作成できます。 テキスト テンプレートに関する基本情報については、「[コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。 テキスト テンプレートは、DSL のデバッグ時に実験モードで動作し、DSL を展開したコンピューター上でも動作します。

> [!NOTE]
> DSL ソリューションを作成すると、サンプル テキスト テンプレートの **\*.tt** ファイルがデバッグ プロジェクトに生成されます。 ドメイン クラスの名前を変更すると、これらのテンプレートは機能しなくなります。 それにもかかわらず、これらには必要な基本ディレクティブが含まれており、DSL に一致するように更新できる例が提供されます。

 テキスト テンプレートからモデルにアクセスするには:

- テンプレート ディレクティブの inherit プロパティを [Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation](/previous-versions/bb893209(v=vs.140)) に設定します。 これにより、ストアへのアクセスが提供されます。

- アクセスする DSL のディレクティブ プロセッサを指定します。 これにより、テキスト テンプレートのコード内でそのドメイン クラス、プロパティ、およびリレーションシップを使用できるように、DSL のアセンブリが読み込まれます。 また、指定したモデル ファイルも読み込まれます。

  DSL の最小言語のテンプレートから新しい Visual Studio ソリューションを作成すると、次の例のような `.tt` ファイルが、デバッグ プロジェクト内に作成されます。

```
<#@ template inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ output extension=".txt" #>
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>

This text will be output directly.

This is the name of the model: <#= this.ModelRoot.Name #>

Here is a list of elements in the model:
<#
  // When you change the DSL Definition, some of the code below may not work.
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {#>
<#= element.Name #>
<#
  }
#>
```

 このテンプレートについては、次の点に注目してください。

- このテンプレートでは、DSL 定義で定義したドメイン クラス、プロパティ、およびリレーションシップを使用できます。

- このテンプレートでは、`requires` プロパティで指定したモデル ファイルが読み込まれます。

- `this` のプロパティには、ルート要素が含まれています。 そこから、コードでモデルの他の要素に移動できます。 プロパティの名前は、通常、DSL のルート ドメイン クラスと同じです。 この例では `this.ExampleModel` です。

- このコード フラグメントが記述されている言語は C# ですが、任意の種類のテキストを生成することができます。 `language="VB"` プロパティを `template` ディレクティブに追加することで、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] にコードを記述することもできます。

- テンプレートをデバッグするには、`debug="true"` を `template` ディレクティブに追加します。 例外が発生した場合、テンプレートは Visual Studio の別のインスタンスで開きます。 コード内の特定の位置でデバッガーを中断する場合は、`System.Diagnostics.Debugger.Break();` ステートメントを挿入します。

   詳細については、「[T4 テキスト テンプレートのデバッグ](../modeling/debugging-a-t4-text-template.md)」を参照してください。

## <a name="about-the-dsl-directive-processor"></a>DSL ディレクティブ プロセッサについて
 このテンプレートでは、DSL 定義で定義したドメイン クラスを使用できます。 これは、通常、テンプレートの先頭付近に表示されるディレクティブによって取り込まれます。 前の例では、次のようになっています。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>
```

 ディレクティブの名前 (この例では `MyLanguage`) は、DSL の名前から派生します。 DSL の一部として生成される "*ディレクティブ プロセッサ*" が呼び出されます。 ソース コードは **Dsl\GeneratedCode\DirectiveProcessor.cs** で見つけることができます。

 DSL ディレクティブ プロセッサは、次の 2 つの主要タスクを実行します。

- DSL を参照するテンプレートにアセンブリとインポート ディレクティブを効果的に挿入します。 これにより、テンプレート コードでドメイン クラスを使用できるようになります。

- `requires` パラメーターで指定されたファイルを読み込み、読み込んだモデルのルート要素を参照するプロパティを `this` に設定します。

## <a name="validating-the-model-before-running-the-template"></a>テンプレートを実行する前のモデルの検証
 テンプレートが実行される前にモデルが検証されるようにすることができます。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1';validation='open|load|save|menu'" #>
```

 次のことに注意してください。

1. `filename` パラメーターと `validation` パラメーターは ";" で区切られ、その他の区切り記号または空白文字は使用できません。

2. 検証カテゴリの一覧によって、実行される検証メソッドが決まります。 複数のカテゴリは "&#124;" で区切る必要があり、その他の区切り記号やスペースは使用できません。

   エラーが見つかった場合は、[エラー] ウィンドウに報告され、結果ファイルにはエラー メッセージが含まれます。

## <a name="accessing-multiple-models-from-a-text-template"></a><a name="Multiple"></a> テキスト テンプレートからの複数のモデルへのアクセス

> [!NOTE]
> この方法では、同じテンプレート内の複数のモデルを読み取ることができますが、ModelBus 参照はサポートされません。 ModelBus 参照によって連結されているモデルを読み取る方法については、「[テキスト テンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)」を参照してください。

 同じテキスト テンプレートから複数のモデルにアクセスする場合は、生成されたディレクティブ プロセッサをモデルごとに 1 回呼び出す必要があります。 `requires` パラメーターに、各モデルのファイル名を指定する必要があります。 `provides` パラメーターに、ルート ドメイン クラスに使用する名前を指定する必要があります。 各ディレクティブ呼び出しの `provides` パラメーターに、異なる値を指定する必要があります。 たとえば、Library.xyz、School.xyz、Work.xyz という 3 つのモデル ファイルがあるとします。 同じテキスト テンプレートからそれらにアクセスするには、次のような 3 つのディレクティブ呼び出しを記述する必要があります。

```
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Library.xyz'" provides="ExampleModel=LibraryModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='School.xyz'" provides="ExampleModel=SchoolModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Work.xyz'" provides="ExampleModel=WorkModel" #>
```

> [!NOTE]
> このコード例は、最小言語ソリューション テンプレートに基づく言語を対象としています。

 テキスト テンプレート内のモデルにアクセスするために、次の例のようなコードを記述できるようになりました。

```csharp
<#
foreach (ExampleElement element in this.LibraryModel.Elements)
...
foreach (ExampleElement element in this.SchoolModel.Elements)
...
foreach (ExampleElement element in this.WorkModel.Elements)
...
#>
```

```vb
<#
For Each element As ExampleElement In Me.LibraryModel.Elements
...
For Each element As ExampleElement In Me.SchoolModel.Elements
...
For Each element As ExampleElement In Me.WorkModel.Elements
...
#>
```

## <a name="loading-models-dynamically"></a>モデルの動的な読み込み
 読み込むモデルを実行時に決定する場合は、DSL 固有のディレクティブを使用するのではなく、プログラム コードでモデル ファイルを動的に読み込むことができます。

 ただし、DSL 固有のディレクティブの機能の 1 つとして、DSL 名前空間のインポートがあり、これにより、その DSL で定義されているドメイン クラスをテンプレート コードで使用できます。 ディレクティブを使用していないため、読み込む可能性のあるすべてのモデルに **\<assembly>** ディレクティブと **\<import>** ディレクティブを追加する必要があります。 読み込む可能性のあるさまざまなモデルが同じ DSL のすべてのインスタンスである場合、これは簡単です。

 ファイルを読み込むには、最も効果的な方法は Visual Studio ModelBus を使用することです。 一般的なシナリオでは、テキスト テンプレートで DSL 固有のディレクティブを使用して、通常の方法で最初のモデルを読み込みます。 そのモデルには、別のモデルへの ModelBus 参照が含まれます。 ModelBus を使用して、参照先のモデルを開き、特定の要素にアクセスできます。 詳細については、「[テキスト テンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)」を参照してください。

 あまり一般的ではないシナリオでは、ファイル名のみが存在し、現在の Visual Studio プロジェクトには含まれていないモデル ファイルを開くことが必要になる場合があります。 この場合、「[方法: プログラム コードでファイルからモデルを開く](../modeling/how-to-open-a-model-from-file-in-program-code.md)」で説明されている方法を使用してファイルを開くことができます。

## <a name="generating-multiple-files-from-a-template"></a>テンプレートからの複数のファイルの生成
 複数のファイルを生成する場合 (たとえば、モデル内の要素ごとに個別のファイルを生成する場合)、いくつかの方法が考えられます。 既定では、各テンプレート ファイルから生成されるファイルは 1 つだけです。

### <a name="splitting-a-long-file"></a>長いファイルの分割
 この方法では、テンプレートを使用して、区切り記号で区切られた単一のファイルを生成します。 次に、そのファイルを部分に分割します。 2 つのテンプレートがあります。1 つは単一のファイルを生成するテンプレート、もう 1 つはそれを分割するテンプレートです。

 **LoopTemplate.t4** では、長い単一ファイルが生成されます。 ファイル拡張子が ".t4" であることに注意してください。これは、 **[すべてのテンプレートの変換]** をクリックしても直接処理されることはないためです。 このテンプレートは、セグメントを区切る区切り記号文字列を指定するパラメーターを受け取ります。

```
<#@ template ninherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ parameter name="delimiter" type="System.String" #>
<#@ output extension=".txt" #>
<#@ MyDSL processor="MyDSLDirectiveProcessor" requires="fileName='SampleModel.mydsl1';validation='open|load|save|menu'" #>
<#
  // Create a file segment for each element:
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {
    // First item is the delimiter:
#>
<#= string.Format(delimiter, element.Id) #>

   Element: <#= element.Name #>
<#
   // Here you generate more content derived from the element.
  }
#>
```

 `LoopSplitter.tt` によって `LoopTemplate.t4` が呼び出され、生成されたファイルがセグメントに分割されます。 このテンプレートはモデルを読み取らないため、モデリング テンプレートである必要はありません。

```
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<#@ import namespace="System.Runtime.Remoting.Messaging" #>
<#@ import namespace="System.IO" #>

<#
  // Get the local path:
  string itemTemplatePath = this.Host.ResolvePath("LoopTemplate.t4");
  string dir = Path.GetDirectoryName(itemTemplatePath);

  // Get the template for generating each file:
  string loopTemplate = File.ReadAllText(itemTemplatePath);

  Engine engine = new Engine();

  // Pass parameter to new template:
  string delimiterGuid = Guid.NewGuid().ToString();
  string delimiter = "::::" + delimiterGuid + ":::";
  CallContext.LogicalSetData("delimiter", delimiter + "{0}:::");
  string joinedFiles = engine.ProcessTemplate(loopTemplate, this.Host);

  string [] separateFiles = joinedFiles.Split(new string [] {delimiter}, StringSplitOptions.None);

  foreach (string nameAndFile in separateFiles)
  {
     if (string.IsNullOrWhiteSpace(nameAndFile)) continue;
     string[] parts = nameAndFile.Split(new string[]{":::"}, 2, StringSplitOptions.None);
     if (parts.Length < 2) continue;
#>
 Generate: [<#= dir #>] [<#= parts[0] #>]
<#
     // Generate a file from this item:
     File.WriteAllText(Path.Combine(dir, parts[0] + ".txt"), parts[1]);
  }
#>
```
