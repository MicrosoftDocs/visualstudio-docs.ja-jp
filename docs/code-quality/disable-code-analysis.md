---
title: コード分析を無効にする
ms.date: 09/01/2020
description: .NET Core、.NET Standard、.NET Framework の各プロジェクトで、Visual Studio のソース コード分析を無効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.openlocfilehash: 6a1f1466caa921d46ce4701f5074b98f3d5ba051
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860387"
---
# <a name="disable-source-code-analysis-for-net"></a>.NET のソース コード分析を無効にする

::: moniker range=">=vs-2019"

このページは、Visual Studio でコード分析を無効にする際に役立ちます。 無効にできるものには制限があり、コード分析を無効にする手順はいくつかの要素によって異なります。

- プロジェクトの種類 (.NET Core および Standard と .NET Framework)

  .NET Core および .NET Standard プロジェクトの [コード分析] のプロパティ ページには、NuGet パッケージとしてインストールされたアナライザーのコード分析を無効にできるオプションがあります。 詳細については、「[.NET Core および .NET Standard プロジェクト](#net-core-and-net-standard-projects)」を参照してください。 .NET Framework プロジェクトのソース コード分析を無効にするには、「[.NET Framework プロジェクト](#net-framework-projects)」を参照してください。

- ソース分析とレガシ分析

  このトピックは、レガシ (バイナリ) 分析ではなく、ソース コード分析に適用されます。 レガシ分析を無効にする方法については、[レガシ コード分析を有効または無効にする方法](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)に関する記事を参照してください。

## <a name="net-core-and-net-standard-projects"></a>.NET Core および .NET Standard プロジェクト

Visual Studio 2019 バージョン 16.3 以降では、[コード分析] のプロパティ ページに、ビルド時およびデザイン時にアナライザーを実行するかどうかを制御できる 2 つのチェック ボックスがあります。 これらのオプションはプロジェクト固有です。

![Visual Studio でライブ コード分析またはビルド時の分析を有効または無効にする](media/run-on-build-run-live-analysis.png)

このページを開くには、**ソリューション エクスプローラー** でプロジェクト ノードを右クリックし、 **[プロパティ]** を選択します。 **[コード分析]** タブを選択します。

- ビルド時のソース分析を無効にするには、 **[ビルド時に実行]** オプションをオフにします。
- ライブ ソース分析を無効にするには、 **[ライブ分析時に実行]** オプションをオフにします。

> [!NOTE]
> Visual Studio 2019 バージョン 16.5 以降では、オンデマンドのコード分析実行ワークフローの方がよい場合は、ライブ分析時やビルド時のアナライザーの実行を無効にして、オンデマンドでプロジェクトまたはソリューションに対してコード分析を手動で 1 回トリガーできます。 コード分析を手動で実行する方法については、[マネージド コードのコード分析を手動で実行する方法](how-to-run-code-analysis-manually-for-managed-code.md)に関する記事を参照してください。

## <a name="net-framework-projects"></a>.NET Framework プロジェクト

アナライザーのソース コード分析を無効にするには、[プロジェクト ファイル](../ide/solutions-and-projects-in-visual-studio.md#project-file)に次の MSBuild プロパティを 1 つ以上追加します。

| MSBuild のプロパティ | 説明 | Default |
| - | - | - |
| `RunAnalyzersDuringBuild` | アナライザーをビルド時に実行するかどうかを制御します。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | アナライザーでデザイン時にコードをライブ分析するかどうかを制御します。 | `true` |
| `RunAnalyzers` | ビルド時とデザイン時の両方でアナライザーを無効にします。 このプロパティは、`RunAnalyzersDuringBuild` および `RunAnalyzersDuringLiveAnalysis` よりも優先されます。 | `true` |

例 :

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>ソース解析

Visual Studio 2017 では、[ソース分析](roslyn-analyzers-overview.md)を無効にすることはできません。 **エラー一覧** からアナライザーのエラーをクリアする場合は、メニュー バーの **[分析]**  >  **[コード分析の実行とアクティブな懸案事項の抑制]** を選択することで、現在のすべての違反を非表示にできます。 詳細については、「[違反を抑制する](use-roslyn-analyzers.md#suppress-violations)」を参照してください。

Visual Studio 2019 バージョン 16.3 以降では、ソース コード分析を無効にしたり、オンデマンドで実行したりできます。 Visual Studio 2019 へのアップグレードを検討してください。

## <a name="legacy-analysis"></a>レガシ分析

**[コード分析]** のプロパティ ページで、ビルド時のレガシ分析を無効にすることができます。 詳細については、[レガシ コード分析を有効または無効にする方法](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)に関する記事を参照してください。

::: moniker-end

## <a name="see-also"></a>関連項目

- [違反を抑制する](use-roslyn-analyzers.md#suppress-violations)
- [方法: レガシ コード分析を有効または無効にする](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
