---
title: 'チュートリアル: テキスト テンプレートを使用したコード生成'
description: コード生成について説明します。コード生成を使用すると、厳密に型指定され、ソース モデルが変わった場合でも簡単に変更できるプログラム コードを作成できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- walkthroughs [text templates], generating application code
- walkthroughs [text templates]
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7e6b824d53c37ef922b8c9580c87a478aef93586
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924063"
---
# <a name="walkthrough-generate-code-by-using-text-templates"></a>チュートリアル: テキスト テンプレートを使用してコードを生成する

コード生成を使用すると、厳密に型指定され、ソース モデルが変わった場合でも簡単に変更できるプログラム コードを作成できます。 コード生成とは対照的に、構成ファイルを使用する完全に汎用的なプログラムを作成する他の手法もあります。構成ファイルを使用すると、柔軟ではありますが、読むのも変更するのも容易ではなく、パフォーマンスもそれほどよくありません。 このチュートリアルでは、コード生成の利点について説明します。

## <a name="typed-code-for-reading-xml"></a>XML 読み取り用の型指定されたコード

System.Xml 名前空間は、XML ドキュメントを読み込み、メモリ内で自由に操作できる包括的なツールとして利用できます。 残念ながら、すべてのノードは XmlNode という同じ型です。 そのため、間違った子ノードの型を期待する、間違った属性を期待するなどのプログラミングのミスを犯しやすくなります。

このプロジェクト例では、テンプレートでサンプル XML ファイルを読み取り、ノードの各型に対応するクラスを生成します。 手入力のコードでは、これらのクラスを使用して XML ファイルを操作できます。 また、同じノード型を使用する他のファイルでも、アプリケーションを実行できます。 サンプル XML ファイルの目的は、アプリケーションで対応できるようにするすべてのノード型の例を提供することです。

> [!NOTE]
> Visual Studio に含まれるアプリケーション [xsd.exe](/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe) では、XML ファイルから厳密に型指定されたクラスを生成できます。 ここで紹介するテンプレートは、例として提供されています。

サンプル ファイルは次のとおりです。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<catalog>
  <artist id ="Mike%20Nash" name="Mike Nash Quartet">
    <song id ="MikeNashJazzBeforeTeatime">Jazz Before Teatime</song>
    <song id ="MikeNashJazzAfterBreakfast">Jazz After Breakfast</song>
  </artist>
  <artist id ="Euan%20Garden" name="Euan Garden">
    <song id ="GardenScottishCountry">Scottish Country Garden</song>
  </artist>
