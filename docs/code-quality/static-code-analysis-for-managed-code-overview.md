---
title: マネージド コードのレガシ分析
ms.date: 06/12/2019
description: Visual Studio でのレガシ分析について説明します。 警告を抑制する方法、手動および自動で分析を実行する方法、チェックイン時とビルド時に分析を実行する方法を示します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: e8d9ddf88086772e0cd21bde856184954bc7143b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867686"
---
# <a name="overview-of-legacy-analysis-for-managed-code-in-visual-studio"></a>Visual Studio でのマネージド コードのレガシ分析の概要

Visual Studio では、マネージド コードのコード分析を 2 とおりの方法で実行できます。[レガシ分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md) (マネージド アセンブリの FxCop 静的分析とも呼ばれます) を使用する方法と、最新の .NET Compiler Platform ベースの[コード アナライザー](../code-quality/roslyn-analyzers-overview.md)を使用する方法です。 このトピックでは、レガシ分析について説明します。 .NET Compiler Platform ベースのコード分析の詳細については、[.NET Compiler Platform ベースのアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)に関する記事をご覧ください。

マネージド コードのコード分析では、マネージド アセンブリが分析され、[.NET デザイン ガイドライン](/dotnet/standard/design-guidelines/)に規定されたプログラミングおよびデザインに関するルールの違反など、アセンブリに関する情報がレポートされます。

分析ツールは、分析中に実行するチェック項目を警告メッセージとして表示します。 警告メッセージは、プログラミングやデザイン上の問題を識別し、可能であれば問題の解決方法を提供します。

> [!NOTE]
> レガシ分析 (静的コード分析) は、Visual Studio の .NET Core および .NET Standard プロジェクトではサポートされていません。 msbuild の一部として .NET Core または .NET Standard プロジェクトでコード分析を実行すると、 **"エラー: CA0055: \<your.dll> のプラットフォームを識別できませんでした"** のようなエラーが表示されます。 .NET Core または .NET Standard プロジェクトのコードを分析するには、代わりに[コード アナライザー](../code-quality/roslyn-analyzers-overview.md)を使用します。

## <a name="ide-integrated-development-environment-integration"></a>IDE (統合開発環境) の統合

プロジェクトでのコード分析は、手動で実行することも、自動的に実行することもできます。

プロジェクトをビルドするたびにコード分析を実行するには、プロジェクトの **[コード分析]** プロパティ ページでそのオプションを選択します。 詳細については、[自動コード分析を有効または無効にする方法](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)に関する記事をご覧ください。

プロジェクトでコード分析を手動で実行するには、メニュー バーで **[分析]**  >  **[コード分析の実行]**  >  **[\<project> でコード分析を実行]** の順に選択します。

## <a name="rule-sets"></a>規則セット

マネージド コード用のコード分析規則は、[規則セット](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)にグループ化されています。 Microsoft 標準ルール セットのいずれかを使用することも、特定のニーズを満たす[カスタム ルール セットを作成](../code-quality/how-to-create-a-custom-rule-set.md)することもできます。

## <a name="suppress-warnings"></a>警告を表示しない

警告が適用されないことを示すと役に立つことがよくあります。 これによって、開発者や、そのコードを後でレビューする担当者は、その警告が既に調査済みであり、抑制されるのかまたは無視されるのかがわかります。

警告のソース内抑制は、カスタム属性を使用して実装します。 警告を抑制するには、次の例のように、属性 `SuppressMessage` をソース コードに追加します。

```csharp
[System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]
Public class MyClass
{
   // code
}
```

詳細については、「[警告を表示しない](../code-quality/in-source-suppression-overview.md)」を参照してください。

::: moniker range="vs-2017"

> [!NOTE]
> プロジェクトを Visual Studio 2017 に移行すると、突然、コード分析の警告が多数表示される場合があります。 警告を修正する準備ができていない場合は、 **[分析]**  >  **[コード分析の実行とアクティブな懸案事項の抑制]** を選択することで、すべての警告を抑制できます。
>
> ![Visual Studio でのコード分析の実行と懸案事項の抑制](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> プロジェクトを Visual Studio 2019 に移行すると、突然、コード分析の警告が多数表示される場合があります。 警告を修正する準備ができていない場合は、 **[分析]**  >  **[アクティブな懸案事項のビルドと抑制]** を選択することで、すべての警告を抑制できます。

::: moniker-end

## <a name="run-code-analysis-as-part-of-check-in-policy"></a>チェックイン ポリシーの一部としてのコード分析の実行

組織的な取り決めとして、チェックインされるすべてのコードが、特定のポリシーを満たしていることが必要な場合があります。 たとえば、次のようなポリシーが考えられます。

- チェックインするコードにビルド エラーが存在しないこと。

- 最新のビルドの一部としてコード分析が実行されていること。

これは、チェックイン ポリシーを指定することにより実現できます。 詳細については、[プロジェクト チェックイン ポリシーによるコード品質の向上](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)に関する記事をご覧ください。

## <a name="team-build-integration"></a>チーム ビルドの統合

ビルド システムの統合機能を使用すると、分析ツールをビルド プロセスの一環として実行できます。 詳細については、「[Azure Pipelines](/azure/devops/pipelines/index?view=vsts&preserve-view=true)」を参照してください。

## <a name="see-also"></a>関連項目

- [.NET Compiler Platform ベースのアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [規則セットを使用したコード分析規則のグループ化](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [方法: 自動コード分析を有効/無効にする](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
