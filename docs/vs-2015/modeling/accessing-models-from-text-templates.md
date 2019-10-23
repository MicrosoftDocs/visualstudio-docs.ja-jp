---
title: テキストテンプレートからのモデルへのアクセス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, accessing models
ms.assetid: cf65395a-0ca3-4826-89c7-b1869562685c
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d1dd414067e64552911c795da4d42cab20ce4d13
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655340"
---
# <a name="accessing-models-from-text-templates"></a>テキスト テンプレートからモデルへのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストテンプレートを使用すると、ドメイン固有の言語モデルに基づいたレポートファイル、ソースコードファイル、およびその他のテキストファイルを作成できます。 テキストテンプレートの基本的な情報については、「[コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。 テキストテンプレートは、DSL のデバッグ時に実験的モードで動作し、DSL を展開したコンピューター上でも動作します。

> [!NOTE]
> DSL ソリューションを作成すると、サンプルテキストテンプレート **\* .tt**ファイルがデバッグプロジェクトで生成されます。 ドメインクラスの名前を変更すると、これらのテンプレートは機能しなくなります。 それにもかかわらず、必要な基本ディレクティブが含まれており、DSL に一致するように更新できる例を提供しています。

 テキストテンプレートからモデルにアクセスするには:

- テンプレートディレクティブの inherit プロパティを[Modeflag Texttransformation](/previous-versions/bb893209(v=vs.140))に設定します。 これにより、ストアへのアクセスが提供されます。

