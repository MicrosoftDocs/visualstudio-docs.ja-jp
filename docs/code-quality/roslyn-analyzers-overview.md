---
title: Roslyn アナライザーを使用したコード分析
ms.date: 09/01/2020
description: Visual Studio のソース コード分析について理解を深めます。 コード修正と、さまざまな種類のアナライザーおよび重大度レベルについて学習します。
ms.custom: SEO-VS-2020
ms.topic: overview
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
- code analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: c3a7192ac55dc4138746e3e1e1abe4eaa6928395
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798337"
---
# <a name="overview-of-source-code-analysis"></a>ソース コード分析の概要

.NET Compiler Platform (Roslyn) アナライザーを使用して、C# または Visual Basic コードのスタイル、品質、保守容易性、設計、その他の問題を検査します。 この検査または分析は、開いているすべてのファイルの設計時に行われます。

アナライザーは、次のグループに分類できます。

- [コード スタイル](/dotnet/fundamentals/code-analysis/code-style-rule-options?preserve-view=true&view=vs-2019#convention-categories) アナライザーは、Visual Studio に組み込まれています。 これらのアナライザーの診断 ID (コード) は、IDE0067 のように、IDExxxx の形式です。 [テキスト エディターのオプション ページ](../ide/code-styles-and-code-cleanup.md)または [EditorConfig ファイル](/dotnet/fundamentals/code-analysis/code-style-rule-options)で、ユーザー設定を構成できます。 .NET 5.0 以降、コード スタイル アナライザーは .NET SDK に含まれており、ビルドの警告またはエラーとして厳密に適用できます。 詳細については、[このページ](/dotnet/fundamentals/productivity/code-analysis#code-style-analysis)を参照してください。

- [コード品質](/dotnet/fundamentals/code-analysis/quality-rules/index)アナライザーが .NET 5 SDK に含まれるようになり、既定で有効になりました。 これらのアナライザーの診断 ID (コード) は、CA1822 のように、CAxxxx の形式です。 詳細については、[.NET コード品質分析の概要](/dotnet/fundamentals/productivity/code-analysis#code-quality-analysis)に関するページを参照してください。

- サード パーティのアナライザーを NuGet パッケージまたは Visual Studio 拡張機能としてインストールできます。 サード パーティのアナライザーには、[StyleCop](https://www.nuget.org/packages/StyleCop.Analyzers/)、[Roslynator](https://www.nuget.org/packages/Roslynator.Analyzers/)、[XUnit Analyzers](https://www.nuget.org/packages/xunit.analyzers/)、[Sonar Analyzer](https://www.nuget.org/packages/SonarAnalyzer.CSharp/) などがあります。

## <a name="severity-levels-of-analyzers"></a>アナライザーの重要度レベル

各アナライザーには、次の重要度レベルのいずれかがあります。

| 重要度 (ソリューション エクスプローラー) | 重要度 (EditorConfig ファイル) | ビルド時の動作 | エディターの動作 |
|-|-|-|
| エラー | `error` | 違反は、エラー一覧とコマンドラインのビルド出力に "*エラー*" として表示され、ビルドが失敗します。| 問題を起こしているコードには赤色の波線が引かれ、スクロール バーに小さい赤色のボックスが示されます。 |
| 警告 | `warning` | 違反は、エラー一覧とコマンドラインのビルド出力に "*警告*" として表示され、ビルドが失敗します。 | 問題を起こしているコードには緑色の波線が引かれ、スクロール バーに小さい緑色のボックスが示されます。 |
| Info | `suggestion` | 違反は、エラー一覧とコマンドラインに "*メッセージ*" として表示され、コマンドラインのビルド出力には表示されません。 | 問題を起こしているコードには灰色の波線が引かれ、スクロール バーに小さい灰色のボックスが示されます。 |
| [非表示] | `silent` | ユーザーに表示されません。 | ユーザーに表示されません。 ただし、診断は IDE 診断エンジンに報告されます。 |
| なし | `none` | 完全に抑制されます。 | 完全に抑制されます。 |
| Default | `default` | ルールの既定の重要度に対応します。 ルールの既定値を確認するには、プロパティ ウィンドウを調べます。 | ルールの既定の重要度に対応します。 |

アナライザーでルール違反が見つかった場合は、コード エディター (問題のあるコードの下の "*波線*" として) および [エラー一覧] ウィンドウで報告されます。

![[エラー一覧] ウィンドウに表示されるアナライザーの違反](../code-quality/media/code-analysis-error-list.png)

エラー一覧に報告されるアナライザーの違反は、ルールの[重要度レベルの設定](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)と一致します。 また、アナライザーの違反は、コード エディター内の問題を起こしているコードの下に波線で示されます。 次の図は、3 つの違反 &mdash; 1 つのエラー (赤色の波線)、1 つの警告 (緑色の波線)、1 つの候補 (灰色の 3 つの点) を示しています。

![Visual Studio でのコード エディターの波線](media/diagnostics-severity-colors.png)

多くのアナライザー ルール ("*診断*") には、1 つ以上の "*コード修正*" が関連付けられており、これを適用してルール違反を修正できます。 コード修正は、電球アイコン メニューに、他の種類の[クイック アクション](../ide/quick-actions.md)と共に示されます。 これらのコード修正については、「[共通のクイック アクション](../ide/quick-actions.md)」を参照してください。

![アナライザーの違反とクイック アクションのコード修正](../code-quality/media/built-in-analyzer-code-fix.png)

## <a name="configure-analyzer-severity-levels&quot;></a>アナライザーの重要度レベルの構成

アナライザー ルールの重要度 (&quot;*診断*") は、[EditorConfig ファイル](../code-quality/use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file) で、または [電球メニュー](../code-quality/use-roslyn-analyzers.md#set-rule-severity-from-the-light-bulb-menu)から構成できます。

ビルド時にコードを検査し、入力と同時にライブにするようにアナライザーを構成することもできます。 現在のドキュメントのみで実行するか、開いているすべてのドキュメントで実行するか、またはソリューション全体で実行するようにライブ コード分析のスコープを構成できます。 「[方法:ライブ コード分析スコープを構成する](./configure-live-code-analysis-scope-managed-code.md)」をご覧ください。

> [!TIP]
> コード アナライザーからのビルド時のエラーと警告が表示されるのは、アナライザーが NuGet パッケージとしてインストールされている場合のみです。 組み込みアナライザー (たとえば、IDE0067 や IDE0068) はビルド時には実行されません。

## <a name="nuget-package-versus-vsix-extension"></a>NuGet パッケージと VSIX 拡張機能

サード パーティのアナライザーは、NuGet パッケージを使用してプロジェクトごとにインストールできます。 また、Visual Studio の拡張機能として使用できるものもあります。この場合、Visual Studio で開くすべてのソリューションに適用されます。 [アナライザーをインストールする](../code-quality/install-roslyn-analyzers.md)これら 2 つの方法には、主な動作の違いがいくつかあります。

### <a name="scope"></a>スコープ

Visual Studio 拡張機能としてアナライザーをインストールする場合は、ソリューション レベルで Visual Studio のすべてのインスタンスに適用されます。 NuGet パッケージとしてアナライザーをインストールする (推奨される方法) 場合、NuGet パッケージがインストールされたプロジェクトにのみ適用されます。 チーム環境では、NuGet パッケージとしてインストールされたアナライザーは、そのプロジェクトで作業する *すべての開発者* のスコープ内にあります。

### <a name="build-errors"></a>ビルド エラー

コマンド ラインから、または継続的インテグレーション (CI) ビルドの一部としてなど、ビルド時にルールを適用するには、次のいずれかのオプションを選択できます。

- .Net SDK に既定でアナライザーが含まれている .NET 5.0 プロジェクトを作成します。 コード分析は、.NET 5.0 以降を対象とするプロジェクトで既定で有効になっています。 [EnableNETAnalyzers](/dotnet/core/project-sdk/msbuild-props#enablenetanalyzers) プロパティを true に設定すると、以前の .NET バージョンを対象とするプロジェクトでコード分析を有効にできます。

- アナライザーを NuGet パッケージとしてインストールします。 拡張機能としてアナライザーをインストールする場合、アナライザーの警告とエラーはビルド レポートに示されません。

次のイメージは、アナライザー ルール違反を含むプロジェクトのビルドからのコマンドライン ビルド出力を示しています。

![ルール違反を示す MSBuild 出力](media/command-line-build-analyzers.png)

### <a name="rule-severity"></a>ルールの重要度

Visual Studio 拡張機能としてインストールされたアナライザーからルールの重要度を構成することはできません。 [ルールの重要度](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)を構成するには、NuGet パッケージとしてアナライザーをインストールします。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Visual Studio にコード アナライザーをインストールする](../code-quality/install-roslyn-analyzers.md)

> [!div class="nextstepaction"]
> [Visual Studio でコード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>関連項目

- [アナライザーに関する FAQ](analyzers-faq.yml)
- [独自のコード アナライザーを作成する](../extensibility/getting-started-with-roslyn-analyzers.md)
- [.NET Compiler Platform SDK](/dotnet/csharp/roslyn-sdk/)