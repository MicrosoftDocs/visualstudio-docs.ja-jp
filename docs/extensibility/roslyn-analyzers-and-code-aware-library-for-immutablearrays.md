---
title: Roslyn アナライザーと ImmutableArray 用コード認識ライブラリ
description: System.Collections.Immutable NuGet パッケージを使用する際、一般的なエラーをキャッチするために、実際の Roslyn アナライザーを構築する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e3bdcc9c35f5acaf9937bd18b0160f9e5a58161c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060588"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>Roslyn アナライザーと ImmutableArray 用コード認識ライブラリ

[.NET Compiler Platform](https://github.com/dotnet/roslyn) ("Roslyn") を使用すると、コード認識ライブラリをビルドできます。 コード認識ライブラリには、最適な方法でのライブラリ使用に役立ち、エラーを回避するために利用できる機能およびツール (Roslyn アナライザー) が用意されています。 このトピックでは、[System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable) NuGet パッケージを使用する際、一般的なエラーをキャッチするために、実際の Roslyn アナライザーを構築する方法について説明します。 また、この例では、アナライザーによって検出されたコードの問題に対してコード修正を行う方法も示しています。 ユーザーは、コード修正を Visual Studio の電球 UI で確認し、そのコードの修正を自動的に適用できます。

## <a name="get-started"></a>はじめに

この例をビルドするには、次のものが必要です。

* Visual Studio 2015 (Express Edition 以外) 以降のバージョン。 無料の [Visual Studio Community Edition](https://visualstudio.microsoft.com/vs/community/) を使用できます
* [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。 また、Visual Studio をインストールするときに、 **[共通ツール]** の **[Visual Studio Extensibility Tools]** をオンにして SDK を同時にインストールすることもできます。 Visual Studio を既にインストールしている場合は、メイン メニューの **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** に移動し、左側のナビゲーション ウィンドウで **[C#]** を選択し、 **[拡張機能]** を選択して、この SDK をインストールすることもできます。 **[Install the Visual Studio Extensibility Tools]** \(Visual Studio Extensibility Tools のインストール\) 階層リンク プロジェクト テンプレートを選択すると、SDK をダウンロードしてインストールするように求められます。
* [.NET Compiler Platform ("Roslyn") SDK](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK)。 メイン メニューの **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** に移動し、左側のナビゲーション ウィンドウで **[C#]** を選択し、 **[機能拡張]** を選択して、この SDK をインストールすることもできます。 **[Download the .NET Compiler Platform SDK]\(.NET Compiler Platform SDK のダウンロード\)** 階層リンク プロジェクト テンプレートを選択すると、SDK をダウンロードしてインストールするように求められます。 この SDK には、[Roslyn Syntax Visualizer](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Syntax-Visualizer.md) が含まれています。 この便利なツールは、アナライザーでどのようなコード モデルの種類を検索する必要があるかを確認するのに役立ちます。 アナライザー インフラストラクチャにより、特定のコード モデルの種類に対してコードが呼び出されるので、コードは必要なときにのみ実行され、関連するコードの分析にのみ集中できます。

## <a name="whats-the-problem"></a>何が問題なのでしょうか。

ImmutableArray (たとえば、<xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>) をサポートするライブラリを用意するとします。 C# の開発者は、.NET の配列に関して多くの経験があります。 ただし、ImmutableArray の性質と実装で使用される最適化技術により、ライブラリのユーザーが、C# 開発者の直感で、以下のように破損したコードを作成してしまうことがあります。 さらに、ユーザーには実行時までエラーが表示されません。これは、.NET を用いる Visual Studio で使い慣れた上質のエクスペリエンスではありません。

ユーザーは、次のようなコードを書くことに慣れています。

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

空の配列を作成して、後続のコード行とコレクション初期化子構文を使って配列を設定することは、C# 開発者にとってなじみ深いものです。 ただし、ImmutableArray に対して次のように同じコードを書くと、実行時にクラッシュします。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

最初のエラーは、ImmutableArray の実装で、構造体を使って基になるデータ ストレージをラップしていることが原因です。 `default(T)` 式からすべてゼロまたは null のメンバーを持つ構造体が返されるように、構造体にパラメーターのないコンストラクターを持たせる必要があります。 コードから `b1.Length` にアクセスするときに、ImmutableArray 構造体に基になるストレージ配列がないため、実行時の null 逆参照エラーが発生します。 空の ImmutableArray を作成する正しい方法は `ImmutableArray<int>.Empty` です。

コレクション初期化子のエラーは、`ImmutableArray.Add` メソッドが呼び出されるたびに新しいインスタンスが返されるために発生します。 ImmutableArray は変更できないため、新しい要素を追加すると、新しい ImmutableArray オブジェクトが返されます (パフォーマンス上の理由から、既存の ImmutableArray とストレージを共有する場合があります)。 `b2` は `Add()` を 5 回呼び出す前の最初の ImmutableArray を指しているので、`b2` はデフォルトの ImmutableArray となります。 その Length を呼び出すと、null 逆参照エラーでクラッシュします。 Add を手動で呼び出すことなく ImmutableArray を初期化する正しい方法は、`ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})` を使用することです。

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>関連する構文ノードの型を検出してアナライザーをトリガーする

 アナライザーのビルドを開始するには、まず、検索する必要がある SyntaxNode の型を確認します。 メニューの **[表示]**  >  **[その他のウィンドウ]**  >  **[Roslyn Syntax Visualizer]** から **Syntax Visualizer** を起動します。

`b1` を宣言する行にエディターのキャレットを配置します。 Syntax Visualizer の表示で、構文ツリーの `LocalDeclarationStatement` ノードに含まれることがわかります。 このノードには、`VariableDeclaration` があり、次に `VariableDeclarator` があり、さらに `EqualsValueClause` があり、最後に `ObjectCreationExpression` があります。 ノードの Syntax Visualizer ツリーをクリックすると、そのノードで表されるコードを示すためにエディター ウィンドウの構文が強調表示されます。 SyntaxNode のサブタイプの名前は、C# 文法で使用されている名前と一致します。

## <a name="create-the-analyzer-project"></a>アナライザー プロジェクトを作成する

メイン メニューから **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログの左側のナビゲーション バーで、 **[C#]** プロジェクトの下にある **[機能拡張]** を選択し、右ペインで **[Analyzer with Code Fix]\(コード修正付きアナライザー\)** プロジェクト テンプレートを選択します。 名前を入力し、ダイアログを確認します。

このテンプレートにより、*DiagnosticAnalyzer.cs* ファイルが開かれます。 [エディター バッファー] タブを選択します。このファイルには、`DiagnosticAnalyzer` (Roslyn API 型) から派生したアナライザー クラス (プロジェクトに指定した名前の形式) が含まれています。 新しいクラスには、アナライザーが C# 言語に関連していることを宣言する `DiagnosticAnalyzerAttribute` があるため、コンパイラによってアナライザーが検出され、読み込まれます。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

C# コードを対象とするアナライザーを Visual Basic を使用して実装できます。また、その逆も可能です。 DiagnosticAnalyzerAttribute では、アナライザーが 1 つの言語を対象とするか、または両方を対象とするかの選択がより重要です。 言語の詳細なモデリングを必要とする洗練されたアナライザーの場合、1 つの言語のみを対象にすることができます。 たとえば、アナライザーが型名またはパブリック メンバー名のみを確認する場合は、Visual Basic と C# の両方に Roslyn に用意されている共通言語モデルを使用することができます。 たとえば、FxCop により、クラスに <xref:System.Runtime.Serialization.ISerializable> が実装されているにもかかわらず、クラスに <xref:System.SerializableAttribute> 属性がないことが警告されます。これは言語に依存せず、Visual Basic と C# の両方のコードで機能します。

## <a name="initialize-the-analyzer"></a>アナライザーを初期化する

 `DiagnosticAnalyzer` クラスの少し下にスクロールして、`Initialize` メソッドを表示します。 アナライザーがアクティブになると、コンパイラからこのメソッドが呼び出されます。 このメソッドは `AnalysisContext` オブジェクトを受け取ります。これで、アナライザーからコンテキスト情報を取得し、分析するコードの種類のイベントのコールバックを登録できるようになります。

```csharp
public override void Initialize(AnalysisContext context) {}
```

このメソッドで新しい行を開き、「context.」と入力して、 IntelliSense の入力候補一覧を表示します。 入力候補一覧には、さまざまな種類のイベントを処理するための多くの `Register...` メソッドがあります。 たとえば、1 つ目の `RegisterCodeBlockAction` により、ブロックがコードにコールバックされます。これは通常、中かっこの間のコードです。 ブロックに対して登録すると、フィールドの初期化子、属性に指定された値、または省略可能なパラメーターの値をコードにコールバックすることもできます。

もう 1 つの例として、`RegisterCompilationStartAction` により、コンパイルの開始時にコードにコールバックされます。これは、さまざまな場所で状態を収集する必要がある場合に便利です。 たとえば、使用されているすべてのシンボルを集めるデータ構造を作成し、構文やシンボルがアナライザーにコールバックされるたびに、それぞれの場所に関する情報をデータ構造に保存することができます。 コンパイルの終了によってコールバックされたときに、保存したすべての場所を分析して、たとえば、コードがそれぞれの `using` ステートメントから使用するシンボルを報告することができます。

**Syntax Visualizer** を使用して、コンパイラによって ObjectCreationExpression が処理されるときに、呼び出されるようにしたい、と気付きました。 このコードを使用して、コールバックを設定します。

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

構文ノードに対して登録し、オブジェクト作成の構文ノードのみをフィルター処理します。 規約により、アナライザーの作成者はアクションを登録するときにラムダ式を使用します。これにより、アナライザーをステートレスに保つことができます。 Visual Studio の **使用法から生成** 機能を使用して、`AnalyzeObjectCreation` メソッドを作成できます。 これにより、正しい型のコンテキスト パラメーターも生成されます。

## <a name="set-properties-for-users-of-your-analyzer"></a>アナライザーのユーザーのプロパティを設定する

アナライザーが Visual Studio UI に適切に表示されるように、次のコード行を探してアナライザーを識別するように変更します。

```csharp
internal const string Category = "Naming";
```

`"Naming"` を `"API Guidance"` に変更します。

次に、**ソリューション エクスプローラー** を使用して、プロジェクト内の *Resources.resx* ファイルを見つけて開きます。 アナライザーの説明、タイトルなどを入力できます。ここでは、これらのすべての値を `"Don't use ImmutableArray<T> constructor"` に変更します。 文字列形式の引数 ({0}、{1} など) を文字列に含めることができます。後で `Diagnostic.Create()` を呼び出すときに、渡される引数の `params` 配列を指定できます。

## <a name="analyze-an-object-creation-expression"></a>オブジェクト作成式を分析する

`AnalyzeObjectCreation` メソッドは、コード アナライザー フレームワークによって提供されるさまざまな型のコンテキストを受け取ります。 `Initialize` メソッドの `AnalysisContext` を使用すると、アクション コールバックを登録してアナライザーを設定できます。 たとえば、`SyntaxNodeAnalysisContext` には `CancellationToken` があり、これを渡すことができます。 ユーザーがエディターで入力を開始すると、Roslyn はアナライザーの実行をキャンセルして作業を保存し、パフォーマンスを向上させます。 もう 1 つの例として、このコンテキストには、オブジェクト作成の構文ノードを返す Node プロパティがあります。

ノードを取得すると、構文ノード アクションをフィルター処理した型であると想定できます。

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>初めてアナライザーを使用して Visual Studio を起動する

アナライザーをビルドおよび実行して Visual Studio を起動します (**F5** キーを押します)。 **ソリューション エクスプローラー** のスタートアップ プロジェクトは VSIX プロジェクトであるため、コードの実行で、コードと VSIX がビルドされ、その VSIX がインストールされて Visual Studio が起動します。 この方法で Visual Studio を起動すると、個別のレジストリ ハイブで起動されるため、メインで使用する Visual Studio は、アナライザーのビルド中にテスト インスタンスの影響を受けることはありません。 この方法で初めて起動すると、Visual Studio をインストールした後、初めて起動したときと同様に、Visual Studio でいくつかの初期化が行われます。

コンソール プロジェクトを作成し、コンソール アプリケーションの Main メソッドに次のような配列コードを入力します。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

`ImmutableArray` を含むコード行には波線が表示されます。これは、不変の NuGet パッケージを取得し、コードに `using` ステートメントを追加する必要があるためです。 **ソリューション エクスプローラー** のプロジェクト ノードで右のポインター ボタンを押して、 **[NuGet パッケージの管理]** を選択します。 NuGet マネージャーで、検索ボックスに「Immutable」と入力し、左ペインで項目 **[System.Collections.Immutable]** を選択して ( **[Microsoft.Bcl.Immutable]** を選択しないでください)、右ペインにある **[インストール]** ボタンを押します。 パッケージをインストールすると、プロジェクト参照への参照が追加されます。

`ImmutableArray` の下にまだ赤い波線が表示されているので、その識別子にキャレットを配置し **Ctrl**+ **.** (ピリオド) を押して、 推奨される修正メニューを表示し、適切な `using` ステートメントを選択して追加します。

ここでは、Visual Studio の 2 番目のインスタンスで、 **[すべてを保存] して [閉じる]** をクリックし、クリーンな状態にして続行します。

## <a name="finish-the-analyzer-using-edit-and-continue"></a>エディット コンティニュを使用してアナライザーを終了する

Visual Studio の最初のインスタンスで、最初の行にキャレットを置き、**F9** キーを押して、`AnalyzeObjectCreation` メソッドの先頭にブレークポイントを設定します。

**F5** キーを押して再度アナライザーを起動し、Visual Studio の 2 番目のインスタンスで、最後に作成したコンソール アプリケーションをもう一度開きます。

ブレークポイントで Visual Studio の最初のインスタンスに戻ります。これは、Roslyn コンパイラによってオブジェクト作成式が確認され、アナライザーが呼び出されたためです。

**オブジェクト作成ノードを取得します。** **F10** キーを押して `objectCreation` 変数を設定する行をステップ オーバーし、 **[イミディエイト ウィンドウ]** で式 `"objectCreation.ToString()"` を評価します。 変数が指す構文ノードが、まさに探しているコード `"new ImmutableArray<int>()"` であることがわかります。

**ImmutableArray<T\> Type オブジェクトを取得します。** 作成される型が ImmutableArray であるかどうかを確認する必要があります。 まず、この型を表すオブジェクトを取得します。 セマンティック モデルを使用して型を調べ、完全に正しい型であることを確認します。`ToString()` からの文字列での比較は行いません。 関数の最後に次のコード行を入力します。

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

メタデータのジェネリック型は、バック クォート (`) とジェネリック パラメーターの数を使用して指定します。 そのため、メタデータ名には "...ImmutableArray\<T>" とは表示されません。

セマンティック モデルには、シンボル、データ フロー、変数の有効期間などの問い合わせを確認できる、多くの便利な機能があります。さまざまなエンジニアリング上の理由 (パフォーマンス、モデリングに誤りのあるコードなど) から、Roslyn により、セマンティック モデルから構文ノードが分離されます。 コンパイル モデルで、参照に含まれている情報を検索して正確な比較を行う必要があります。

エディター ウィンドウの左側では、黄色の実行ポインターをドラッグできます。 `objectCreation` 変数が設定されている行までドラッグし、**F10** キーを使用して新しいコード行にステップ オーバーします。 変数 `immutableArrayOfType` の上にマウス ポインターを合わせると、セマンティック モデルで正確な型が見つかったことがわかります。

**オブジェクト作成式の型を取得します。** この記事では、"型" がいくつかの方法で使われていますが、これは "new Foo" という式があれば、Foo のモデルを取得する必要があることを意味します。 ImmutableArray\<T> 型であるかどうかを確認するために、オブジェクト作成式の型を取得する必要があります。 セマンティック モデルを再度使用して、オブジェクト作成式の型シンボル (ImmutableArray) のシンボル情報を取得します。 関数の最後に次のコード行を入力します。

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

アナライザーにより、エディター バッファー内の不完全または正しくないコードを処理する必要があるため (たとえば、`using` ステートメントが存在しない)、`symbolInfo` が `null` であることを確認する必要があります。 分析を完了するには、シンボル情報オブジェクトから名前付きの型 (INamedTypeSymbol) を取得する必要があります。

**型を比較します。** 検索している T にはオープン ジェネリック型があり、コード内の型が具象ジェネリック型であるため、型が何から構成されているか (オープン ジェネリック型) に関してシンボル情報のクエリを実行し、その結果を `immutableArrayOfTType` と比較します。 メソッドの最後に次のコード行を入力します。

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**診断を報告します。** 診断の報告は非常に簡単です。 プロジェクト テンプレートで生成されたルールを使用します。これは、Initialize メソッドの前に定義されています。 このコードの状況はエラーであるため、ルールを初期化した行を変更して、`DiagnosticSeverity.Warning` (緑の波線) を `DiagnosticSeverity.Error` (赤の波線) に変えることができます。 ルールの残りの部分では、チュートリアルの冒頭付近で編集したリソースから初期化します。 また、波線の場所を報告する必要もあります。これは、オブジェクト作成式の型指定の場所です。 次のコードを `if` ブロックに入力します。

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

関数は次のようになります (おそらく、書式は異なります)。

```csharp
private void AnalyzeObjectCreation(SyntaxNodeAnalysisContext context)
{
    var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
    var immutableArrayOfTType =
        context.SemanticModel
               .Compilation
               .GetTypeByMetadataName(
                   "System.Collections.Immutable.ImmutableArray`1");
    var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as
        INamedTypeSymbol;
    if (symbolInfo != null &&
        symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
    {
        context.ReportDiagnostic(
            Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
    }
}
```

ブレークポイントを削除して、アナライザーの動作を確認できるようにします (Visual Studio の最初のインスタンスに戻らなくなります)。 実行ポインターをメソッドの先頭にドラッグし、**F5** キーを押して実行を続行します。 Visual Studio の 2 番目のインスタンスに戻ると、再びコンパイラによってコードの検証が開始され、アナライザーが呼び出されます。 `ImmutableType<int>` の下に波線が表示されます。

## <a name="adding-a-code-fix-for-the-code-issue"></a>コードの問題に対する "コード修正" の追加

開始する前に、Visual Studio の 2 番目のインスタンスを閉じ、Visual Studio の最初のインスタンス (アナライザーを開発している場所) でデバッグを停止します。

**新しいクラスを追加します。** **ソリューション エクスプローラー** のプロジェクト ノードのショートカット メニュー (右ポインター ボタン) を使い、選択して新しい項目を追加します。 `BuildCodeFixProvider` というクラスを追加します。 このクラスは `CodeFixProvider` から派生する必要があり、**Ctrl**+ **.** (ピリオド) キーを使用して、 正しい `using` ステートメントを追加するコード修正を呼び出す必要があります。 このクラスには `ExportCodeFixProvider` 属性の注釈を付ける必要もあり、`LanguageNames` 列挙型を解決するために `using` ステートメントを追加する必要があります。 クラス ファイルには、次のコードが含まれている必要があります。

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**派生メンバーをスタブします。** ここで、エディターのキャレットを識別子 `CodeFixProvider` に配置し、**Ctrl**+ **.** (ピリオド) キーを押して、 この抽象基本クラスの実装をスタブします。 これにより、プロパティとメソッドが生成されます。

**プロパティを実装します。** `FixableDiagnosticIds` プロパティの `get` 本体に次のコードを入力します。

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn により、単なる文字列であるこれらの識別子が照合され、診断と修正がまとめられます。 プロジェクト テンプレートによって診断 ID が生成されます。これは、自由に変更できます。 プロパティのコードにより、アナライザー クラスからの ID のみが返されます。

**RegisterCodeFixAsync メソッドがコンテキストを受け取ります。** 1 つのコード修正が複数の診断に適用されたり、1 行のコードで複数の問題が発生したりする可能性があるため、コンテキストは重要です。 メソッドの本体で「context.」と入力すると、 IntelliSense の入力候補一覧に、有用なメンバーがいくつか表示されます。 修正を取り消す必要があるかどうかを確認できる CancellationToken メンバーがあります。 多数の有用なメンバーを持つ Document メンバーがあり、それらを使用してプロジェクトおよびソリューション モデル オブジェクトにアクセスできます。 診断の報告で指定されたコードの開始と終了の場所を示す Span メンバーがあります。

**メソッドを非同期にします。** 最初に行う必要があるのは、生成されたメソッド宣言を `async` メソッドに修正することです。 メソッドから `async` が返される場合でも、抽象クラスの実装をスタブするコード修正には、`Task` キーワードが含まれていません。

**構文ツリーのルートを取得します。** コードを変更するには、コード修正によって行われた変更を含む新しい構文ツリーを生成する必要があります。 コンテキストから `Document` を取得して、`GetSyntaxRootAsync` を呼び出す必要があります。 構文ツリーを取得する不明な作業 (ディスクからのファイルの取得、解析、Roslyn コードモデルの構築など) があるため、これは非同期メソッドです。 この間、Visual Studio UI の応答性を向上させる必要がありますが、`async` の使用でそれが可能になります。 メソッドのコード行を次のように置き換えます。

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**問題のあるノードを見つけます。** コンテキストのスパンを渡しますが、見つけたノードは、変更する必要のあるコードではない可能性があります。 報告された診断では、(波線が属している) 型識別子のスパンのみが指定されていましたが、オブジェクト作成式全体を置き換える必要があります。これには、先頭の `new` キーワードと末尾のかっこが含まれます。 次のコードをメソッドに追加します (それから **Ctrl**+ **.** キーを使用して、 `ObjectCreationExpressionSyntax` 用に `using` ステートメントを追加します)。

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**電球 UI のコード修正を登録します。** コード修正を登録すると、Roslyn により Visual Studio の電球 UI に自動的にプラグインされます。 エンド ユーザーが **Ctrl**+ **.** (ピリオド) キーを使用できるのは、 アナライザーにより、不適切な `ImmutableArray<T>` コンストラクターの使用が波線で表示されているときです。 コード修正プロバイダーは問題が発生した場合にのみ実行されるため、探していたオブジェクト作成式があると想定できます。 コンテキスト パラメーターから、`RegisterCodeFixAsync` メソッドの末尾に次のコードを追加することで、新しいコード修正を登録できます。

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

エディターのキャレットを識別子 `CodeAction` に配置し、**Ctrl**+ **.** (ピリオド) キーを使用して、 この型に適切な `using` ステートメントを追加します。

次に、エディターのキャレットを識別子 `ChangeToImmutableArrayEmpty` に配置し、**Ctrl**+ **.** (ピリオド) キーをもう一度使用して、 このメソッドのスタブを生成します。

追加されたこの最後のコード スニペットは、`CodeAction` と、見つかった問題の種類に応じた診断 ID を渡すことにより、コード修正を登録します。 この例では、このコードで提供される修正の診断 ID が 1 つしかないため、診断 ID 配列の最初の要素を渡すだけで済みます。 `CodeAction` を作成するときに、電球 UI がコード修正の説明として使用するテキストを渡します。 また、CancellationToken を受け取り、新しい Document を返す関数も渡します。 新しい Document には、`ImmutableArray.Empty` を呼び出す修正コードを含む新しい構文ツリーがあります。 このコード スニペットでは、objectCreation ノードとコンテキストの Document を閉じることができるように、ラムダ式を使用しています。

**新しい構文ツリーを構築します。** 先ほど生成したスタブがある `ChangeToImmutableArrayEmpty` メソッドで、コード行「`ImmutableArray<int>.Empty;`」を入力します。 **Syntax Visualizer** ツール ウィンドウをもう一度表示すると、この構文が SimpleMemberAccessExpression ノードであることがわかります。 これは、このメソッドにより、新しい Document を構築して返すために必要なものです。

`ChangeToImmutableArrayEmpty` への最初の変更は、`Task<Document>` の前に `async` を追加することです。これは、コードジェネレーターがメソッドが非同期であると想定できないためです。

本体に次のコードを入力して、メソッドが次のようになるようにします。

```csharp
private async Task<Document> ChangeToImmutableArrayEmpty(
    ObjectCreationExpressionSyntax objectCreation, Document document,
    CancellationToken c)
{
    var generator = SyntaxGenerator.GetGenerator(document);
    var memberAccess =
        generator.MemberAccessExpression(objectCreation.Type, "Empty");
    var oldRoot = await document.GetSyntaxRootAsync(c);
    var newRoot = oldRoot.ReplaceNode(objectCreation, memberAccess);
    return document.WithSyntaxRoot(newRoot);
}
```

エディターのキャレットを `SyntaxGenerator` 識別子に配置し、**Ctrl**+ **.** (ピリオド) キーを使用して、 この型に適切な `using` ステートメントを追加します。

このコードでは、新しいコードを構築するための便利な型である、`SyntaxGenerator` を使用しています。 コードの問題があるドキュメントのジェネレーターを取得した後、`ChangeToImmutableArrayEmpty` は `MemberAccessExpression` を呼び出し、アクセスしたいメンバーを持つ型を渡し、メンバーの名前を文字列として渡します。

次に、メソッドはドキュメントのルートをフェッチします。一般的なケースでは、ここで任意の処理が含まれる可能性があるため、コードはこの呼び出しを待機し、キャンセル トークンを渡します。 Roslyn コード モデルは、.NET 文字列を使用する場合と同様に変更不可です。文字列を更新すると、新しい文字列オブジェクトが返されます。 `ReplaceNode` を呼び出すと、新しいルート ノードが返されます。 構文ツリーの大部分は (不変であるため) 共有されていますが、`objectCreation` ノードは `memberAccess` ノードに置き換えられ、構文ツリー ルートまでのすべての親ノードも置き換えられます。

## <a name="try-your-code-fix"></a>コード修正を試す

**F5** キーを押して、Visual Studio の 2 番目のインスタンスでアナライザーを実行できるようになりました。 前に使用したコンソール プロジェクトを開きます。 これで、`ImmutableArray<int>` の新しいオブジェクト作成式の場所に電球が表示されるはずです。 **Ctrl**+ **.** (ピリオド) キーを押すと、 コード修正が表示され、自動生成されたコード差分のプレビューが電球 UI で表示されます。 これは、Roslyn によって作成されます。

**Pro ヒント:** Visual Studio の 2 番目のインスタンスを起動したときに、コード修正で電球が表示されない場合は、Visual Studio コンポーネントキャッシュをクリアする必要があります。 キャッシュをクリアすると、Visual Studio でコンポーネントが再検証されるため、Visual Studio によって最新のコンポーネントが取得されるはずです。 最初に、Visual Studio の 2 番目のインスタンスをシャットダウンします。 次に、**Windows エクスプローラー** で *%LOCALAPPDATA%\Microsoft\VisualStudio\16.0Roslyn\\* に移動します ("16.0" は、Visual Studio のバージョンごとに変わります)。サブディレクトリ *ComponentModelCache* を削除します。

## <a name="talk-video-and-finish-code-project"></a>講演ビデオとコード プロジェクトの完了

この例については、[この講演](https://channel9.msdn.com/events/Build/2015/3-725)でさらに開発を進め、説明しています。 この講演では、動作するアナライザーを実演し、その構築方法を説明しています。

完成したすべてのコードは、[こちら](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)で確認できます。 サブフォルダー *DoNotUseImmutableArrayCollectionInitializer* および *DoNotUseImmutableArrayCtor* にはそれぞれ、問題を見つけるための C# ファイルと、Visual Studio の電球 UI で表示されるコード修正を実装する C# ファイルがあります。 完成したコードでは、ImmutableArray\<T> 型オブジェクトが何度もフェッチされるのを避けるためにもう少し抽象化されていることに注意してください。 入れ子になった登録済みのアクションを使用して、サブ アクション (オブジェクト作成の分析とコレクション初期化の分析) が実行されるたびに使用できるコンテキストに型オブジェクトを保存します。

## <a name="see-also"></a>こちらもご覧ください

* [\\\ビルド 2015 講演](https://channel9.msdn.com/events/Build/2015/3-725)
* [GitHub 上の完成したコード](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [3 種類のアナライザーにグループ化された GitHub 上のいくつかの例](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [GitHub OSS サイト上のその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [GitHub 上の Roslyn アナライザーに実装されている FxCop のルール](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)
