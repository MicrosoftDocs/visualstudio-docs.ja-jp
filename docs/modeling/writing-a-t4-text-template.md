---
title: T4 テキスト テンプレートの作成
description: T4 テキスト テンプレートについて、およびディレクティブ、テキスト ブロック、コントロール ブロックを含むテキスト テンプレートを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, syntax
- text templates, guide
- text templates, functions that generate text
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8034e0d1df6410c842f7d93a4ee3023957904744
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388088"
---
# <a name="writing-a-t4-text-template"></a>T4 テキスト テンプレートの作成
テキスト テンプレートには、そのテンプレートから生成されるテキストが含まれます。 たとえば、Web ページを作成するテンプレートには、「\<html>...」および HTML ページを構成する他のすべての標準的なパーツが含まれます。 テンプレートには、プログラム コードのフラグメントである "*コントロール ブロック*" が挿入されます。 コントロール ブロックはさまざまな値を提供すると共に、テキストの一部を条件付きにしたり、繰り返したりできるようにします。

 この構造によって、テンプレートの作成が簡単になります。生成されるファイルのプロトタイプを最初に作成しておき、結果を変化させるコントロール ブロックは徐々に挿入するという手法を利用できるためです。

 テキスト テンプレートは次の要素から構成されます。

- **ディレクティブ**: テンプレートの処理方法を制御する要素。

- **テキスト ブロック**: 出力に直接コピーされるコンテンツ。

- **コントロール ブロック**: 変数値をテキストに挿入したり、テキストの条件付きの部分または繰り返し部分を制御したりするプログラム コード。

