---
title: EditorConfig とアナライザー
ms.date: 03/11/2019
description: Visual Studio での .NET Compiler Platform ベースのコード分析について説明します。 EditorConfig ファイル、ルール セット、その他のトピックに関する質問への回答を示します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6d67471027f36d0e22c055f4306ce2137d972463
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800569"
---
# <a name="code-analysis-faq"></a>コード分析に関する FAQ

このページには、Visual Studio での .NET Compiler Platform ベースのコード分析についてよく寄せられる質問への回答が記載されています。

## <a name="code-analysis-versus-editorconfig"></a>コード分析と EditorConfig

**Q**: コード スタイルをチェックするためにコード分析または EditorConfig を使用する必要はありますか?

**A**: コード分析と EditorConfig ファイルは連携して機能します。 [EditorConfig ファイル](/dotnet/fundamentals/code-analysis/code-style-rule-options)または[テキスト エディターの [オプション]](../ide/code-styles-and-code-cleanup.md) ページでコード スタイルを定義すると、実際には、Visual Studio に組み込まれているコード アナライザーが構成されます。 EditorConfig ファイルを使用すると、アナライザー ルールを有効または無効にすることができ、NuGet アナライザー パッケージを構成することもできます。

## <a name="editorconfig-versus-rule-sets"></a>EditorConfig とルール セット

**Q**: ルール セットまたは EditorConfig ファイルを使用してアナライザーを構成する必要はありますか?

**A**: ルール セットと EditorConfig ファイルは共存でき、どちらもアナライザーの構成に使用できます。 EditorConfig ファイルとルール セットでは、どちらもルールを有効または無効にし、その重大度を設定できます。

ただし、EditorConfig ファイルでは、ルールを構成するための他の方法も提供されます。

- .NET コード品質アナライザーの場合、EditorConfig ファイルを使用して、[分析するコードの種類を定義](/dotnet/fundamentals/code-analysis/code-quality-rule-options)できます。
- Visual Studio に組み込まれている .NET コード スタイル アナライザーの場合、EditorConfig ファイルを使用して、コードベースの[優先コード スタイルを定義](/dotnet/fundamentals/code-analysis/code-style-rule-options)できます。

ルール セットと EditorConfig ファイルに加えて、C# および VB コンパイラの[追加ファイル](../ide/build-actions.md#build-action-values)としてマークされたテキスト ファイルを使用して構成されるアナライザーもあります。

> [!NOTE]
> - EditorConfig ファイルを使用したルールの有効化とその重大度の設定は、Visual Studio 2019 バージョン 16.3 以降でのみ可能です。
> - EditorConfig ファイルを使用してレガシ分析を構成することはできませんが、ルール セットでは可能です。

## <a name="code-analysis-in-ci-builds"></a>CI ビルドでのコード分析

**Q**: .NET Compiler Platform ベースのコード分析は継続的インテグレーション (CI) ビルドで機能しますか?

