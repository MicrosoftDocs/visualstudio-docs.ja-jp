---
title: コード分析規則セット
ms.date: 04/02/2018
description: Visual Studio コード分析の組み込みのルール セットとカスタマイズされたルール セットについて説明します。 ファイル内でルール セットを指定する方法と、プロジェクトでルール セットを構成する方法を示します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 980c77067ac237dba13c8c888c358a0adeab6d1f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859659"
---
# <a name="use-rule-sets-to-group-code-analysis-rules"></a>ルール セットを使用してコード分析規則をグループ化する

Visual Studio でコード分析を構成するときに、組み込みの "*ルール セット*" の一覧から選択できます。 ルール セットとは、そのプロジェクトの対象となる問題と特定の条件を示すコード分析規則のグループです。 たとえば、公開されている API のコードをスキャンすることを目的としたルール セットを適用できます。 また、使用可能なすべてのルールが含まれたルール セットを適用することもできます。

ルールを追加または削除したり、 **[エラー一覧]** に警告またはエラーとして表示するためにルールの重大度を変更したりすることで、ルール セットをカスタマイズできます。 カスタマイズした規則セットで、特定の開発環境の要件を満たすことができます。 ルール セットをカスタマイズする場合、ルール セット エディターには、このプロセスで役立つ検索ツールとフィルター処理ツールが用意されています。

ルール セットは、[マネージド コード分析](/dotnet/fundamentals/code-analysis/code-quality-rule-options)、[マネージド コードのレガシ分析](how-to-configure-code-analysis-for-a-managed-code-project.md)、[C++ コード分析](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run)に使用できます。

## <a name="rule-set-format"></a>ルール セットの形式

ルール セットは、 *.ruleset* ファイルに XML 形式で指定されます。 ID と "*アクション*" で構成されるルールは、ファイル内でアナライザー ID と名前空間でグループ化されます。

*.ruleset* ファイルの内容は、この XML のようになります。

```xml
<RuleSet Name="Rules for Hello World project" Description="These rules focus on critical issues for the Hello World app." ToolsVersion="10.0">
  <Localization ResourceAssembly="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.dll" ResourceBaseName="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.Localized">
    <Name Resource="HelloWorldRules_Name" />
    <Description Resource="HelloWorldRules_Description" />
  </Localization>
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1009" Action="Warning" />
    <Rule Id="CA1016" Action="Warning" />
    <Rule Id="CA1033" Action="Warning" />
  </Rules>
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1802" Action="Error" />
    <Rule Id="CA1814" Action="Info" />
    <Rule Id="CA1823" Action="None" />
    <Rule Id="CA2217" Action="Warning" />
  </Rules>
</RuleSet>
```

> [!TIP]
> 手動よりも、グラフィカルな **ルール セット エディター** で[ルール セットを編集](../code-quality/working-in-the-code-analysis-rule-set-editor.md)する方が簡単です。

## <a name="specify-a-rule-set-for-a-project"></a>プロジェクトのルール セットを指定する

プロジェクトのルール セットは、Visual Studio プロジェクト ファイルの **CodeAnalysisRuleSet** プロパティで指定します。 次に例を示します。

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

## <a name="see-also"></a>関連項目

- [コード分析規則セットの参照](../code-quality/rule-set-reference.md)