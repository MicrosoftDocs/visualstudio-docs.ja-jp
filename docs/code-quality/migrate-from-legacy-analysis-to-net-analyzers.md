---
title: FxCop からソース分析 (.NET アナライザー) に移行する
ms.custom: SEO-VS-2020
description: コードを初めて分析する方法や、バイナリ分析 (FxCop) から、ソース分析 (.NET アナライザー) を使用したマネージド コードの新しい分析方法に移行する方法について説明します。
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
ms.openlocfilehash: 9a673e7467816e71b8240de9e5f68840c9188dcd
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798233"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-net-analyzers"></a>レガシ分析 (FxCop) からソース分析 (.NET アナライザー) に移行する

.NET Compiler Platform ("Roslyn") アナライザーによるソース分析は、マネージド コードの[レガシ分析](../code-quality/code-analysis-for-managed-code-overview.md)に代わるものです。 .NET Core プロジェクトや .NET Standard プロジェクトなどの新しいプロジェクト テンプレートでは、レガシ分析は使用できません。

レガシ分析 (FxCop) 規則の多くは、.NET アナライザー (Roslyn コード アナライザーのセット) 用に既に書き換えられています。 Roslyn アナライザーでは、コンパイラの実行中にソースコード ベースの分析が実行されます。 アナライザーの結果は、コンパイラーの結果と共に報告されます。

レガシ分析とソース分析の違いの詳細については、次の記事をご覧ください。

- [ソース コード分析と従来の分析](../code-quality/net-analyzers-faq.yml#what-s-the-difference-between-legacy-fxcop-and--net-analyzers-)

- [.NET アナライザーに関する FAQ](../code-quality/net-analyzers-faq.yml)

## <a name="migration"></a>移行

ソース分析に移行するには、[.NET アナライザーを有効にするかインストールします](install-net-analyzers.md)。 従来の分析のルール違反と同様に、ソース コード分析の違反は Visual Studio の [エラー一覧] ウィンドウに表示されます。 さらに、ソース コード分析の違反は、コード エディターで問題のあるコードの下に "*波線*" としても示されます。 波線の色は、ルールの[重要度設定](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)によって異なります。 新しい .NET アナライザーに移植されたルールの状態を確認するには、[移植されたルールと移植されていないルール](../code-quality/fxcop-rule-port-status.md)に関する記事をご覧ください。

> [!NOTE]
> Visual Studio 2019 16.8 および .NET 5.0 より前では、これらのアナライザーは `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)として出荷されていました。 Visual Studio 2019 16.8 および .NET 5.0 以降では、これらのアナライザーは [.NET SDK に含まれています](/dotnet/fundamentals/code-analysis/overview)。 これらは、`Microsoft.CodeAnalysis.NetAnalyzers` [NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)として入手することもできます。 詳細については、「[FxCop アナライザーから .NET アナライザーに移行する](migrate-from-fxcop-analyzers-to-net-analyzers.md)」をご覧ください。

## <a name="configuration"></a>構成

.NET アナライザーの構成方法の詳細を確認するには:

- .NET アナライザーを構成するには、[.NET アナライザーの構成](/dotnet/fundamentals/code-analysis/code-quality-rule-options)に関する記事をご覧ください。

- EditorConfig またはルール セット ファイルで定義済みのルールを使用してアナライザーを構成する方法については、[ルールのカテゴリの有効化](/dotnet/fundamentals/code-analysis/code-quality-rule-options)に関する記事をご覧ください。

## <a name="see-also"></a>こちらもご覧ください

- [FxCop アナライザーから .NET アナライザーへの移行](migrate-from-fxcop-analyzers-to-net-analyzers.md)