- アクセスする DSL のディレクティブプロセッサを指定します。 これにより、テキストテンプレートのコード内でそのドメインクラス、プロパティ、および関係を使用できるように、DSL のアセンブリが読み込まれます。 また、指定したモデルファイルも読み込まれます。

  次の例のような `.tt` ファイルは、DSL 最小言語テンプレートから新しい [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションを作成するときに、デバッグプロジェクトで作成されます。

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

 このテンプレートについては、次の点に注意してください。

- このテンプレートでは、DSL 定義で定義したドメインクラス、プロパティ、およびリレーションシップを使用できます。

- このテンプレートは、`requires` プロパティに指定したモデルファイルを読み込みます。

- @No__t_0 のプロパティには、ルート要素が含まれています。 そこから、コードでモデルの他の要素に移動できます。 プロパティの名前は、通常、DSL のルートドメインクラスと同じです。 この例では、 `this.ExampleModel`です。

- コードフラグメントが記述されている言語はですC#が、任意の種類のテキストを生成できます。 または、プロパティ `language="VB"` を `template` ディレクティブに追加して、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] でコードを記述することもできます。

- テンプレートをデバッグするには、`template` ディレクティブに `debug="true"` を追加します。 このテンプレートは、例外が発生した場合に [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の別のインスタンスで開きます。 コード内の特定の位置でデバッガーを中断する場合は、ステートメントを挿入 `System.Diagnostics.Debugger.Break();`

     詳細については、「 [T4 テキストテンプレートのデバッグ](../modeling/debugging-a-t4-text-template.md)」を参照してください。

## <a name="about-the-dsl-directive-processor"></a>DSL ディレクティブプロセッサについて
 このテンプレートでは、DSL 定義で定義したドメインクラスを使用できます。 これは、通常、テンプレートの先頭付近に表示されるディレクティブによって取り込まれます。 前の例では、次のようになっています。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>
```

 ディレクティブの名前 (この例では `MyLanguage`) は、DSL の名前から取得されます。 これは、DSL の一部として生成される*ディレクティブプロセッサ*を呼び出します。 ソースコードは**Dsl\GeneratedCode\DirectiveProcessor.cs**で見つけることができます。

 DSL ディレクティブプロセッサは、次の2つの主要タスクを実行します。

- これは、DSL を参照するテンプレートにアセンブリとインポートディレクティブを効果的に挿入します。 これにより、テンプレートコードでドメインクラスを使用できるようになります。

- @No__t_0 パラメーターに指定したファイルが読み込まれ、読み込まれたモデルのルート要素を参照する `this` のプロパティが設定されます。

## <a name="validating-the-model-before-running-the-template"></a>テンプレートを実行する前にモデルを検証しています
 テンプレートが実行される前にモデルが検証されるようにすることができます。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1';validation='open|load|save|menu'" #>

```

 以下の点に注意してください。

1. @No__t_0 パラメーターと `validation` パラメーターは ";" で区切られており、その他の区切り記号やスペースは使用できません。

2. 検証カテゴリの一覧によって、実行される検証メソッドが決まります。 複数のカテゴリは "&#124;" で区切る必要があり、その他の区切り記号やスペースは使用できません。

   エラーが見つかった場合は、[エラー] ウィンドウに報告され、結果ファイルにはエラーメッセージが含まれます。

## <a name="Multiple"></a>テキストテンプレートからの複数のモデルへのアクセス

> [!NOTE]
> このメソッドを使用すると、同じテンプレート内の複数のモデルを読み取ることができますが、ModelBus 参照はサポートされません。 ModelBus 参照によって interlinked されるモデルを読み取る方法については、「[テキストテンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)」を参照してください。

 同じテキストテンプレートから複数のモデルにアクセスする場合は、生成されたディレクティブプロセッサをモデルごとに1回呼び出す必要があります。 @No__t_0 パラメーターには、各モデルのファイル名を指定する必要があります。 @No__t_0 パラメーターで、ルートドメインクラスに使用する名前を指定する必要があります。 各ディレクティブ呼び出しの `provides` パラメーターには、異なる値を指定する必要があります。 たとえば、Library という名前の3つのモデルファイルがあるとします。これは、"xyz"、"School"、"xyz" という名前です。 同じテキストテンプレートからアクセスするには、次のような3つのディレクティブ呼び出しを記述する必要があります。

```
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Library.xyz'" provides="ExampleModel=LibraryModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='School.xyz'" provides="ExampleModel=SchoolModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Work.xyz'" provides="ExampleModel=WorkModel" #>
```

> [!NOTE]
> このコード例は、最小言語ソリューションテンプレートに基づく言語を対象としています。

 テキストテンプレート内のモデルにアクセスするために、次の例のコードのようなコードを記述できるようになりました。

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
 読み込むモデルを実行時に決定する場合は、DSL 固有のディレクティブを使用するのではなく、プログラムコードでモデルファイルを動的に読み込むことができます。

 ただし、dsl 固有のディレクティブの機能の1つとして、dsl 名前空間をインポートして、その DSL で定義されているドメインクラスをテンプレートコードで使用できるようにします。 ディレクティブを使用していないため、読み込む可能性のあるすべてのモデルに対して、 **\<assembly >** と **\<import >** ディレクティブを追加する必要があります。 読み込む可能性のあるさまざまなモデルが同じ DSL のすべてのインスタンスである場合、これは簡単です。

 ファイルを読み込むには、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus を使用する方法が最も効果的です。 一般的なシナリオでは、テキストテンプレートは DSL 固有のディレクティブを使用して、通常の方法で最初のモデルを読み込みます。 このモデルには、別のモデルへの ModelBus 参照が含まれます。 ModelBus を使用して、参照先のモデルを開き、特定の要素にアクセスできます。 詳細については、「[テキストテンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)」を参照してください。

 あまり一般的ではないシナリオでは、ファイル名のみが存在し、現在の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトに含まれていないモデルファイルを開くことができます。 この場合、「[方法: プログラムコードでファイルからモデルを開く](../modeling/how-to-open-a-model-from-file-in-program-code.md)」で説明されている方法を使用してファイルを開くことができます。

## <a name="generating-multiple-files-from-a-template"></a>テンプレートから複数のファイルを生成する
 複数のファイルを生成する場合は (たとえば、モデル内の要素ごとに個別のファイルを生成する場合)、いくつかの方法が考えられます。 既定では、各テンプレートファイルから生成されるファイルは1つだけです。

### <a name="splitting-a-long-file"></a>長いファイルの分割
 このメソッドでは、テンプレートを使用して、区切り記号で区切られた1つのファイルを生成します。 次に、ファイルをその部分に分割します。 2つのテンプレートがあります。1つは1つのファイルを生成するテンプレート、もう1つは分割するテンプレートです。

 **LoopTemplate**は、長い単一ファイルを生成します。 **[すべてのテンプレートの変換]** をクリックしても直接処理されないため、ファイル拡張子が "t4" であることに注意してください。 このテンプレートは、セグメントを区切る区切り記号文字列を指定するパラメーターを受け取ります。

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

 `LoopSplitter.tt` は `LoopTemplate.t4` を呼び出し、結果として得られたファイルをそのセグメントに分割します。 このテンプレートはモデルを読み取れないため、モデリングテンプレートである必要はありません。

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
