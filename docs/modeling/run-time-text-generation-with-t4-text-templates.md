---
title: T4 テキスト テンプレートを使用した実行時テキスト生成
description: Visual Studio ランタイム テキスト テンプレートを使用して、実行時にアプリケーションでテキスト文字列を生成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- Preprocessed Text Template project item
- TextTemplatingFilePreprocessor custom tool
- text templates, TransformText() method
- text templates, generating files at run time
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5c64dd1c8ee25f2e0a3c2b94caa8026438b32286
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937954"
---
# <a name="run-time-text-generation-with-t4-text-templates"></a>T4 テキスト テンプレートを使用した実行時テキスト生成

Visual Studio 実行時テキスト テンプレートを使用して、実行時にアプリケーションでテキスト文字列を生成できます。 アプリケーションを実行するコンピューターに Visual Studio がインストールされている必要はありません。 実行時テンプレートは、コンパイル時にテンプレートによって実行時に実行されるコードが生成されるため、"前処理済みテキスト テンプレート" と呼ばれることがあります。

各テンプレートは、生成される文字列に出現するテキストと、プログラム コードのフラグメントを組み合わせたものです。 プログラム フラグメントでは、文字列の変数部分の値を指定すると共に、条件と反復の部分も制御します。

たとえば、HTML レポートを作成するアプリケーションでは、次のテンプレートを使用できます。

```html
<#@ template language="C#" #>
<html><body>
<h1>Sales for Previous Month</h2>
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
This report is Company Confidential.
</body></html>
```

テンプレートは HTML ページであり、変数部分がプログラム コードに置き換えられていることに注意してください。 このようなページのデザインを開始するには、HTML ページの静的なプロトタイプを作成します。 次に、テーブルやその他の変数部分を、場合によって異なるコンテンツを生成するプログラム コードに置き換えることができます。

アプリケーションでテンプレートを使用すると、たとえば長い一連の書き込みステートメントの場合よりも、出力の最終形を簡単に確認しやすくなります。 出力の形式を変更することが、より簡単でより信頼のあるものになります。

## <a name="creating-a-run-time-text-template-in-any-application"></a>任意のアプリケーションで実行時テキスト テンプレートを作成する

### <a name="to-create-a-run-time-text-template"></a>実行時テキスト テンプレートを作成するには

1. ソリューション エクスプローラーのプロジェクトのショートカット メニューで **[追加]**  >  **[新しい項目]** の順に選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[実行時テキスト テンプレート]** を選択します (Visual Basic では **[共通項目]**  >  **[全般]** )。

3. テンプレート ファイルの名前を入力します。

    > [!NOTE]
    > テンプレート ファイル名は、生成されたコードでクラス名として使用されます。 したがって、スペースや句読点は使用できません。

4. **[追加]** を選びます。

    拡張子が **.tt** の新しいファイルが作成されます。 その **[カスタム ツール]** プロパティは、**TextTemplatingFilePreprocessor** に設定されています。 次の行が含まれます。

    ```
    <#@ template language="C#" #>
    <#@ assembly name="System.Core" #>
    <#@ import namespace="System.Linq" #>
    <#@ import namespace="System.Text" #>
    <#@ import namespace="System.Collections.Generic" #>
    ```

## <a name="converting-an-existing-file-to-a-run-time-template"></a>既存のファイルを実行時テンプレートに変換する

テンプレートを作成するには、出力の既存の例を変換することをお勧めします。 たとえば、アプリケーションで HTML ファイルを生成する場合は、プレーン HTML ファイルを作成することから始めることができます。 正しく動作し、その表示が正しいことを確認します。 次に、それを Visual Studio プロジェクトに含め、テンプレートに変換します。

### <a name="to-convert-an-existing-text-file-to-a-run-time-template"></a>既存のテキスト ファイルを実行時テンプレートに変換するには

1. ファイルを Visual Studio プロジェクトに含めます。 ソリューション エクスプローラーのプロジェクトのショートカット メニューで、 **[追加]**  >  **[既存アイテム]** を選択します。