このトピックの例を試すには、「[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」で説明されているように、テンプレート ファイルにコピーします。 テンプレート ファイルの編集が終わったら、そのファイルを保存し、出力される **.txt** ファイルを調べてください。

## <a name="directives"></a>ディレクティブ
 テキスト テンプレート ディレクティブは、変換コードと出力ファイルの生成方法に関する一般的な指示をテキスト テンプレート エンジンに与えます。

 たとえば、次のディレクティブでは、出力ファイルに .txt という拡張子を付けるように指定しています。

```
<#@ output extension=".txt" #>
```

 ディレクティブの詳細については、「[T4 テキスト テンプレートのディレクティブ](../modeling/t4-text-template-directives.md)」を参照してください。

## <a name="text-blocks"></a>テキスト ブロック
 テキスト ブロックのテキストは、出力ファイルに直接挿入されます。 テキスト ブロックに特別な書式指定はありません。 たとえば、次のテキスト テンプレートからは、"Hello" という単語を含むテキスト ファイルが生成されます。

```
<#@ output extension=".txt" #>
Hello
```

## <a name="control-blocks"></a>コントロール ブロック
 コントロール ブロックは、テンプレートの変換に使用されるプログラム コードのセクションです。 既定の言語は C# ですが、次のディレクティブをファイルの先頭に記述すると、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] を使用できます。

```
<#@ template language="VB" #>
```

 コントロール ブロックでのコードの記述に使用する言語は、生成されるテキストの言語とは関係ありません。

### <a name="standard-control-blocks"></a>標準コントロール ブロック
 標準コントロール ブロックは、出力ファイルの一部を生成するプログラム コードのセクションです。

 テンプレート ファイルには、任意の数のテキスト ブロックと標準コントロール ブロックを混在させることができます。 ただし、コントロール ブロックを他のコントロール ブロックの内部に配置することはできません。 それぞれの標準コントロール ブロックは、`<# ... #>` という記号で区切られます。

 たとえば、次のコントロール ブロックとテキスト ブロックを使用した場合、出力ファイルには "0, 1, 2, 3, 4 Hello!" という行が含まれます。

```
<#
    for(int i = 0; i < 4; i++)
    {
        Write(i + ", ");
    }
    Write("4");
#> Hello!
```

 明示的な `Write()` ステートメントを使用する代わりに、インタリーブ テキストとインタリーブ コードを使用できます。 次の例では、"Hello!" が 4 回出力されます。

```
<#
    for(int i = 0; i < 4; i++)
    {
#>
Hello!
<#
    }
#>
```

 テキスト ブロックは、`Write();` ステートメントを使用できる場所であれば、どこにでも挿入できます。

> [!NOTE]
> ループや条件などの複合ステートメント内にテキスト ブロックを埋め込む場合は、テキスト ブロックを必ず中かっこ ({...}) で囲んでください。

### <a name="expression-control-blocks"></a>式コントロール ブロック
 式コントロール ブロックでは、式を評価して文字列に変換します。 出力ファイルにはその文字列が挿入されます。

 式コントロール ブロックは `<#= ... #>` という記号で区切られます。

 たとえば、次のコントロール ブロックを使用した場合、出力ファイルには "5" が含まれます。

```
<#= 2 + 3 #>
```

 先頭の記号として「<#=」の 3 つの文字が含まれています。

 式には、スコープ内の任意の変数を含めることができます。 たとえば、次のブロックでは、数値を含む複数の行が出力されます。

```
<#@ output extension=".txt" #>
<#
    for(int i = 0; i < 4; i++)
    {
#>
This is hello number <#= i+1 #>: Hello!
<#
    }
#>
```

### <a name="class-feature-control-blocks"></a>クラス機能コントロール ブロック
 クラス機能コントロール ブロックでは、メインの変換の対象から除外する、プロパティやメソッドなどのコードを定義します。 クラス機能ブロックは、ヘルパー関数でよく使用されます。  クラス機能ブロックは、複数のテキスト テンプレートで[インクルード](#Include)できるように、一般には独立したファイルに配置します。

 クラス機能コントロール ブロックは `<#+ ... #>` という記号で区切られます。

 たとえば、次のテンプレート ファイルでは、メソッドを宣言して使用しています。

```
<#@ output extension=".txt" #>
Squares:
<#
    for(int i = 0; i < 4; i++)
    {
#>
    The square of <#= i #> is <#= Square(i+1) #>.
<#
    }
#>
That is the end of the list.
<#+   // Start of class feature block
private int Square(int i)
{
    return i*i;
}
#>
```

 クラス機能は、それを記述するファイルの末尾に配置する必要があります。 ただし、`<#@include#>` を使用すると、`include` ディレクティブの後ろに標準ブロックとテキストが続く場合でも、クラス機能を含むファイルをインクルードすることができます。

 コントロール ブロックの詳細については、「[テキスト テンプレートのコントロール ブロック](../modeling/text-template-control-blocks.md)」を参照してください。

### <a name="class-feature-blocks-can-contain-text-blocks"></a>クラス機能ブロックにはテキスト ブロックを含めることができる
 テキストを生成するメソッドを記述できます。 次に例を示します。

```
List of Squares:
<#
   for(int i = 0; i < 4; i++)
   {  WriteSquareLine(i); }
#>
End of list.
<#+   // Class feature block
private void WriteSquareLine(int i)
{
#>
   The square of <#= i #> is <#= i*i #>.
<#+
}
#>
```

 テキストを生成するメソッドは、複数のテンプレートでインクルードできる独立したファイルに配置すると特に便利です。

## <a name="using-external-definitions"></a>外部定義の使用

### <a name="assemblies"></a>アセンブリ
 テンプレートのコード ブロックでは、最もよく使用される .NET アセンブリ (System.dll など) で定義されている型を使用できます。 さらに、他の .NET アセンブリや独自のアセンブリを参照することもできます。 パス名、つまりアセンブリの厳密な名前を指定できます。

```
<#@ assembly name="System.Xml" #>
```

 絶対パス名を使用するか、パス名で標準マクロ名を使用する必要があります。 次に例を示します。

```
<#@ assembly name="$(SolutionDir)library\MyAssembly.dll" #>
```

 assembly ディレクティブは、[前処理されたテキスト テンプレート](../modeling/run-time-text-generation-with-t4-text-templates.md)では無効です。

 詳細については、「[T4 アセンブリ ディレクティブ](../modeling/t4-assembly-directive.md)」を参照してください。

### <a name="namespaces"></a>名前空間
 import ディレクティブは、C# での `using` 句または Visual Basic での `imports` 句と同じ働きをします。 これを使用すると、完全修飾名を使用せずにコードで型を参照できます。

```
<#@ import namespace="System.Xml" #>
```

 `assembly` ディレクティブと `import` ディレクティブは、必要に応じていくつでも使用できます。 これらのディレクティブは、テキスト ブロックとコントロール ブロックの前に配置する必要があります。

 詳細については、「[T4 インポート ディレクティブ](../modeling/t4-import-directive.md)」を参照してください。

### <a name="including-code-and-text"></a><a name="Include"></a> コードとテキストのインクルード
 `include` ディレクティブを使用すると、別のテンプレート ファイルのテキストを挿入できます。 たとえば、次のディレクティブでは、`test.txt` のコンテンツが挿入されます。

```
<#@ include file="c:\test.txt" #>
```

 インクルードされたコンテンツは、インクルード先のテキスト テンプレートに元から含まれていた場合とほとんど同じように処理されます。 ただし、include ディレクティブの後に通常のテキスト ブロックと標準コントロール ブロックが続く場合でも、クラス機能ブロック (`<#+...#>`) を含むファイルをインクルードすることができます。

 詳細については、「[T4 インクルード ディレクティブ](../modeling/t4-include-directive.md)」を参照してください。

### <a name="utility-methods"></a>ユーティリティ メソッド
 `Write()` をはじめ、コントロール ブロックでいつでも使用できるメソッドがいくつかあります。 これには、出力のインデントに役立つメソッドや、エラーの報告に役立つメソッドが含まれます。

 独自のユーティリティ メソッドのセットを記述することもできます。

 詳細については、「[テキスト テンプレートのユーティリティ メソッド](../modeling/text-template-utility-methods.md)」を参照してください。

## <a name="transforming-data-and-models"></a>データとモデルの変換
 テキスト テンプレートが最も役に立つのは、モデル、データベース、データ ファイルなどのソースのコンテンツに基づいてマテリアルを生成する場合です。 テンプレートによってデータが抽出され、その書式が再設定されます。 テンプレートのコレクションでは、このようなソースを複数のファイルに変換できます。

 ソース ファイルを読み取る方法はいくつかあります。

 **テキスト テンプレートでファイルを読み取る**。 これは、テンプレートにデータを取り込む方法としては最も簡単です。

```
<#@ import namespace="System.IO" #>
<# string fileContent = File.ReadAllText(@"C:\myData.txt"); ...
```

 **ナビゲート可能なモデルとしてファイルを読み込む**。 より効果的な方法は、テキスト テンプレート コードでナビゲートできるモデルとしてデータを読み取ることです。 たとえば、XML ファイルを読み込み、XPath 式でそのファイル内をナビゲートできます。 [xsd.exe](/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe) を使用して、XML データの読み取りに使用できるクラスのセットを作成することもできます。

 **ダイアグラムまたはフォームでモデル ファイルを編集する。** [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]には、モデルをダイアグラムまたは Windows フォームとして編集できるツールが用意されています。 このため、生成されたアプリケーションのユーザーと、モデルについて効率的に話し合うことができます。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]では、モデルの構造を反映した、厳密に型指定されたクラスのセットも作成できます。 詳細については、「[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)」を参照してください。

### <a name="relative-file-paths-in-design-time-templates"></a>デザイン時テンプレートの相対ファイル パス
 [デザイン時テキスト テンプレート](../modeling/design-time-code-generation-by-using-t4-text-templates.md)で、テキスト テンプレートを基準とする場所にあるファイルを参照する場合は、`this.Host.ResolvePath()` を使用します。 また、`hostspecific="true"` ディレクティブで `template` を設定する必要もあります。

```
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of MyFile.txt is:
<#= myFile #>
```

ホストから提供される他のサービスを取得することもできます。 詳細については、[テンプレートから Visual Studio またはその他のホストへのアクセス](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\))に関するページを参照してください。