</catalog>
```

このチュートリアルで作成するプロジェクトでは、次のようなコードを記述できます。IntelliSense では、入力内容に応じて正しい属性と子の名前が表示されます。

```csharp
Catalog catalog = new Catalog(xmlDocument);
foreach (Artist artist in catalog.Artist)
{
  Console.WriteLine(artist.name);
  foreach (Song song in artist.Song)
  {
    Console.WriteLine("   " + song.Text);
  }
}
```

テンプレートを使用せずに、型指定されていないコードを作成した場合は次のようになります。

```csharp
XmlNode catalog = xmlDocument.SelectSingleNode("catalog");
foreach (XmlNode artist in catalog.SelectNodes("artist"))
{
    Console.WriteLine(artist.Attributes["name"].Value);
    foreach (XmlNode song in artist.SelectNodes("song"))
    {
         Console.WriteLine("   " + song.InnerText);
     }
}
```

厳密に型指定されているバージョンの場合、XML スキーマを変更すると、クラスも変更されます。 コンパイラでは、変更が必要なアプリケーション コードの部分が強調表示されます。 汎用的な XML コードを使用する型指定されていないバージョンの場合、このようなサポートはありません。

このプロジェクトでは、1 つのテンプレート ファイルを使用して、型指定されたバージョンを可能にするクラスを生成します。

## <a name="set-up-the-project"></a>プロジェクトをセットアップする

### <a name="create-or-open-a-c-project"></a>C# プロジェクトを作成する、または開く

この手法は任意のコード プロジェクトに適用できます。 このチュートリアルでは、C# プロジェクトを使用します。また、テストの目的でコンソール アプリケーションを使用します。

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

2. **[Visual C#]** ノードをクリックし、 **[テンプレート]** ウィンドウで **[コンソール アプリケーション]** をクリックします。

### <a name="add-a-prototype-xml-file-to-the-project"></a>プロトタイプの XML ファイルをプロジェクトに追加する

このファイルの目的は、アプリケーションで読み取ることができるようにする XML ノード型のサンプルを提供することです。 このファイルは、アプリケーションのテストにも使用できます。 このテンプレートで、ファイル内の各ノード型について C# クラスが生成されます。

このファイルは、テンプレートで読み取ることができるようにプロジェクトに含める必要がありますが、コンパイルされたアプリケーションには組み込まれません。

1. **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[追加]** をクリックしてから **[新しい項目]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[テンプレート]** ウィンドウの **[XML ファイル]** を選択します。

3. サンプルの内容をファイルに追加します。

4. このチュートリアルでは、ファイルに `exampleXml.xml`と名前を付けます。 前のセクションで示した XML のようにファイルの内容を設定します。

### <a name="add-a-test-code-file"></a>テスト コード ファイルを追加する

C# ファイルをプロジェクトに追加し、どのような記述方法を実現したいかを踏まえて、そのファイルにコードのサンプルを記述します。 次に例を示します。

```csharp
using System;
namespace MyProject
{
  class CodeGeneratorTest
  {
    public void TestMethod()
    {
      Catalog catalog = new Catalog(@"..\..\exampleXml.xml");
      foreach (Artist artist in catalog.Artist)
      {
        Console.WriteLine(artist.name);
        foreach (Song song in artist.Song)
        {
          Console.WriteLine("   " + song.Text);
} } } } }
```

この段階では、このコードはコンパイルに失敗します。 コンパイルを可能にするクラスは、テンプレートを作成する過程で生成することになります。

より広範囲なテストを実行すれば、サンプル XML ファイルの既知のコンテンツに照らして、テスト関数の出力をチェックすることもできます。 ただし、このチュートリアルでは、テスト メソッドがコンパイルされたら目的が達成されたと見なします。

### <a name="add-a-text-template-file"></a>テキスト テンプレート ファイルを追加する

テキスト テンプレート ファイルを追加し、出力の拡張子を *.cs* に設定します。

1. **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[追加]** をクリックしてから **[新しい項目]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[テンプレート]** ウィンドウの **[テキスト テンプレート]** を選択します。

    > [!NOTE]
    > [前処理されたテキスト テンプレート] ではなく、[テキスト テンプレート] を追加するようにしてください。

3. ファイルの template ディレクティブで、 `hostspecific` 属性を `true`に変更します。

     この変更によって、テンプレート コードが Visual Studio のサービスにアクセスできるようになります。

4. output ディレクティブの extension 属性を ".cs" に変更します。これで、このテンプレートから C# ファイルが生成されるようになります。 Visual Basic プロジェクトの場合は、これを ".vb" に変更します。

5. ファイルを保存します。 この段階で、テキスト テンプレート ファイルには、次の行が含まれていることになります。

    ```
    <#@ template debug="false" hostspecific="true" language="C#" #>
    <#@ output extension=".cs" #>
    ```

ソリューション エクスプローラーで、テンプレート ファイルの下位項目として .cs ファイルが表示されることに注意してください。 これは、テンプレート ファイルの名前の横にある [+] をクリックすることで確認できます。 このファイルは、テンプレート ファイルを保存したり、テンプレート ファイルからフォーカスを移動したりするたびに、テンプレート ファイルから生成されます。 生成されたファイルは、プロジェクトの一部としてコンパイルされます。

テンプレート ファイルの開発中は、テンプレート ファイルと生成されたファイルのウィンドウを並べて表示すると便利です。 このようにすると、テンプレートの出力結果をすぐに確認できます。 また、テンプレートから無効な C# コードが生成された場合、エラー メッセージ ウィンドウにエラーが表示されることがわかります。

生成されたファイルに直接加えた編集は、テンプレート ファイルを保存するとすべて失われます。 そのため、生成されたファイルは一切編集しないようにするか、一時的な実験に限って編集するようにしてください。 IntelliSense が有効な生成されたファイル内で、短いコード片を試し、その後、テンプレート ファイルにコピーすると便利です。

## <a name="develop-the-text-template"></a>テキスト テンプレートを開発する

ここでは、アジャイル開発の慣例に従って、テンプレートを小さなステップに分けて開発します。1 つのステップを経るたびにいくつかのエラーを解消し、最終的にテスト コードを正常にコンパイルして実行できる状態にします。

### <a name="prototype-the-code-to-be-generated"></a>生成されるコードのプロトタイプを作成する

テスト コードは、ファイル内の各ノードに対応するクラスを必要とします。 そのため、いくつかのコンパイル エラーは、次のコード行をテンプレートに追加して保存すると解消されます。

```csharp
class Catalog {}
class Artist {}
class Song {}
```

これで必要なものはわかりましたが、宣言は、サンプル XML ファイル内のノード型から生成される必要があります。 これらの試験的なコード行をテンプレートから削除してください。

### <a name="generate-application-code-from-the-model-xml-file"></a>モデル XML ファイルからアプリケーション コードを生成する

XML ファイルを読み込んでクラスの宣言を生成するには、テンプレート コンテンツを次のテンプレート コードで置き換えます。

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml"#>
<#@ import namespace="System.Xml" #>
<#
 XmlDocument doc = new XmlDocument();
 // Replace this file path with yours:
 doc.Load(@"C:\MySolution\MyProject\exampleXml.xml");
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
#>
  public partial class <#= node.Name #> {}
<#
 }
#>
```

