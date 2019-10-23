---
title: FxCop アナライザーの規則セットと editorconfig ファイル
ms.date: 10/08/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzer packages, rule sets
- rule sets for analyzers
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d40e88f123f397cfc77fe44757c2f72305390302
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72606544"
---
# <a name="enable-a-category-of-rules"></a>ルールのカテゴリを有効にする

Analyzer パッケージには、定義済みの[Editorconfig](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)ファイルと[ルールセット](using-rule-sets-to-group-code-analysis-rules.md)ファイルが含まれている場合があります。このファイルを使用すると、セキュリティや設計ルールなどのルールのカテゴリをすばやく簡単に有効にすることができます。 [FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) NuGet analyzer パッケージには、(バージョン2.6.2 以降で始まる) 規則セットと editorconfig ファイル (バージョン2.9.5 以降) の両方が含まれています。 特定のカテゴリのルールを有効にすることで、対象となる問題と特定の条件を特定できます。

> [!NOTE]
> アナライザーの規則を有効にし、EditorConfig ファイルを使用して重要度を設定することは、Visual Studio 2019 バージョン16.3 以降でサポートされています。

FxCop analyzer NuGet パッケージには、次の規則カテゴリの定義済みの規則セットと EditorConfig ファイルが含まれています。

- すべてのルール
- データフロー
- デザイン
- ドキュメント
- グローバリゼーション
- 相互運用性
- やすさ
- 名前付け
- パフォーマンス
- FxCop からの移植
- 信頼性
- セキュリティ
- 使用方法

これらの規則の各カテゴリには、次のように EditorConfig ファイルまたは規則セットファイルがあります。

- カテゴリ内のすべてのルールを有効にします (他のすべてのルールを無効にします)。
- 各ルールの既定の重要度と有効化の設定を使用します (他のすべてのルールを無効にします)。

> [!TIP]
> [すべてのルール] カテゴリには、すべてのルールを無効にするための追加の EditorConfig ファイルまたはルールセットファイルがあります。 このファイルを使用すると、プロジェクト内のアナライザーの警告またはエラーがすぐに除去されます。

> [!TIP]
> 従来の "FxCop" 分析から .NET Compiler Platform ベースのコード分析に移行している場合は、EditorConfig ファイルとルールセットファイルを使用して、[以前に使用したもの](rule-set-reference.md)と同様の規則の構成を引き続き使用することができます。

## <a name="predefined-editorconfig-files"></a>定義済みの EditorConfig ファイル

FxCopAnalyzers analyzer パッケージの定義済み EditorConfig ファイルは、 *% USERPROFILE% \\ nuget\packages\microsoft.codeanalysis.fxcopanalyzers \\ \<version \>/editorconfig にあります。* ディレクトリ。 たとえば、すべてのセキュリティ規則を有効にする EditorConfig ファイルは、 *% USERPROFILE% \\. nuget\packages\microsoft.codeanalysis.fxcopanalyzers \\ \<version \> \ Editorconfig\ securityrules enabled \\ にあります。editorconfig*。

選択した editorconfig ファイルをプロジェクトのルートディレクトリにコピーします。

## <a name="predefined-rule-sets"></a>定義済みの規則セット

FxCopAnalyzers analyzer パッケージの定義済みの規則セットファイルは、 *% USERPROFILE% \\ nuget\packages\microsoft.codeanalysis.fxcopanalyzers \\ \<version \> \ ルール*セットにあります。名簿. たとえば、すべてのセキュリティ規則を有効にする規則セットファイルは、 *% USERPROFILE% \\. nuget\packages\microsoft.codeanalysis.fxcopanalyzers \\ \<version \> \ Ruleset\ securityrules enabledに*あります。

1つ以上の規則セットをコピーし、Visual Studio プロジェクトが格納されているディレクトリまたは**ソリューションエクスプローラー**に直接貼り付けます。

また、[定義済みの規則セット](how-to-create-a-custom-rule-set.md)を自分の好みに合わせてカスタマイズすることもできます。 たとえば、1つまたは複数のルールの重要度を変更して、**エラー一覧**に違反がエラーまたは警告として表示されるようにすることができます。

### <a name="set-the-active-rule-set"></a>アクティブな規則セットを設定する

アクティブな規則セットを設定するプロセスは、.NET Core/.NET Standard プロジェクトと .NET Framework プロジェクトのどちらを使用しているかによって若干異なります。

#### <a name="net-core"></a>.NET Core

.NET Core または .NET Standard プロジェクトで、分析用のアクティブな規則セットを規則に設定するには、 **CodeAnalysisRuleSet**プロパティをプロジェクトファイルに手動で追加します。 たとえば、次のコードスニペットは、`HelloWorld.ruleset` をアクティブな規則セットとして設定します。

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

#### <a name="net-framework"></a>.NET Framework

.NET Framework プロジェクトで分析のためのアクティブな規則セットを規則に設定するには、次のようにします。

- **ソリューションエクスプローラー**でプロジェクトを右クリックし、 **[プロパティ]** を選択します。

- プロジェクトのプロパティページで、 **[コード分析]** タブを選択します。

::: moniker range="vs-2017"

- **[この規則セットを実行]** で、 **[参照]** を選択し、プロジェクトディレクトリにコピーした規則セットを選択します。

::: moniker-end

::: moniker range=">=vs-2019"

- **[アクティブな規則]** で **[参照]** を選択し、プロジェクトディレクトリにコピーした規則セットを選択します。

::: moniker-end

   これで、選択した規則セットで有効になっている規則に対する規則違反のみが表示されるようになりました。

## <a name="see-also"></a>関連項目

- [アナライザーに関する FAQ](analyzers-faq.md)
- [.NET Compiler Platform アナライザーの概要](roslyn-analyzers-overview.md)
- [アナライザーのインストール](install-roslyn-analyzers.md)
- [アナライザーの構成](use-roslyn-analyzers.md)
- [規則セットを使用したコード分析規則のグループ化](using-rule-sets-to-group-code-analysis-rules.md)
