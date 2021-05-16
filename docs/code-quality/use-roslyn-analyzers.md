---
title: アナライザーの構成
ms.date: 09/02/2020
description: Roslyn アナライザーのルールをカスタマイズする方法について学びます。 アナライザーの重要度を調整する方法、違反を抑制する方法、および生成されたコードとしてファイルを指定する方法を確認します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 956e63384619a82b7f0abb7dd3771ed2db9cba01
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101684374"
---
# <a name="overview"></a>概要

各 Roslyn アナライザーの "*診断*" すなわちルールには、既定の重要度と抑制の状態がありますが、これらはプロジェクトのために上書きしたりカスタマイズしたりできます。 この記事では、アナライザーの重要度の設定と、アナライザーの違反の抑制について説明します。

## <a name="configure-severity-levels"></a>重要度レベルを構成する

::: moniker range=">=vs-2019"

Visual Studio 2019 バージョン 16.3 以降では、アナライザーのルールすわなち "*診断*" の重要度を、[EditorConfig ファイル](#set-rule-severity-in-an-editorconfig-file)、[電球メニュー](#set-rule-severity-from-the-light-bulb-menu)、およびエラー一覧で構成できます。

::: moniker-end

::: moniker range="vs-2017"

NuGet パッケージとして [アナライザーをインストール](../code-quality/install-roslyn-analyzers.md)した場合は、アナライザーのルールすなわち "*診断*" の重要度を構成できます。 ルールの重要度は、[ソリューション エクスプローラー](#set-rule-severity-from-solution-explorer)または[ルール セット ファイル内](#set-rule-severity-in-the-rule-set-file)で変更できます。

::: moniker-end

次の表は、さまざまな重要度のオプションを示しています。

| 重要度 (ソリューション エクスプローラー) | 重要度 (EditorConfig ファイル) | ビルド時の動作 | エディターの動作 |
|-|-|-|
| エラー | `error` | 違反は、エラー一覧とコマンドラインのビルド出力に "*エラー*" として表示され、ビルドが失敗します。| 問題を起こしているコードには赤色の波線が引かれ、スクロール バーに小さい赤色のボックスが示されます。 |
| 警告 | `warning` | 違反は、エラー一覧とコマンドラインのビルド出力に "*警告*" として表示され、ビルドが失敗します。 | 問題を起こしているコードには緑色の波線が引かれ、スクロール バーに小さい緑色のボックスが示されます。 |
| Info | `suggestion` | 違反は、エラー一覧とコマンドラインに "*メッセージ*" として表示され、コマンドラインのビルド出力には表示されません。 | 問題を起こしているコードには灰色の波線が引かれ、スクロール バーに小さい灰色のボックスが示されます。 |
| [非表示] | `silent` | ユーザーに表示されません。 | ユーザーに表示されません。 ただし、診断は IDE 診断エンジンに報告されます。 |
| なし | `none` | 完全に抑制されます。 | 完全に抑制されます。 |
| Default | `default` | ルールの既定の重要度に対応します。 ルールの既定値を確認するには、プロパティ ウィンドウを調べます。 | ルールの既定の重要度に対応します。 |

アナライザーでルール違反が見つかった場合は、コード エディター (問題のあるコードの下の "*波線*" として) および [エラー一覧] ウィンドウで報告されます。

エラー一覧に報告されるアナライザーの違反は、ルールの[重要度レベルの設定](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)と一致します。 また、アナライザーの違反は、コード エディター内の問題を起こしているコードの下に波線で示されます。 次の図は、3 つの違反 &mdash; 1 つのエラー (赤色の波線)、1 つの警告 (緑色の波線)、1 つの候補 (灰色の 3 つの点) を示しています。

![Visual Studio でのコード エディターの波線](media/diagnostics-severity-colors.png)

次のスクリーンショットには、エラー一覧に表示されるのと同じ 3 つの違反が示されています。

![エラー一覧のエラー、警告、および情報の違反](media/diagnostics-severities-in-error-list.png)

多くのアナライザー ルール ("*診断*") には、1 つ以上の "*コード修正*" が関連付けられており、これを適用してルール違反を修正できます。 コード修正は、電球アイコン メニューに、他の種類の[クイック アクション](../ide/quick-actions.md)と共に示されます。 これらのコード修正については、「[共通のクイック アクション](../ide/quick-actions.md)」を参照してください。

![アナライザーの違反とクイック アクションのコード修正](../code-quality/media/built-in-analyzer-code-fix.png)

### <a name="hidden-severity-versus-none-severity"></a>'Hidden' 重要度および 'None' 重要度

既定で有効になっている `Hidden` 重要度のルールは、無効すなわち `None` 重要度のルールとは 2 つの点で異なります。

- `Hidden` 重要度のルールに対してコード修正が登録されている場合、非表示の診断がユーザーに表示されませんが、Visual Studio で電球のコード リファクタリング アクションとして修正が提供されます。 これは、無効になっている `None` 重要度のルールには当てはまりません。
- `Hidden` 重要度ルールは、[EditorConfig ファイル内で一度に複数のアナライザー ルールのルール重要度を設定](#set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file)するエントリによって一括構成できます。 `None` 重要度ルールをこのように構成することはできません。 代わりに、[ルール ID ごとに EditorConfig ファイルでルールの重要度を設定](#set-rule-severity-in-an-editorconfig-file)するエントリを使用して構成する必要があります。

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>EditorConfig ファイルでルールの重要度を設定する

(Visual Studio 2019 バージョン 16.3 以降)

次の構文を使用して、EditorConfig ファイルでコンパイラの警告またはアナライザーのルールの重要度を設定できます。

`dotnet_diagnostic.<rule ID>.severity = <severity>`

EditorConfig ファイルでのルールの重要度の設定は、ルール セットまたはソリューション エクスプローラーで設定される重要度よりも優先されます。 EditorConfig ファイルで重要度を[手動で](#manually-configure-rule-severity-in-an-editorconfig-file)構成することも、違反の横に表示される電球を使用して[自動的に](#set-rule-severity-from-the-light-bulb-menu)構成することもできます。

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>EditorConfig ファイルで一度に複数のアナライザー ルールのルール重要度を設定する

(Visual Studio 2019 バージョン 16.5 以降)

EditorConfig ファイルの 1 つのエントリで、特定のカテゴリのアナライザー ルールの重要度を設定することも、すべてのアナライザー ルールの重要度を設定することもできます。

- あるカテゴリのアナライザー ルールのルール重要度を設定します。

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- すべてのアナライザー ルールのルール重要度を設定します。

`dotnet_analyzer_diagnostic.severity = <severity>`

> [!NOTE]
> 一度に複数のアナライザー ルールを構成するエントリは、"*既定で有効*" になっているルールにのみ適用されます。 アナライザー パッケージで既定で無効とマークされているアナライザー ルールは、明示的な `dotnet_diagnostic.<rule ID>.severity = <severity>` エントリを使用して有効にする必要があります。

特定のルール ID に適用できるエントリが複数ある場合、該当するエントリを選択するための優先順位は次のとおりです。

- ID に基づく個々のルールに対する重要度エントリは、カテゴリに対する重要度エントリよりも優先されます。
- カテゴリに対する重要度エントリは、すべてのアナライザー ルールに対する重要度エントリよりも優先されます。

次の EditorConfig の例を考えてみましょう。[CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) はカテゴリが "パフォーマンス" に指定されています。

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

前の例では、3 つのエントリすべてが CA1822 に適用できます。 ただし、指定した優先順位ルールを使用すると、最初のルール ID ベースの重要度エントリが次のエントリに優先されます。 この例の場合、CA1822 の有効な重要度は "error" です。 "パフォーマンス" カテゴリのその他すべてのルールの重要度は "warning" になります。 "パフォーマンス" カテゴリではないその他すべてのアナライザー ルールの重要度は "suggestion" になります。

#### <a name="manually-configure-rule-severity-in-an-editorconfig-file"></a>EditorConfig ファイルでルール重要度を手動で構成する

1. プロジェクトの EditorConfig ファイルがまだない場合は、[1 つ追加](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)します。

2. 対応するファイル拡張子の下に、構成するルールごとにエントリを追加します。 たとえば、[CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) の重要度を C# ファイルについて `error` と設定する場合、エントリは次のようになります。

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> IDE コードスタイルのアナライザーでは、別の構文を使用して、EditorConfig ファイルに構成することもできます (例: `dotnet_style_qualification_for_field = false:suggestion`)。 ただし、`dotnet_diagnostic` 構文を使用して重要度を設定した場合は、そちらが優先されます。 詳細については、[EditorConfig の言語規則](/dotnet/fundamentals/code-analysis/style-rules/language-rules)に関するページを参照してください。

### <a name="set-rule-severity-from-the-light-bulb-menu"></a>電球メニューでルールの重要度を設定する

Visual Studio には、[クイック アクション](../ide/quick-actions.md)の電球メニューからルールの重要度を構成する便利な方法が用意されています。

1. 違反が発生した後、エディターで違反の波線をポイントし、電球メニューを開きます。 または、その行にカーソルを置き、**Ctrl**+ **.** (ピリオド) を押します。

2. 電球メニューで、 **[問題の構成または抑制]** > **[構成] \<rule ID> [重要度]** を選択します。

   ![Visual Studio の電球メニューでルールの重要度を構成する](media/configure-rule-severity.png)

3. そこで、重要度オプションのいずれかを選択します。

   ![ルールの重要度を Suggestion として構成する](media/configure-rule-severity-suggestion.png)

   Visual Studio によって EditorConfig ファイルにエントリが追加され、プレビュー ボックスに示されているように、要求されたレベルのルールが構成されます。

   > [!TIP]
   > プロジェクトに EditorConfig ファイルがまだない場合、Visual Studio によって作成されます。

### <a name="set-rule-severity-from-the-error-list-window"></a>[エラー一覧] ウィンドウでルールの重要度を設定する

また、Visual Studio では、[エラー一覧] のコンテキスト メニューからルールの重要度を構成する便利な方法も提供されています。

1. 違反が発生した後で、[エラー一覧] の診断エントリを右クリックします。

2. コンテキスト メニューで、 **[重要度の設定]** を選択します。

   ![Visual Studio の [エラー一覧] でルールの重要度を構成する](media/configure-rule-severity-error-list.png)

3. そこで、重要度オプションのいずれかを選択します。

   Visual Studio によって EditorConfig ファイルにエントリが追加され、要求されたレベルのルールが構成されます。

   > [!TIP]
   > プロジェクトに EditorConfig ファイルがまだない場合、Visual Studio によって作成されます。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>ルールの重要度をソリューション エクスプローラーで設定する

**ソリューション エクスプローラー** で、アナライザー診断のカスタマイズの多くを行うことができます。 NuGet パッケージとして [アナライザーをインストール](../code-quality/install-roslyn-analyzers.md)すると、**ソリューション エクスプローラー** で **[参照]** または **[依存関係]** ノードの下に **[アナライザー]** ノードが表示されます。 **[アナライザー]** を展開してから、アナライザー アセンブリの 1 つを展開すると、そのアセンブリ内のすべての診断が表示されます。

![ソリューション エクスプローラーの [アナライザー] ノード](media/analyzers-expanded-in-solution-explorer.png)

**[プロパティ]** ウィンドウに、説明や既定の重要度など、診断のプロパティが表示されます。 プロパティを表示するには、ルールを右クリックして **[プロパティ]** を選択するか、ルールを選択してから **Alt**+**Enter** キーを押します。

![[プロパティ] ウィンドウの [診断のプロパティ]](media/analyzer-diagnostic-properties.png)

診断のオンラインドキュメントを表示するには、診断を右クリックし、 **[ヘルプの表示]** を選択します。

**ソリューション エクスプローラー** の各診断の横にあるアイコンは、エディターで開いたときにルール セットに表示されるアイコンと対応しています。

- 円の中の "x" は、[重要度](#configure-severity-levels) **Error** を示します。
- 三角形の中の "!" は、[重要度](#configure-severity-levels) **Warning** を示します。
- 円の中の "i" は、[重要度](#configure-severity-levels) **Info** を示します。
- 白抜きの円の中の "i" は、[重要度](#configure-severity-levels) **Hidden** を示します。
- 円の中の下向き矢印は、診断が抑制されていることを示します。

![ソリューション エクスプローラーの診断アイコン](media/diagnostics-icons-solution-explorer.png)

::: moniker range=">=vs-2019"

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>既存のルール セット ファイルを EditorConfig ファイルに変換する

Visual Studio 2019 バージョン 16.5 以降では、ルール セット ファイルは非推奨になり、マネージド コードのアナライザー構成で EditorConfig ファイルが優先されます。 アナライザーのルールの重要度を構成するための Visual Studio ツールのほとんどが、ルール セット ファイルではなく EditorConfig ファイルで動作するように更新されました。 EditorConfig ファイルを使用すると、Visual Studio IDE のコード スタイル オプションを含め、アナライザーのルールの重要度とアナライザーのオプションの両方を構成できます。 既存のルール セット ファイルを EditorConfig ファイルに変換することを強くお勧めします。 また、EditorConfig ファイルは、リポジトリのルートまたはソリューション フォルダーに保存することをお勧めします。 リポジトリのルートまたはソリューション フォルダーを使用すると、このファイルの重要度設定が、それぞれリポジトリ全体またはソリューション全体に自動的に適用されるようになります。

既存のルール セット ファイルを EditorConfig ファイルに変換するには、いくつかの方法があります。

- Visual Studio のルール セット エディターで (Visual Studio 2019 16.5 以降が必要)。 特定のルール セット ファイルが `CodeAnalysisRuleSet` としてプロジェクトで既に使用されている場合、Visual Studio 内のルール セット エディターで同等の EditorConfig ファイルに変換できます。

    1. ソリューション エクスプローラーでルール セット ファイルをダブルクリックします。

       ルール セット エディターでルール セット ファイルが開きます。 ルール セット エディターの上部にクリック可能な **情報バー** が表示されます。

       ![ルール セット エディターでルール セットを EditorConfig ファイルに変換する](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. **情報バー** のリンクを選択します。

       これで、 **[名前を付けて保存]** ダイアログ ボックスが開くので、ここで EditorConfig ファイルを生成するディレクトリを選択します。

    3. **[保存]** ボタンを選択して、EditorConfig ファイルを生成します。

       生成された EditorConfig がエディターで開きます。 また、MSBuild プロパティ `CodeAnalysisRuleSet` がプロジェクト ファイルで更新され、元のルール セット ファイルが参照されなくなります。

- コマンドラインから:

    1. NuGet パッケージ [Microsoft CodeAnalysis. RulesetToEditorconfigConverter](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter) をインストールします。

    2. ルール セット ファイルと EditorConfig ファイルへのパスをコマンドライン引数として、インストールしたパッケージの `RulesetToEditorconfigConverter.exe` を実行します。

   ```
   Usage: RulesetToEditorconfigConverter.exe <%ruleset_file%> [<%path_to_editorconfig%>]
   ```

変換するルール セット ファイルの例を次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules for ConsoleApp" Description="Code analysis rules for ConsoleApp.csproj." ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1821" Action="Warning" />
    <Rule Id="CA2213" Action="Warning" />
    <Rule Id="CA2231" Action="Warning" />
  </Rules>
</RuleSet>
```

変換された EditorConfig ファイルを次に示します。

```ini
# NOTE: Requires **VS2019 16.3** or later

# Rules for ConsoleApp
# Description: Code analysis rules for ConsoleApp.csproj.

# Code files
[*.{cs,vb}]


dotnet_diagnostic.CA1001.severity = warning

dotnet_diagnostic.CA1821.severity = warning

dotnet_diagnostic.CA2213.severity = warning

dotnet_diagnostic.CA2231.severity = warning
```
::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>ルールの重要度をソリューション エクスプローラーで設定する

1. ソリューション エクスプローラーで、 **[参照]**  >  **[アナライザー]** (または .NET Core プロジェクトでは **[依存関係]**  >  **[アナライザー]** ) を展開します。

2. 重要度を設定するルールが含まれているアセンブリを展開します。

::: moniker range=">=vs-2019"
3. 右クリックし、 **[重要度の設定]** を選択します。 コンテキスト メニューで、重要度オプションの 1 つを選択します。

   Visual Studio によって EditorConfig ファイルにエントリが追加され、要求されたレベルのルールが構成されます。 プロジェクトで EditorConfig ファイルではなくルール セット ファイルが使用されている場合、重要度エントリがルール セット ファイルに追加されます。

   > [!TIP]
   > プロジェクトに EditorConfig ファイルまたはルール セット ファイルがまだない場合は、Visual Studio によって新しい EditorConfig ファイルが作成されます。
::: moniker-end

::: moniker range="vs-2017"
3. ルールを右クリックし、 **[ルール セットの重要度を設定]** を選択します。 コンテキスト メニューで、重要度オプションの 1 つを選択します。

   ルールの重要度が、アクティブなルール セット ファイルに保存されます。
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>ルール セット ファイルでルールの重要度を設定する

![ソリューション エクスプローラーのルール セット ファイル](media/ruleset-in-solution-explorer.png)

1. 次のいずれかの方法で、アクティブなルール セット ファイルを開きます。

- **ソリューション エクスプローラー** で、ファイルをダブルクリックし、 **[参照]**  >  **[アナライザー]** ノードを右クリックして、 **[アクティブなルール セットを開く]** を選択します。
- プロジェクトの **[コード分析]** プロパティ ページで、 **[開く]** を選択します。

  このとき初めてルール セットを編集する場合は、Visual Studio によって既定のルール セット ファイルのコピーが作成され、 *\<projectname>.ruleset* という名前が付けられてプロジェクトに追加されます。 このカスタム ルール セットが、プロジェクトのアクティブなルール セットにもなります。

   > [!NOTE]
   > .NET Core および .NET Standard のプロジェクトは、**ソリューション エクスプローラー** のルール セットのメニュー コマンド ( **[アクティブなルール セットを開く]** など) に対応していません。 .NET Core または .NET Standard pプロジェクトに対して既定以外のルール セットを指定するには、プロジェクト ファイルに手動で [**CodeAnalysisRuleSet** プロパティを追加](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)します。 ただし、Visual Studio のルール セット エディター UI でルール セット内のルールを構成することはできます。

1. 含まれているアセンブリを展開して、ルールを参照します。

1. **[アクション]** 列で、値を選択してドロップダウン リストを開き、目的の重要度を一覧から選択します。

   ![エディターに開かれたルール セット ファイル](media/ruleset-file-in-editor.png)

::: moniker range=">=vs-2019"

## <a name="configure-generated-code"></a>生成されたコードを構成する

アナライザーは、プロジェクト内のすべてのソース ファイルに対して実行され、それらについて違反を報告します。 ただし、これらの違反は、生成されたコード ファイル (デザイナーで生成されたコード ファイルやビルド システムによって生成された一時ソース ファイルなど) に対しては役に立ちません。ユーザーは、これらのファイルを手動で編集できず、ツールで生成されたこのようなファイルでの違反の修正には関係ありません。

既定では、アナライザーを実行するアナライザー ドライバーによって、特定の名前、ファイル拡張子、または自動生成されたファイル ヘッダーを持つファイルが生成されたコード ファイルとして扱われます。 たとえば、`.designer.cs` または `.generated.cs` で終わるファイル名は、生成されたコードと見なされます。 ただし、このようなヒューリスティックでは、ユーザーのソース コード内で生成されたカスタム コード ファイルをすべて特定できない可能性があります。

Visual Studio 2019 16.5 以降では、エンド ユーザーが、生成されたコードとして扱う特定のファイルやフォルダーを [Editorconfig ファイル](https://editorconfig.org/)で構成できます。 このような構成を追加するには、次の手順に従います。

1. プロジェクトの EditorConfig ファイルがまだない場合は、[1 つ追加](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)します。

2. 特定のファイルやフォルダーに対する `generated_code = true | false` エントリを追加します。 たとえば、名前が `.MyGenerated.cs` で終わるすべてのファイルを生成されたコードとして扱うには、次のエントリを追加します。

   ```ini
   [*.MyGenerated.cs]
   generated_code = true
   ```

::: moniker-end

## <a name="suppress-violations"></a>違反を抑制する

ルール違反を抑制する方法は複数あります。

::: moniker range=">=vs-2019"

- **EditorConfig ファイル** で

  重要度を `none` に設定します。たとえば、`dotnet_diagnostic.CA1822.severity = none` です。

- **[分析]** メニューから

  メニュー バーで **[分析]**  >  **[アクティブな懸案事項のビルドと抑制]** を選択し、現在のすべての違反を抑制します。 これは、"基準" と呼ばれることもあります。

::: moniker-end

::: moniker range="vs-2017"

- **[分析]** メニューから

  メニュー バーで **[分析]**  >  **[コード分析の実行とアクティブな懸案事項の抑制]** を選択し、現在のすべての違反を抑制します。 これは、"基準" と呼ばれることもあります。

::: moniker-end

- **ソリューション エクスプローラー** から

  ルールの重要度を **[なし]** に設定します。

- **ルール セット エディター** から

  名前の横のチェック ボックスをオフにするか、 **[アクション]** を **[なし]** にします。

- **コード エディター** から

  違反があるコード行にカーソルを置き、**Ctrl**+**ピリオド (.)** キーを押して、 **[クイック アクション]** メニューを開きます。 **[Suppress CAXXXX]\(CAXXXX の抑制\)**  >  **[ソース内]/[抑制ファイル内]** を選択します。

  ![[クイック アクション] メニューで診断を抑制する](media/suppress-diagnostic-from-editor.png)

- **[エラー一覧]** から

  抑制するルールを選択し、右クリックして **[抑制]**  >  **[ソース内]/[抑制ファイル内]** を選択します。

  - **[ソース内]** を抑制する場合、 **[変更のプレビュー]** ダイアログが開き、ソース コードに追加された C# [#pragma warning](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) または Visual Basic [#Disable warning](/dotnet/visual-basic/language-reference/directives/directives) ディレクティブが表示されます。

    ![コード ファイルへの #pragma warning の追加のプレビュー](media/pragma-warning-preview.png)

  - **[抑制ファイル内]** を選択すると、 **[変更のプレビュー]** ダイアログが開き、グローバル抑制ファイルに追加された <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性のプレビューが表示されます。

    ![抑制ファイルへの SuppressMessage 属性の追加のプレビュー](media/preview-changes-in-suppression-file.png)

  **[変更のプレビュー]** ダイアログで、 **[適用]** を選択します。

  > [!NOTE]
  > **ソリューション エクスプローラー** に **[抑制]** メニュー オプションが表示されない場合、違反がライブ分析ではなくビルドから発生している可能性があります。 **[エラー一覧]** には、診断すなわちルールの違反が、ライブ コード分析とビルドの両方から表示されます。 ビルド診断は古くなっている可能性があります。たとえば、コードを編集して違反を修正してもリビルドしていない場合、 **[エラー一覧]** でこれらの診断を抑制できません。 ライブ分析すなわち IntelliSense の診断は、最新のソースを使用して常に最新状態であり、 **[エラー一覧]** で抑制できます。 選択から "*ビルド*" 診断を除外するには、 **[エラー一覧]** のソース フィルターを **[ビルド + IntelliSense]** から **[IntelliSense のみ]** に切り替えます。 次に、抑制する診断を選択し、前述の説明に従って続けます。
  >
  > ![Visual Studio の [エラー一覧] のソース フィルター](media/error-list-filter.png)

## <a name="command-line-usage"></a>コマンド ラインの使用

コマンドラインでプロジェクトをビルドするとき、次の条件が満たされた場合に、ルール違反がビルドの出力に表示されます。

- アナライザーが、VSIX 拡張機能としてではなく、.NET SDK を使用するか NuGet パッケージとしてインストールされています。

  .NET SDK を使用してインストールされたアナライザーでは、[アナライザーの有効化](../code-quality/install-net-analyzers.md)が必要になることがあります。 コード スタイルでは、MSBuild プロパティを設定して、[ビルドにコード スタイルを適用](/dotnet/fundamentals/code-analysis/overview#code-style-analysis)することもできます。

- プロジェクトのコードで 1 つ以上のルールの違反があります。

- 違反しているルールの [重要度](#configure-severity-levels)が、**warning** (違反のためにビルドが失敗しない) または **error** (違反のためにビルドが失敗する) に設定されています。

ビルド出力の詳細度は、ルール違反が表示されるかどうかには影響しません。 詳細度が **quiet** でも、ルール違反はビルド出力に表示されます。

> [!TIP]
> *FxCopCmd.exe* を使用したり、msbuild を **RunCodeAnalysis** フラグと一緒に使用したりして、コマンド ラインからレガシ分析を実行することに慣れている場合、これをコード アナライザーで行う方法を次に示します。

msbuild を使用してプロジェクトをビルドするときにコマンド ラインでアナライザーの違反を表示するには、次のようなコマンドを実行します。

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

次のイメージは、アナライザー ルール違反を含むプロジェクトのビルドからのコマンドライン ビルド出力を示しています。

![ルール違反を示す MSBuild 出力](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依存プロジェクト

.NET Core プロジェクトでは、NuGet アナライザーを含むプロジェクトに参照を追加すると、それらのアナライザーも依存プロジェクトに自動的に追加されます。 この動作を無効にするには、たとえば依存プロジェクトが単体テスト プロジェクトの場合であれば、**PrivateAssets** 属性を使用して、参照されるプロジェクトの NuGet パッケージを *.csproj* または *.vbproj* ファイルでプライベートとマークします。

```xml
<PackageReference Include="Microsoft.CodeAnalysis.NetAnalyzers" Version="5.0.0" PrivateAssets="all" />
```

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio のコード アナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [コード アナライザーのバグを送信する](https://github.com/dotnet/roslyn-analyzers/issues)
- [ルール セットを使用する](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [コード分析の警告を抑制する](../code-quality/in-source-suppression-overview.md)
- [コード分析の構成オプション (.NET)](/dotnet/fundamentals/code-analysis/configuration-options)