ファイルのパスは、実際のプロジェクトのパスに置き換えてください。

コード ブロックの区切り記号 ( `<#...#>`) に注目してください。 テキストを生成するプログラム コードのフラグメントは、これらの区切り記号で囲みます。 文字列に評価できる式は、式ブロックの区切り記号 ( `<#=...#>` ) で囲みます。

アプリケーションのソース コードを生成するテンプレートを記述しているときは、このように 2 種類のプログラム テキストを扱っていることになります。 コード ブロックの区切り記号の内側に記述されたプログラムは、テンプレートを保存したり、フォーカスを別のウィンドウに切り替えたりするたびに実行されます。 そこから生成されるテキストは区切り記号の外側に配置され、生成されたファイルにコピーされ、アプリケーション コードの一部となります。

`<#@assembly#>` ディレクティブは参照と同じように動作し、テンプレート コードでアセンブリを使用できるようにします。 テンプレートから見えるアセンブリのリストは、アプリケーション プロジェクトの参照の一覧とは異なります。

`<#@import#>` ディレクティブは `using` ステートメントと同じように動作し、インポートされた名前空間内のクラスを短い名前で使用できるようにします。

このテンプレートはコードを生成しますが、残念なことに、サンプル XML ファイル内のすべてのノードのクラス宣言が出力されます。したがって、 `<song>` ノードの複数のインスタンスが存在すると、song クラスの宣言も複数生成されることになります。

### <a name="read-the-model-file-then-generate-the-code"></a>モデル ファイルを読み取ってからコードを生成する

多くのテキスト テンプレートは、テンプレートの最初の部分でソース ファイルを読み取り、次の部分でテンプレートを生成するというパターンに従います。 ここでも、サンプル ファイルをすべて読み取り、その中に含まれているノード型をまとめてから、クラス宣言を生成する必要があります。 `Dictionary<>:` を使用できるようにするために、`<#@import#>` がもう 1 つ必要です。

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml"#>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.Collections.Generic" #>
<#
 // Read the model file
 XmlDocument doc = new XmlDocument();
 doc.Load(@"C:\MySolution\MyProject\exampleXml.xml");
 Dictionary <string, string> nodeTypes =
        new Dictionary<string, string>();
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
   nodeTypes[node.Name] = "";
 }
 // Generate the code
 foreach (string nodeName in nodeTypes.Keys)
 {
#>
  public partial class <#= nodeName #> {}
<#
 }
