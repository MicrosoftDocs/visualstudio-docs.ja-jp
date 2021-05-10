---
title: ファーストパーティの .NET アナライザーを有効またはインストールする
ms.date: 08/03/2018
description: .NET SDK からファーストパーティの .NET アナライザーを有効にする方法、または NuGet パッケージとしてこれらのアナライザーをインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 368fd5bc9c8b7e2659c86b6e3dc69a609da37617
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144664"
---
# <a name="enable-or-install-first-party-net-analyzers"></a>ファーストパーティの .NET アナライザーを有効またはインストールする

## <a name="overview"></a>概要

.NET のコンパイラ プラットフォーム (Roslyn) アナライザーでは、お使いの C# または Visual Basic コードについて、コード品質やコード スタイルに関する問題を検査できます。 ファーストパーティの .NET アナライザーは、**ターゲットプラットフォームに依存しません**。 つまり、プロジェクトで特定の .NET プラットフォームをターゲットにする必要はありません。 これらのアナライザーは、`net5.0` のほか、以前のバージョンの .NET (`netcoreapp`、`netstandard`、`net472` など) をターゲットとするプロジェクトで機能します。

ファーストパーティの .NET アナライザーは、次のいずれかの方法で有効にしたり、インストールしたりすることができます。

- **.NET SDK から有効にする**: Visual Studio 2019 16.8 および .NET 5.0 以降では、これらのアナライザーが [.NET SDK に含まれています](/dotnet/fundamentals/code-analysis/overview)。 分析は、.NET 5.0 以降をターゲットとするプロジェクトで既定で有効になっています。 MSBUILD の [EnableNETAnalyzers](/dotnet/core/project-sdk/msbuild-props#enablenetanalyzers) プロパティを `true` に設定すると、以前の .NET バージョンを対象とするプロジェクトでコード分析を有効にできます。 `EnableNETAnalyzers` を `false` に設定すると、自分のプロジェクトでコード分析を無効にすることもできます。

- **NuGet パッケージとしてインストールする**: .NET 5 以降の SDK に移行しない場合、または NuGet パッケージベースのモデルを使用する場合は、Visual Studio 2019 の `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)でアナライザーを入手することもできます。  オンデマンドのバージョン更新には、パッケージベースのモデルを使用することをお勧めします。 Visual Studio 2017 を使用している場合は、代わりに最新の `2.9.x` バージョンの `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/)をインストールしてください。

> [!NOTE]
> 可能な場合は、`Microsoft.CodeAnalysis.NetAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)をインストールするのではなく、.NET SDK からアナライザーを有効にすることをお勧めします。 .NET SDK からアナライザーを有効にした場合は、SDK を更新するとすぐに、アナライザーのバグ修正と新しいアナライザーが自動的に取得されるようになります。 NuGet モデルでは、最新のバグ修正が必要になるたびに NuGet パッケージを更新する必要があります。 NuGet パッケージはより頻繁に更新されます。

## <a name="see-also"></a>関連項目

- [Visual Studio のコード アナライザーの概要](roslyn-analyzers-overview.md)
- [Visual Studio でコード アナライザーを使用する](use-roslyn-analyzers.md)
- [レガシ分析から .NET アナライザーへの移行](migrate-from-legacy-analysis-to-net-analyzers.md)
- [FxCop アナライザーから .NET アナライザーへの移行](migrate-from-fxcop-analyzers-to-net-analyzers.md)
