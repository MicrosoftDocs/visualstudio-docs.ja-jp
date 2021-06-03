---
title: T4 テンプレート ディレクティブ
description: 通常、Visual Studio の T4 テキスト テンプレートは、テンプレートの処理方法を指定する template ディレクティブで始まります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ccb5a216aa9a43581327b04d4b6b56f49f9b2bae
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924648"
---
# <a name="t4-template-directive"></a>T4 テンプレート ディレクティブ

通常、Visual Studio の T4 テキスト テンプレートは、テンプレートの処理方法を指定する `template` ディレクティブで始まります。 テキスト テンプレートおよびそれに含まれるファイルには、template ディレクティブを 1 つしか含めることができません。

テキスト テンプレートの作成方法の概要については、「[T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

## <a name="using-the-template-directive"></a>template ディレクティブの使用

```
<#@ template [language="VB"] [compilerOptions="options"] [culture="code"] [debug="true"] [hostspecific="true"] [inherits="templateBaseClass"] [visibility="internal"] [linePragmas="false"] #>
```

`template` ディレクティブには、変換のさまざまな側面を指定できる属性がいくつかあります。 属性はすべて省略可能です。

## <a name="compileroptions-attribute"></a>compilerOptions 属性

例:

`compilerOptions="optimize+"`

有効な値:

有効なコンパイラ オプション。

実行時 (前処理された) テンプレートでは無視されます。

テンプレートが [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] または [!INCLUDE[vb_current_short](../debugger/includes/vb_current_short_md.md)] に変換されている場合にこれらのオプションが適用され、生成されたコードがコンパイルされます。

## <a name="culture-attribute"></a>culture 属性

例:

`culture="de-CH"`

有効な値:

インバリアント カルチャである "" (既定値)。

xx-XX 形式の文字列で表現されたカルチャ。 たとえば、en-US、ja-JP、de-CH、de-DE などがあります。 詳細については、「<xref:System.Globalization.CultureInfo?displayProperty=fullName>」を参照してください。

culture 属性では、式ブロックをテキストに変換する際に使用するカルチャを指定します。

## <a name="debug-attribute"></a>debug 属性

例:

```
debug="true"
```

有効な値:

`true`

`false` (既定)

`debug` 属性が `true` の場合、デバッガーでテンプレート内の中断または例外の発生位置を正確に特定できるようにする情報が中間コード ファイルに出力されるようになります。

デザイン時テンプレートの場合、中間コード ファイルは **%TEMP%** ディレクトリに書き込まれます。

デバッガーでデザイン時テンプレートを実行するには、テキスト テンプレートを保存し、ソリューション エクスプローラーでテキスト テンプレートのショートカット メニューを開き、 **[T4 テンプレートのデバッグ]** をクリックします。

## <a name="hostspecific-attribute"></a>hostspecific 属性

例:

```
hostspecific="true"
```

有効な値:

`true`

`false` (既定)

`trueFromBase`

この属性の値を `true` に設定した場合、テキスト テンプレートによって生成されたクラスに、`Host` というプロパティが追加されます。 このプロパティは変換エンジンのホストへの参照であり、[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) として宣言されます。 カスタム ホストを定義している場合は、そのカスタム ホストの型にキャストできます。

このプロパティの型はホストの型に依存するため、特定のホストとのみ連携するテキスト テンプレートを作成している場合以外、利用価値はありません。 これは[デザイン時テンプレート](../modeling/design-time-code-generation-by-using-t4-text-templates.md)には当てはまりますが、[実行時テンプレート](../modeling/run-time-text-generation-with-t4-text-templates.md)には当てはまりません。

`hostspecific` が `true` であるときに Visual Studio を使用している場合は、`this.Host` を IServiceProvider にキャストして Visual Studio の機能にアクセスできます。 また、`Host.ResolvePath(filename)` を使用して、プロジェクトのファイルの絶対パスを取得することもできます。 次に例を示します。

```csharp
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#@ import namespace="System.IO" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<# // Get the Visual Studio API as a service:
 DTE dte = ((IServiceProvider)this.Host).GetCOMService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>

<#
 // Find a path within the current project:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>
```

`inherits` 属性と `hostspecific` 属性を一緒に使用する場合は、派生クラスで host="trueFromBase"、基底クラスで host="true" を指定します。 これで、生成されるコードで `Host` プロパティの定義が重複することを回避できます。

## <a name="language-attribute"></a>language 属性

例:

`language="VB"`

有効な値:

`C#` (既定)

`VB`

`language` 属性では、ステートメントおよび式ブロック内のソース コードに使用する言語 ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] または [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]) を指定します。 出力の生成元である中間コード ファイルでこの言語が使用されます。 この言語はテンプレートで生成される言語とは無関係であり、どのような種類のテキストであってもかまいません。

次に例を示します。

```vb
<#@ template language="VB" #>
<#@ output extension=".txt" #>
Squares of numbers:
<#
  Dim number As Integer
  For number = 1 To 4
#>
  Square of <#= number #> is <#= number * number #>
<#
  Next number
#>
```

## <a name="inherits-attribute"></a>inherits 属性