#>
```

### <a name="add-an-auxiliary-method"></a>補助メソッドを追加する

クラス機能コントロール ブロックは、補助メソッドを定義できるブロックです。 このブロックは `<#+...#>` で囲み、ファイル内の最後のブロックとして記述する必要があります。

クラス名の先頭文字を大文字にするには、テンプレートの最後の部分を次のテンプレート コードで置き換えます。

```
// Generate the code
 foreach (string nodeName in nodeTypes.Keys)
 {
#>
  public partial class <#= UpperInitial(nodeName) #> {}
<#
 }
#>
<#+
 private string UpperInitial(string name)
 { return name[0].ToString().ToUpperInvariant() + name.Substring(1); }
#>
```

この段階で、生成される *.cs* ファイルには次の宣言が含まれています。

```csharp
public partial class Catalog {}
public partial class Artist {}
public partial class Song {}
```

同じアプローチを使用して、子ノードのプロパティ、属性、内部テキストなど、より詳細な情報を追加することもできます。

### <a name="access-the-visual-studio-api"></a>Visual Studio API にアクセスする

`<#@template#>` ディレクティブの `hostspecific` 属性を設定すると、テンプレートから Visual Studio API にアクセスできます。 テンプレートでは、これを使用してプロジェクト ファイルの場所を取得することにより、テンプレート コードでの絶対パスの使用を避けることができます。

```
<#@ template debug="false" hostspecific="true" language="C#" #>
...
<#@ assembly name="EnvDTE" #>
...
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
// Open the prototype document.
XmlDocument doc = new XmlDocument();
doc.Load(System.IO.Path.Combine(dte.ActiveDocument.Path, "exampleXml.xml"));
```

## <a name="complete-the-text-template"></a>テキスト テンプレートを完成させる

次のテンプレート コンテンツで、テスト コードのコンパイルと実行を可能にするコードが生成されます。

```
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.Collections.Generic" #>
using System;using System.Collections.Generic;using System.Linq;using System.Xml;namespace MyProject{
<#
 // Map node name --> child name --> child node type
 Dictionary<string, Dictionary<string, XmlNodeType>> nodeTypes = new Dictionary<string, Dictionary<string, XmlNodeType>>();

 // The Visual Studio host, to get the local file path.
 EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
 // Open the prototype document.
 XmlDocument doc = new XmlDocument();
 doc.Load(System.IO.Path.Combine(dte.ActiveDocument.Path, "exampleXml.xml"));
 // Inspect all the nodes in the document.
 // The example might contain many nodes of the same type,
 // so make a dictionary of node types and their children.
 foreach (XmlNode node in doc.SelectNodes("//*"))
 {
   Dictionary<string, XmlNodeType> subs = null;
   if (!nodeTypes.TryGetValue(node.Name, out subs))
   {
     subs = new Dictionary<string, XmlNodeType>();
     nodeTypes.Add(node.Name, subs);
   }
   foreach (XmlNode child in node.ChildNodes)
   {
     subs[child.Name] = child.NodeType;
   }
   foreach (XmlNode child in node.Attributes)
   {
     subs[child.Name] = child.NodeType;
   }
 }
 // Generate a class for each node type.
 foreach (string className in nodeTypes.Keys)
 {
    // Capitalize the first character of the name.
#>
    partial class <#= UpperInitial(className) #>
    {      private XmlNode thisNode;      public <#= UpperInitial(className) #>(XmlNode node)       { thisNode = node; }

<#
    // Generate a property for each child.
    foreach (string childName in nodeTypes[className].Keys)
    {
      // Allow for different types of child.
      switch (nodeTypes[className][childName])
      {
         // Child nodes:
         case XmlNodeType.Element:
#>
      public IEnumerable<<#=UpperInitial(childName)#>><#=UpperInitial(childName) #>      {         get         {            foreach (XmlNode node in                thisNode.SelectNodes("<#=childName#>"))              yield return new <#=UpperInitial(childName)#>(node);       } }
<#
         break;
         // Child attributes:
         case XmlNodeType.Attribute:
#>
      public string <#=childName #>      { get { return thisNode.Attributes["<#=childName#>"].Value; } }
<#
         break;
         // Plain text:
         case XmlNodeType.Text:
#>
      public string Text  { get { return thisNode.InnerText; } }
<#
         break;
       } // switch
     } // foreach class child
  // End of the generated class:
#>
   }
<#
 } // foreach class

   // Add a constructor for the root class
   // that accepts an XML filename.
   string rootClassName = doc.SelectSingleNode("*").Name;
#>
   partial class <#= UpperInitial(rootClassName) #>   {      public <#= UpperInitial(rootClassName) #>(string fileName){        XmlDocument doc = new XmlDocument();        doc.Load(fileName);        thisNode = doc.SelectSingleNode("<#=rootClassName#>");}   }}
<#+
   private string UpperInitial(string name)
   {
      return name[0].ToString().ToUpperInvariant() + name.Substring(1);
   }
#>
```