2. ファイルの **[カスタム ツール]** プロパティを **TextTemplatingFilePreprocessor** に設定します。 ソリューション エクスプローラーのファイルのショートカット メニューで、 **[プロパティ]** を選択します。

    > [!NOTE]
    > プロパティが既に設定されている場合は、**TextTemplatingFileGenerator** ではなく **TextTemplatingFilePreprocessor** であることを確認します。 これは、拡張子が **.tt** のファイルを既に含めている場合に発生する可能性があります。

3. ファイル名拡張子を **.tt** に変更します。 この手順は省略可能ですが、正しくないエディターでファイルを開くことを避けるのに役立ちます。

4. ファイル名のメイン部分から、スペースまたは句読点があれば削除します。 たとえば、"My Web Page.tt" は適切ではありませんが、"MyWebPage.tt" は適切です。 ファイル名は、生成されたコードでクラス名として使用されます。

5. ファイルの先頭に次の行を挿入します。 Visual Basic プロジェクトで作業している場合は、"C#" を "VB" に置き換えます。

    `<#@ template language="C#" #>`

## <a name="the-content-of-the-run-time-template"></a>実行時テンプレートのコンテンツ

### <a name="template-directive"></a>テンプレート ディレクティブ

テンプレートの最初の行は、ファイルを作成したときのままにします。

`<#@ template language="C#" #>`

language パラメーターは、プロジェクトの言語によって異なります。

### <a name="plain-content"></a>プレーン コンテンツ

アプリケーションで生成するテキストが含まれるように **.tt** ファイルを編集します。 次に例を示します。

```html
<html><body>
<h1>Sales for January</h2>
<!-- table to be inserted here -->
This report is Company Confidential.
</body></html>
```

### <a name="embedded-program-code"></a>埋め込みプログラム コード

プログラム コードは、`<#` と `#>` の間に挿入できます。 次に例を示します。

```csharp
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
```

```vb
<table>
<#
    For i As Integer = 1 To 10
#>
    <tr><td>Test name <#= i #> </td>
      <td>Test value <#= i*i #> </td></tr>
<#
    Next
#>
</table>
```

