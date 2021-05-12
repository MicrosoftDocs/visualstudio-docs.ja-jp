---
title: FxCop コード分析 (バイナリ分析) と .NET アナライザー (ソース分析)
ms.date: 09/06/2018
description: Visual Studio でのレガシ FxCop (バイナリ分析) と .NET アナライザー (ソース分析) の違いを説明します。 これらのアナライザーの使用方法に関する質問への回答です。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis FAQ
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 951e9b951f1d90077fe29506e9c288fb19f2d5ff
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800567"
---
# <a name="frequently-asked-questions-about-legacy-fxcop-and-net-analyzers"></a>レガシ FxCop および .NET アナライザーに関してよく寄せられる質問

レガシ FxCop (バイナリ分析) と .NET アナライザー (ソース分析) の違いは、少し理解しにくい場合があります。 この記事は、ユーザーの方々がお持ちの質問を解決することを意図しています。

## <a name="whats-the-difference-between-legacy-fxcop-and-net-analyzers"></a>レガシ FxCop と .NET アナライザー間の違いは何ですか?

従来の FxCop は、コンパイル済みのアセンブリ上でビルド後の分析を実行します。 これは、**FxCopCmd.exe** という別の実行可能ファイルとして実行されます。 FxCopCmd.exe はコンパイル済みのアセンブリを読み込み、コード分析を実行し、結果 (または *診断*) を報告します。

.NET アナライザーは .NET Compiler Platform ("Roslyn") に基づいています。 これは、[.NET SDK から有効にするか、NuGet パッケージとしてインストール](install-net-analyzers.md)します。このパッケージは、プロジェクトまたはソリューションによって参照されます。 アナライザーは、コンパイラーの実行中にソース コードに基づく分析を実行します。 アナライザーは、**csc.exe** または **vbc.exe** のコンパイラーのプロセス内にホストされ、プロジェクトの構築時に分析を実行します。 アナライザーの結果は、コンパイラーの結果と共に報告されます。

## <a name="whats-the-difference-between-fxcop-analyzers-and-net-analyzers"></a>FxCop アナライザーと .NET アナライザーの違いは何ですか?

FxCop アナライザーと .NET アナライザーはどちらも、FxCop CA 規則の .NET Compiler Platform ("Roslyn") アナライザーの実装を参照します。 Visual Studio 2019 16.8 および .NET 5.0 より前のリリースでは、これらのアナライザーが `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)として出荷されていました。 Visual Studio 2019 16.8 および .NET 5.0 以降は、これらのアナライザーが [.NET SDK](/dotnet/fundamentals/code-analysis/overview) に含まれています。 これらのアナライザーは、`Microsoft.CodeAnalysis.NetAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)として入手することもできます。 [FxCop アナライザーから .NET アナライザーへの移行](migrate-from-fxcop-analyzers-to-net-analyzers.md)を検討してください。

## <a name="does-the-run-code-analysis-command-run-net-analyzers"></a>.NET アナライザーは、[コード分析の実行] コマンドで実行されるのですか?

Visual Studio 2019 16.5 リリースより前のバージョンでは、 **[分析]**  >  **[コード分析の実行]** を選択すると、レガシ分析が実行されます。 Visual Studio 2019 16.5 以降では、 **[コード分析の実行]** メニュー オプションを使用すると、選択したプロジェクトまたはソリューションに対して Roslyn ベースのアナライザーが実行されます。 .NET アナライザーがインストールされている場合は、それらも実行されます。 詳細については、[マネージド コードに手動でコード分析を実行する方法に関するページ](how-to-run-code-analysis-manually-for-managed-code.md)を参照してください。

## <a name="does-the-runcodeanalysis-msbuild-project-property-run-analyzers"></a>RunCodeAnalysis msbuild プロジェクト プロパティはアナライザーを実行しますか?

いいえ。 (たとえば *.csproj* の) プロジェクト ファイル内の **RunCodeAnalysis** プロパティは、従来の FxCop を実行するためのみに使用します。 これは、**FxCopCmd.exe** を起動するビルド後の msbuild タスクを実行します。

## <a name="so-how-do-i-run-net-analyzers-then"></a>では、.NET アナライザーはどのように実行するのですか?

.NET アナライザーを実行するには、最初に [.NET SDK から有効にするか、NuGet パッケージとしてインストール](install-net-analyzers.md)します。 次いでプロジェクトまたはソリューションを Visual Studio または msbuild を使用してビルドします。 Roslyn アナライザーが生成する警告やエラーは、 **[エラー一覧]** またはコマンド ウィンドウに表示されます。

## <a name="i-get-warning-ca0507-even-after-ive-installed-the-net-analyzers-nuget-package"></a>.NET アナライザーの NuGet パッケージをインストールした後でも警告 CA0507 が表示される

.NET アナライザーをインストールしても、" **"コード分析の実行" は廃止され、ビルド時には FxCop アナライザーが実行されます**" という警告 CA0507 が引き続き表示される場合は、状況に応じて、[プロジェクト ファイル](../ide/solutions-and-projects-in-visual-studio.md#project-file)内の **RunCodeAnalysis** msbuild プロパティを **false** に設定することが必要である可能性があります。 それ以外の場合、レガシ分析は、各ビルドの後に実行されます。

```xml
<RunCodeAnalysis>false</RunCodeAnalysis>
```

## <a name="which-rules-have-been-ported-to-net-analyzers"></a>.NET アナライザーには、どの規則が移植されていますか?

.NET アナライザーに移植されたレガシ分析規則の詳細については、「[Fxcop 規則の移植ステータス](fxcop-rule-port-status.md)」を参照してください。

## <a name="code-analysis-warnings-are-treated-as-errors"></a>コード分析の警告がエラーとして扱われる

プロジェクトでビルド オプションが使用されて警告がエラーとして扱われる場合は、アナライザーの警告がエラーとして表示されることがあります。 コード分析の警告がエラーとして扱われないようにするには、「[コード分析に関する FAQ](../code-quality/analyzers-faq.md#treat-warnings-as-errors)」にある手順を実行します。

## <a name="see-also"></a>こちらもご覧ください

- [.NET Compiler Platform アナライザーの概要](roslyn-analyzers-overview.md)
- [.NET アナライザーへの移行](migrate-from-legacy-analysis-to-net-analyzers.md)
- [.NET アナライザーのインストール](install-net-analyzers.md)
