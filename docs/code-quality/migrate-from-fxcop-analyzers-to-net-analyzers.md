---
title: FxCop アナライザーから .NET アナライザーへの移行
ms.custom: SEO-VS-2020
description: FxCop アナライザーから .NET アナライザーに移行する方法について説明します
ms.date: 03/06/2020
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- FxCop, migration
- legacy analysis, migration
- source code analysis, migration
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: d6f9c36b1b64abe648c3aa9014c633e4e4949b1a
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798259"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>FxCop アナライザーから .NET アナライザーへの移行

.NET Compiler Platform ("Roslyn") アナライザーによるソース分析は、マネージド コードの[レガシ分析](code-analysis-for-managed-code-overview.md)に代わるものです。 レガシ分析 (FxCop) 規則の多くは、ソース アナライザーとして既に書き換えられています。

Visual Studio 2019 16.8 および .NET 5.0 より前では、これらのアナライザーは `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)として出荷されていました。

Visual Studio 2019 16.8 および .NET 5.0 以降では、これらのアナライザーは [.NET SDK に含まれています](/dotnet/fundamentals/code-analysis/overview)。 .NET 5 以降の SDK に移行しない場合、または NuGet パッケージベースのモデルを使用する場合は、`Microsoft.CodeAnalysis.NetAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)でアナライザーを入手することもできます。 オンデマンドのバージョン更新には、パッケージベースのモデルを使用することをお勧めします。

> [!NOTE]
> ファーストパーティの .NET アナライザーは、ターゲットプラットフォームに依存しません。 つまり、プロジェクトで特定の .NET プラットフォームをターゲットにする必要はありません。 これらのアナライザーは、`net5.0` のほか、以前のバージョンの .NET (`netcoreapp`、`netstandard`、`net472` など) をターゲットとするプロジェクトで機能します。

## <a name="migration-steps"></a>移行の手順

バージョン `3.3.2` 以降では、`Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet パッケージは非推奨になりました。 次の手順に従って、プロジェクトまたはソリューションを `Microsoft.CodeAnalysis.FxCopAnalyzers` から .NET アナライザーに移行してください。

1. `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet パッケージをアンインストールします。

2. [.NET アナライザーを有効にするか、インストールします](install-net-analyzers.md)。 プロジェクトのターゲット プラットフォームを変更する必要はありません。

3. 追加のルールを有効にします。`Microsoft.CodeAnalysis.NetAnalyzers` は `Microsoft.CodeAnalysis.FxCopAnalyzers` に比べてはるかに保守的です。 FxCopAnalyzers パッケージとは異なり、[ビルドの警告として既定で有効になっている](/dotnet/fundamentals/code-analysis/overview#enabled-rules)正確性規則はごくわずかです。 [AnalysisMode](/dotnet/core/project-sdk/msbuild-props#analysismode) MSBuild プロパティをカスタマイズすることで、[追加のルールを有効にする](/dotnet/fundamentals/code-analysis/overview#enable-additional-rules)ことができます。 たとえば、このプロパティを `AllEnabledByDefault` に設定すると、適用可能なすべての CA ルールがビルドの警告として既定で有効になります。

   ```xml
   <PropertyGroup>
     <AnalysisMode>AllEnabledByDefault</AnalysisMode>
   </PropertyGroup>
   ```

## <a name="see-also"></a>こちらもご覧ください

- [ソース コード分析と従来の分析](net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)
- [レガシ分析から .NET アナライザーへの移行](migrate-from-legacy-analysis-to-net-analyzers.md)
- [.NET アナライザーの有効化またはインストール](install-net-analyzers.md)
- [.NET アナライザーに関する FAQ](net-analyzers-faq.yml)
- [.NET アナライザーの構成](/dotnet/fundamentals/code-analysis/code-quality-rule-options)