`<# ... #>` の間にステートメントが挿入され、`<#= ... #>` の間に式が挿入されることに注意してください。 詳細については、「[T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

## <a name="using-the-template"></a>テンプレートの使用

### <a name="the-code-built-from-the-template"></a>テンプレートからビルドされたコード

**.tt** ファイルを保存すると、従属する **.cs** または **.vb** ファイルが生成されます。 このファイルを **ソリューション エクスプローラー** で表示するには、 **.tt** ファイル ノードを展開します。 Visual Basic プロジェクトで、まず、**ソリューション エクスプローラー** のツール バーの **[すべてのファイルを表示]** を選択します。

この場合、従属ファイルには、`TransformText()` というメソッドを含む部分クラスが含まれていることに注意してください。 このメソッドは、アプリケーションから呼び出すことができます。

### <a name="generating-text-at-run-time"></a>テキストを実行時に生成する

アプリケーション コードでは、次のような呼び出しを使用して、テンプレートのコンテンツを生成できます。

```csharp
MyWebPage page = new MyWebPage();
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

```vb
Dim page = New My.Templates.MyWebPage
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

生成されたクラスを特定の名前空間に配置するには、テキスト テンプレート ファイルの **[カスタム ツールの名前空間]** プロパティを設定します。

### <a name="debugging-runtime-text-templates"></a>実行時テキスト テンプレートをデバッグする

通常のコードと同じ方法で、実行時テキスト テンプレートをデバッグおよびテストします。

テキスト テンプレートにブレークポイントを設定できます。 Visual Studio からデバッグ モードでアプリケーションを起動する場合は、通常の方法でコードをステップ実行し、ウォッチ式を評価できます。

### <a name="passing-parameters-in-the-constructor"></a>コンストラクターでパラメーターを渡す

通常、テンプレートでは、アプリケーションの他の部分からデータをインポートする必要があります。 これを簡単にするため、テンプレートによって作成されたコードは部分クラスです。 プロジェクト内の別のファイルに、同じクラスの別の部分を作成できます。 そのファイルには、テンプレートに埋め込まれているコードからと、アプリケーションの残りの部分からの両方でアクセスできる、パラメーター、プロパティ、関数を持つコンストラクターを含めることができます。

たとえば、個別のファイル **MyWebPageCode.cs** を作成するとします。

```csharp
partial class MyWebPage
{
    private MyData m_data;
    public MyWebPage(MyData data) { this.m_data = data; }}
```

テンプレート ファイル **MyWebPage.tt** で、次のように記述するとします。

```html
<h2>Sales figures</h2>
<table>
<# foreach (MyDataItem item in m_data.Items)
   // m_data is declared in MyWebPageCode.cs
   { #>
      <tr><td> <#= item.Name #> </td>
          <td> <#= item.Value #> </td></tr>
<# } // end of foreach
#>
</table>
```

アプリケーションでこのテンプレートを使用するには:

```csharp
MyData data = ...;
MyWebPage page = new MyWebPage(data);
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

#### <a name="constructor-parameters-in-visual-basic"></a>Visual Basic のコンストラクター パラメーター

Visual Basic では、個別のファイル **MyWebPageCode.vb** に次のものが含まれます。

```vb
Namespace My.Templates
  Partial Public Class MyWebPage
    Private m_data As MyData
    Public Sub New(ByVal data As MyData)
      m_data = data
    End Sub
  End Class
End Namespace
```

テンプレート ファイルには次のものが含まれるとします。

```html
<#@ template language="VB" #>
<html><body>
<h1>Sales for January</h2>
<table>
<#
    For Each item In m_data.Items
#>
    <tr><td>Test name <#= item.Name #> </td>
      <td>Test value <#= item.Value #> </td></tr>
<#
    Next
#>
</table>
This report is Company Confidential.
</body></html>
```

テンプレートは、コンストラクターでパラメーターを渡すことによって呼び出すことができます。

```vb
Dim data = New My.Templates.MyData
    ' Add data values here ....
Dim page = New My.Templates.MyWebPage(data)
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

#### <a name="passing-data-in-template-properties"></a>テンプレート プロパティでデータを渡す

テンプレートにデータを渡す別の方法として、部分クラス定義でテンプレート クラスにパブリック プロパティを追加する方法があります。 アプリケーションでは、`TransformText()` を呼び出す前にプロパティを設定できます。

また、部分定義でテンプレート クラスにフィールドを追加することもできます。 これにより、連続したテンプレート実行の間でデータを渡すことができます。

### <a name="use-partial-classes-for-code"></a>コードに部分クラスを使用する

多くの開発者は、大規模なコード本体をテンプレートに記述することは避けようとします。 代わりに、テンプレート ファイルと同じ名前を持つ部分クラスでメソッドを定義できます。 これらのメソッドをテンプレートから呼び出します。 このようにすることにより、テンプレートでは、ターゲットの出力文字列がどのように表示されるかがより明確に示されます。 結果の外観に関する議論は、表示されるデータを作成するためのロジックから分離できます。

### <a name="assemblies-and-references"></a>アセンブリと参照

テンプレート コードで .NET またはその他のアセンブリ (**System.Xml.dll** など) を参照する場合は、通常の方法でプロジェクトの **[参照]** に追加します。

`using` ステートメントと同じ方法で名前空間をインポートする場合は、`import` ディレクティブを使用してこれを行うことができます。

```
<#@ import namespace="System.Xml" #>
```

これらのディレクティブは、ファイルの先頭で `<#@template` ディレクティブの直後に配置する必要があります。

### <a name="shared-content"></a>共有コンテンツ

複数のテンプレート間で共有されるテキストがある場合は、それを個別のファイルに配置し、出現させる各ファイルにインクルードすることができます。

```
<#@include file="CommonHeader.txt" #>
```

インクルードされるコンテンツには、プログラム コードとプレーン テキストの任意の組み合わせを含めることができ、他のインクルード ディレクティブやその他のディレクティブを含めることができます。

インクルード ディレクティブは、テンプレート ファイルまたはインクルードされるファイルのテキスト内の任意の場所で使用できます。

### <a name="inheritance-between-run-time-text-templates"></a>実行時テキスト テンプレート間の継承

基本クラス テンプレート (これは抽象になることがあります) を記述することによって、実行時テンプレート間でコンテンツを共有できます。 `<@#template#>` ディレクティブの `inherits` パラメーターを使用して、別の実行時テンプレート クラスを参照します。

#### <a name="inheritance-pattern-fragments-in-base-methods"></a>継承パターン: 基本メソッドのフラグメント

次の例で使用しているパターンでは、次の点に注意してください。

- 基本クラス `SharedFragments` では、クラス機能ブロック `<#+ ... #>` 内のメソッドを定義します。

- 基本クラスにはフリー テキストは含まれません。 代わりに、すべてのテキスト ブロックがクラス機能メソッド内で発生します。

- 派生クラスは、`SharedFragments` で定義されているメソッドを呼び出します。

- アプリケーションでは派生クラスの `TextTransform()` メソッドを呼び出しますが、基本クラス `SharedFragments` を変換しません。

- 基本と派生の両方のクラスは、実行時テキスト テンプレートです。つまり、 **[カスタム ツール]** プロパティは **TextTemplatingFilePreprocessor** に設定されます。

**SharedFragments.tt:**

```
<#@ template language="C#" #>
<#+
protected void SharedText(int n)
{
#>
   Shared Text <#= n #>
<#+
}
// Insert more methods here if required.
#>
```

**MyTextTemplate1.tt:**

```
<#@ template language="C#" inherits="SharedFragments" #>
begin 1
   <# SharedText(2); #>
end 1
```

**MyProgram.cs:**

```csharp
...
MyTextTemplate1 t1  = new MyTextTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**結果の出力:**

```
begin 1
    Shared Text 2
end 1
```

#### <a name="inheritance-pattern-text-in-base-body"></a>継承パターン: 基本の本文のテキスト

テンプレートの継承を使用するこの別の方法では、テキストの大部分が基本テンプレートで定義されます。 派生テンプレートでは、基本コンテンツに適したデータとテキスト フラグメントが提供されます。

**AbstractBaseTemplate1.tt:**

```
<#@ template language="C#" #>

Here is the description for this derived template:
  <#= this.Description #>

Here is the fragment specific to this derived template:
<#
  this.PushIndent("  ");
  SpecificFragment(42);
  this.PopIndent();
#>
End of common template.
<#+
  // State set by derived class before calling TextTransform:
  protected string Description = "";
  // 'abstract' method to be defined in derived classes:
  protected virtual void SpecificFragment(int n) { }
#>
```

**DerivedTemplate1.tt:**

```
<#@ template language="C#" inherits="AbstractBaseTemplate1" #>
<#
  // Set the base template properties:
  base.Description = "Description for this derived class";

  // Run the base template:
  base.TransformText();

#>
End material for DerivedTemplate1.

<#+
// Provide a fragment specific to this derived template:

protected override void SpecificFragment(int n)
{
#>
   Specific to DerivedTemplate1 : <#= n #>
<#+
}
#>
```

**アプリケーション コード:**

```csharp
...
DerivedTemplate1 t1 = new DerivedTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**結果の出力:**

```
Here is the description for this derived template:
  Description for this derived class

Here is the fragment specific to this derived template:
     Specific to DerivedTemplate1 : 42
End of common template.
End material for DerivedTemplate1.
```

## <a name="related-topics"></a>関連トピック

デザイン時テンプレート: テンプレートを使用してアプリケーションの一部となるコードを生成する場合は、「[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」を参照してください。

実行時テンプレートは、コンパイル時にテンプレートとそのコンテンツが決定されるすべてのアプリケーションで使用できます。 ただし、実行時に変更されるテンプレートからテキストを生成する Visual Studio 拡張機能を記述する場合は、[VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)
- [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)
- [T4 ツールボックス](http://olegsych.com/T4Toolbox/)