**A**: はい。 NuGet パッケージからインストールされたアナライザーの場合、そのルールは[ビルド時に適用](roslyn-analyzers-overview.md#build-errors)されます。これには CI ビルド時も含まれます。 CI ビルドで使用されるアナライザーでは、ルール セットと EditorConfig ファイルの両方のルール構成が考慮されます。 現在、Visual Studio に組み込まれているコード アナライザーは NuGet パッケージとして入手できないため、これらのルールは CI ビルドでは適用できません。

## <a name="ide-analyzers-versus-stylecop"></a>IDE アナライザーと StyleCop

**Q**: Visual Studio IDE コード アナライザーと StyleCop アナライザーの違いは何ですか?

**A**: Visual Studio IDE には、コードのスタイルと品質の両方の問題を探す組み込みのアナライザーがあります。 これらのルールにより、導入された新しい言語機能を使用し、コードの保守容易性を向上させることができます。 IDE アナライザーは、Visual Studio のリリースごとに継続的に更新されます。

[StyleCop アナライザー](https://github.com/DotNetAnalyzers/StyleCopAnalyzers)は、NuGet パッケージとしてインストールされるサードパーティのアナライザーであり、コードのスタイルの一貫性をチェックします。 一般に、StyleCop のルールを使用すると、推奨されるスタイルが示されるのではなく、コードベースの個人用設定を構成できます。

## <a name="code-analyzers-versus-legacy-analysis"></a>コード アナライザーとレガシ分析

**Q**: レガシ分析と .NET Compiler Platform ベースのコード分析の違いは何ですか?

**A**: .NET Compiler Platform ベースのコード分析では、ソース コードがリアルタイムおよびコンパイル時に分析されます。一方、レガシ分析では、ビルドの完了後にバイナリ ファイルが分析されます。 詳細については、[.NET Compiler Platform ベースの分析とレガシ分析の比較](../code-quality/net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers)に関するセクションを参照してください。

## <a name="fxcop-analyzers-versus-net-analyzers"></a>FxCop アナライザーと .NET アナライザー

**Q**: FxCop アナライザーと .NET アナライザーの違いは何ですか?

**A**: FxCop アナライザーと .NET アナライザーはどちらも、FxCop CA ルールの .NET Compiler Platform ("Roslyn") アナライザー実装を参照します。 Visual Studio 2019 16.8 および .NET 5.0 より前では、これらのアナライザーは `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)として出荷されていました。 Visual Studio 2019 16.8 および .NET 5.0 以降では、これらのアナライザーは [.NET SDK に含まれています](/dotnet/fundamentals/code-analysis/overview)。 これらは、`Microsoft.CodeAnalysis.NetAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)として入手することもできます。 [FxCop アナライザーから .NET アナライザーへの移行](migrate-from-fxcop-analyzers-to-net-analyzers.md)を検討してください。

## <a name="treat-warnings-as-errors"></a>警告をエラーとして扱う

**Q**: プロジェクトで、警告をエラーとして扱うビルド オプションを使用しています。 レガシ分析からソース コード分析への移行後、コード分析のすべての警告がエラーとして表示されるようになりました。 これを防ぐにはどうすればよいですか?

**A**: コード分析の警告がエラーとして扱われないようにするには、これらの手順に従います。

  1. 次の内容の .props ファイルを作成します。

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. .csproj または .vbproj プロジェクト ファイルに行を追加して、前の手順で作成した .props ファイルをインポートします。 この行は、アナライザーの .props ファイルをインポートする行の前に配置する必要があります。 たとえば、.props ファイルの名前が codeanalysis.props の場合、次のようになります。

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.NetAnalyzers.5.0.0\build\Microsoft.CodeAnalysis.NetAnalyzers.props')" />
     ...
     ```

## <a name="code-analysis-solution-property-page"></a>コード分析ソリューションのプロパティ ページ

**Q**: ソリューションの [コード分析] プロパティ ページはどこにありますか?

**A**: ソリューション レベルの [コード分析] プロパティ ページが削除され、より信頼性の高い共有プロパティ グループが採用されました。 プロジェクト レベルでコード分析を管理するために、[コード分析] プロパティ ページを引き続き使用できます (マネージド プロジェクトの場合、ルール構成のためにルール セットから EditorConfig に移行することもお勧めします)。ソリューションまたはリポジトリ内の複数のプロジェクトまたはすべてのプロジェクトでルール セットを共有する場合は、共有 props/targets ファイルまたは *Directory.props/Directory.targets* ファイルで [CodeAnalysisRuleSet](../code-quality/using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project) プロパティを使用してプロパティ グループを定義することをお勧めします。 すべてのプロジェクトでインポートされる、このような共通の props または targets がない場合は、最上位のソリューション ディレクトリにある [Directory.props または Directory.targets ファイル](../msbuild/customize-your-build.md)にこのようなプロパティ グループを追加することを検討してください。これは、ディレクトリまたはそのサブディレクトリで定義されているすべてのプロジェクト ファイルに自動的にインポートされます。

## <a name="see-also"></a>こちらもご覧ください

- [アナライザーの概要](roslyn-analyzers-overview.md)
- [EditorConfig の .NET コーディング規則の設定](/dotnet/fundamentals/code-analysis/code-style-rule-options)