### <a name="run-the-test-program"></a>テスト プログラムを実行する

テスト メソッドは、コンソール アプリケーションの Main にある次のコード行によって実行されます。 F5 キーを押して、プログラムをデバッグ モードで実行します。

```csharp
using System;
namespace MyProject
{
  class Program
  {
    static void Main(string[] args)
    {
      new CodeGeneratorTest().TestMethod();
      // Allow user to see the output:
      Console.ReadLine();
    }
  }
}
```

### <a name="write-and-update-the-application"></a>アプリケーションを作成して更新する

これで、汎用的な XML コードの代わりに生成されたクラスを使用して、厳密に型指定されたスタイルでアプリケーションを記述できるようになりました。

XML スキーマが変更された場合は、新しいクラスを簡単に生成できます。 コンパイラは、アプリケーション コードの変更が必要な部分を開発者に示します。

サンプルの XML ファイルが変更されたときにクラスを再生成するには、**ソリューション エクスプローラー** で、ツールバーの **[すべてのテンプレートの変換]** をクリックします。

## <a name="conclusion"></a>まとめ

このチュートリアルでは、コード生成に関して、いくつかの手法と利点を紹介しました。

- *コード生成* とは、アプリケーションのソース コードの一部を *モデル* から作成することです。 モデルには、アプリケーション ドメインに適した形式で情報が格納されています。モデルは、アプリケーションのライフタイムを通して変化する可能性があります。

- コード生成の利点の 1 つは、厳密な型指定が可能になることです。 モデルは、よりユーザーに適した形式で情報を表現します。これに対して生成されたコードは、アプリケーションの他の部分で、一連の型を使用して情報を扱うことができるようにします。

- 新しいコードを記述する場合も、スキーマが更新された場合も、IntelliSense とコンパイラによって、モデルのスキーマに沿ったコードを効率的に作成できます。

- 単純なテンプレート ファイルを 1 つプロジェクトに追加するだけで、このような利点が生み出されます。

- テキスト テンプレートは、すばやく増分的に開発およびテストできます。

このチュートリアルでは、実際にモデルのインスタンスからプログラム コードが生成されます。このモデルは、アプリケーションによって処理される XML ファイルの典型的な例です。 より本格的なアプローチでは、XML スキーマを .xsd ファイルまたはドメイン固有言語定義の形式でテンプレートへの入力として使用します。 このアプローチの方が、リレーションシップの多重度など、さまざまな特性をテンプレートで判断しやすくなります。

## <a name="troubleshoot-the-text-template"></a>テキスト テンプレートのトラブルシューティングを行う

テンプレートの変換エラーやコンパイル エラーが **[エラー一覧]** に表示された場合、または出力ファイルが正しく生成されなかった場合は、「[TextTransform ユーティリティを使用したファイルの生成](../modeling/generating-files-with-the-texttransform-utility.md)」で説明されている方法を使用してテキスト テンプレートをトラブルシューティングできます。

## <a name="see-also"></a>関連項目

- [T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
- [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)