### <a name="design-time-text-templates-run-in-a-separate-appdomain"></a>別の AppDomain で実行されるデザイン時テキスト テンプレート

 [デザイン時テキスト テンプレート](../modeling/design-time-code-generation-by-using-t4-text-templates.md)は、メイン アプリケーションとは別の AppDomain で実行されることに注意してください。 ほとんどの場合、これは重要ではありませんが、一部の複雑な状況で制限が生じることがあります。 たとえば、別のサービスからテンプレート内またはテンプレート外のデータを渡す場合、そのサービスでシリアル化可能な API を提供する必要があります。

 (これは、コードの残りの部分と共にコンパイルされるコードを提供する[実行時テキスト テンプレート](../modeling/run-time-text-generation-with-t4-text-templates.md)には当てはまりません。)

## <a name="editing-templates"></a>テンプレートの編集
 拡張機能マネージャーのオンライン ギャラリーからは、専用のテキスト テンプレート エディターをダウンロードできます。 **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。 **[オンライン ギャラリー]** をクリックし、検索ツールを使用します。

## <a name="related-topics"></a>関連トピック

|タスク|トピック|
|-|-|
|テンプレートを作成する。|[T4 テキスト テンプレートの記述に関するガイドライン](../modeling/guidelines-for-writing-t4-text-templates.md)|
|プログラム コードを使用してテキストを生成する。|[テキスト テンプレートの構造](../modeling/writing-a-t4-text-template.md)|
|Visual Studio ソリューション内にファイルを生成する。|[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|Visual Studio の外部でテキストの生成を実行する。|[TextTransform ユーティリティを使用したファイルの生成](../modeling/generating-files-with-the-texttransform-utility.md)|
|ドメイン固有言語の形式でデータを変換する。|[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)|
|独自のデータ ソースを変換するためのディレクティブ プロセッサを作成する。|[T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)|