テンプレートのプログラム コードを別のクラスから継承できることを指定できます。クラスは、テキスト テンプレートから生成することもできます。

### <a name="inheritance-in-a-run-time-preprocessed-text-template"></a>実行時 (前処理された) テキスト テンプレートでの継承

実行時テキスト テンプレート間で継承を使用して、複数の派生バリアントを含む基本テンプレートを作成できます。 実行時テンプレートは、 **[カスタム ツール]** プロパティが **TextTemplatingFilePreprocessor** に設定されているテンプレートです。 実行時テンプレートでは、そのテンプレートに定義されているテキストを作成するために、アプリケーションで呼び出すことができるコードが生成されます。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

`inherits` 属性を指定しない場合は、テキスト テンプレートから基底クラスと派生クラスが生成されます。 `inherits` 属性を指定すると、派生クラスだけが生成されます。 基底クラスは手動で作成できますが、派生クラスで使用するメソッドを提供する必要があります。

通常は、前処理された別のテンプレートを基底クラスとして指定します。 基本テンプレートでは、派生テンプレートのテキストとインタリーブできる共通のテキスト ブロックを提供します。 クラス機能ブロック (`<#+ ... #>`) を使用して、テキスト フラグメントを含むメソッドを定義できます。 たとえば、基本テンプレートに出力テキストのフレームワークを配置し、派生テンプレートでオーバーライドできる仮想メソッドを提供することができます。

実行時 (前処理された) テキスト テンプレートの BaseTemplate.tt:

```scr
This is the common header.
<#
  SpecificFragment1();
#>
A common central text.
<#
  SpecificFragment2();
#>
This is the common footer.
<#+
  // Declare abstract methods
  protected virtual void SpecificFragment1() { }
  protected virtual void SpecificFragment2() { }
#>
```

実行時 (前処理された) テキスト テンプレートの DerivedTemplate1.tt:

```csharp
<#@ template language="C#" inherits="BaseTemplate" #>
<#
  // Run the base template:
  base.TransformText();
#>
<#+
// Provide fragments specific to this derived template:
protected override void SpecificFragment1()
{
#>
   Fragment 1 for DerivedTemplate1
<#+
}
protected override void SpecificFragment2()
{
#>
   Fragment 2 for DerivedTemplate1
<#+
}
#>
```

DerivedTemplate1 を呼び出すアプリケーション コード:

```csharp
Console.WriteLine(new DerivedTemplate().TransformText());
```

結果の出力:

```
This is the common header.
   Fragment 1 for DerivedTemplate1
A common central text.
   Fragment 2 for DerivedTemplate1
This is the common footer.
```

さまざまなプロジェクトの基底クラスと派生クラスを作成できます。 派生プロジェクトの参照に基本プロジェクトまたは基本アセンブリを追加することを忘れないでください。

手動で作成した通常のクラスを基底クラスとして使用することもできます。 基底クラスでは、派生クラスで使用するメソッドを提供する必要があります。

> [!WARNING]
> `inherits` 属性と `hostspecific` 属性を一緒に使用する場合は、派生クラスで hostspecific="trueFromBase"、基底クラスで host="true" を指定します。 これで、生成されるコードで `Host` プロパティの定義が重複することを回避できます。

### <a name="inheritance-in-a-design-time-text-template"></a>デザイン時テキスト テンプレートでの継承

デザイン時テキスト テンプレートは、 **[カスタム ツール]** が **TextTemplatingFileGenerator** に設定されているファイルです。 このテンプレートでは、Visual Studio プロジェクトの一部となるコードまたはテキストの出力ファイルが生成されます。 出力ファイルを生成するために、テンプレートは、まず中間プログラム コード ファイルに変換されます。通常、このファイルは表示されません。 `inherits` 属性では、この中間コードの基底クラスを指定します。

デザイン時テキスト テンプレートの場合、<xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName> から派生した基底クラスを指定できます。 `<#@assembly#>` ディレクティブを使用して、基底クラスを含むアセンブリまたはプロジェクトを読み込みます。

詳細については、[Gareth Jones のブログに掲載されたテキスト テンプレートでの継承に関する記事](/archive/blogs/garethj/vs2010-sp1-t4-template-inheritance-part-i-sample-metadata)を参照してください。

## <a name="linepragmas-attribute"></a>linePragmas 属性

例:

`linePragmas="false"`

有効な値:

`true` (既定)

`false`

この属性を false に設定すると、生成されたコード内で行番号を識別するタグが削除されます。 つまり、コンパイラは生成されたコードの行番号を使用してエラーを報告します。このため、デバッグ時の選択肢が増えて、テキスト テンプレートをデバッグするか、それとも生成されたコードをデバッグするかを選択できます。

この属性は、プラグマの絶対ファイル名によってソース コード管理下で無駄なマージが発生している場合にも役立ちます。

## <a name="visibility-attribute"></a>visibility 属性

例:

`visibility="internal"`

有効な値:

`public` (既定)

`internal`

実行時テキスト テンプレートでは、これは生成されたクラスの可視性属性を設定します。 既定では、クラスはコードのパブリック API の一部ですが、`visibility="internal"` を設定すると、自分のコードだけがそのテキスト生成クラスを使用するようにできます。