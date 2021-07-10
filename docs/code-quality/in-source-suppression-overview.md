---
title: コード分析の違反を抑制する
ms.date: 05/10/2021
description: Visual Studio でコード分析の違反を抑制する方法について説明します。 ソース内での抑制に SuppressMessageAttribute 属性を使用する方法を説明します。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: fd177a96b8789760927933fad5c0320553a72f57
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973344"
---
# <a name="suppress-code-analysis-violations"></a>コード分析の違反を抑制する

警告が適用されないことを示すと役に立つことがよくあります。 これは、コードがレビューされたことと、警告を抑制できることを、チーム メンバーに示します。 この記事では、Visual Studio IDE を使用してコード分析の違反を抑制するさまざまな方法について説明します。

::: moniker range=">=vs-2019"

## <a name="suppress-violations-using-the-editorconfig-file"></a>EditorConfig ファイルを使用して違反を抑制する

**EditorConfig ファイル** で、重要度を `none` (たとえば `dotnet_diagnostic.CA1822.severity = none` に) 設定します。 EditorConfig ファイルを追加するには、「[EditorConfig ファイルをプロジェクトに追加する](../ide/create-portable-custom-editor-options.md#add-and-remove-editorconfig-files)」を参照してください。

::: moniker-end

## <a name="suppress-violations-in-source-code"></a>ソース コードの違反を抑制する

プリプロセッサ ディレクティブである [#pragma warning (C#)](/dotnet/csharp/language-reference/preprocessor-directives.md#pragma-warning) または [Disable (Visual Basic)](/dotnet/visual-basic/language-reference/directives/disable-enable.md) ディレクティブを使用してコード内の違反を抑制し、特定のコード行についてのみ警告を抑制することができます。 または、[SuppressMessage 属性](#in-source-suppression-and-the-suppressmessage-attribute)を使用することもできます。

- **コード エディター** から

  違反があるコード行にカーソルを置き、**Ctrl**+**ピリオド (.)** キーを押して、 **[クイック アクション]** メニューを開きます。 **[CAXXXX の非表示]** を選択し、 **[ソース内]** または **[in Source (attribute)]\(ソース内 (属性)\)** を選択します。

  **[ソース内]** を選択した場合は、コードに追加されるプリプロセッサ ディレクティブのプレビューが表示されます。

  ::: moniker range="vs-2017"
  :::image type="content" source="media/suppress-diagnostic-from-editor.png" alt-text="[クイック アクション] メニューで診断を抑制する":::
  ::: moniker-end
  ::: moniker range=">=vs-2019"
  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor.png" alt-text="[クイック アクション] メニューで診断を抑制する":::

  **[in Source (attribute)]\(ソース内 (属性)\)** を選択した場合は、コードに追加される [SuppressMessage attribute](#in-source-suppression-and-the-suppressmessage-attribute) のプレビューが表示されます。

  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor-attribute.png" alt-text="属性を使用してクイック アクション メニューから診断を抑制する":::
  ::: moniker-end

- **[エラー一覧]** から

  抑制するルールを選択し、右クリックして **[抑制]**  >  **[ソース内]** を選択します。

  - **[ソース内]** を抑制する場合、 **[変更のプレビュー]** ダイアログが開き、ソース コードに追加された C# [#pragma warning](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) または Visual Basic [#Disable warning](/dotnet/visual-basic/language-reference/directives/directives) ディレクティブが表示されます。

    ![コード ファイルへの #pragma warning の追加のプレビュー](media/pragma-warning-preview.png)

  **[変更のプレビュー]** ダイアログで、 **[適用]** を選択します。

  > [!NOTE]
  > **ソリューション エクスプローラー** に **[抑制]** メニュー オプションが表示されない場合、違反がライブ分析ではなくビルドから発生している可能性があります。 **[エラー一覧]** には、診断すなわちルールの違反が、ライブ コード分析とビルドの両方から表示されます。 ビルド診断は古くなっている可能性があります。たとえば、コードを編集して違反を修正してもリビルドしていない場合、 **[エラー一覧]** でこれらの診断を抑制できません。 ライブ分析すなわち IntelliSense の診断は、最新のソースを使用して常に最新状態であり、 **[エラー一覧]** で抑制できます。 選択から "*ビルド*" 診断を除外するには、 **[エラー一覧]** のソース フィルターを **[ビルド + IntelliSense]** から **[IntelliSense のみ]** に切り替えます。 次に、抑制する診断を選択し、前述の説明に従って続けます。
  >
  > ![Visual Studio の [エラー一覧] のソース フィルター](media/error-list-filter.png)

## <a name="suppress-violations-using-a-global-suppression-file"></a>グローバル抑制ファイルを使用して違反を抑制する

[グローバル抑制ファイル](#global-level-suppressions)には [SuppressMessage 属性](#in-source-suppression-and-the-suppressmessage-attribute)を使用します。

- **エラー一覧** から抑制するルールを選択し、右クリックして **[抑制]**  >  **[抑制ファイル内]** を選択します。 **[変更のプレビュー]** ダイアログが開き、グローバル抑制ファイルに追加された <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性のプレビューが表示されます。

  ![抑制ファイルへの SuppressMessage 属性の追加のプレビュー](media/preview-changes-in-suppression-file.png)

- **コード エディター** から、違反のあるコード行にカーソルを置き、 **[クイック アクションとリファクタリング]** (または **Ctrl**+**Period (.)** キー) を押して、 **[クイック アクション]** メニューを開きます。 **[CAXXXX の抑制]** を選択し、 **[抑制ファイル内]** を選択します。 作成または変更される[グローバル抑制ファイル](#global-level-suppressions)のプレビューが表示されます。

::: moniker range=">=vs-2019"

- **[分析]** メニューから、メニュー バーの **[分析]**  >  **[アクティブな懸案事項のビルドと抑制]** を選択し、現在のすべての違反を抑制します。 これは、"基準" と呼ばれることもあります。

::: moniker-end
::: moniker range="vs-2017"

- **[分析]** メニューから、メニュー バーの **[分析]**  >  **[コード分析の実行とアクティブな懸案事項の抑制]** を選択し、現在のすべての違反を抑制します。 これは、"基準" と呼ばれることもあります。
::: moniker-end

## <a name="suppress-violations-using-project-settings"></a>プロジェクト設定を使用して違反を抑制する

**ソリューション エクスプローラー** から、プロジェクトのプロパティを開きます (プロジェクトを右クリックして **[プロパティ]** を選択します (または **Alt + Enter** キーを押します))。次に **[コード分析]** タブを使用してオプションを構成します。 たとえば、ライブ コード分析を無効にしたり、.NET アナライザーを無効にしたりすることができます。

## <a name="suppress-violations-using-a-rule-set"></a>ルール セットを使用して違反を抑制する

**ルール セット エディター** から、名前の横のチェック ボックスをオフにするか、 **[アクション]** を **[なし]** に設定します。

## <a name="in-source-suppression-and-the-suppressmessage-attribute"></a>ソース内抑制と SuppressMessage 属性

ソース内抑制 (ISS) では、警告を抑制するために <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性を使用します。 この属性は、警告が生成されたコード セグメントの近くに配置できます。 入力することによってソース ファイルに <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性を追加するか、 **[エラー一覧]** の警告のショートカット メニューを使用して自動的に追加することができます。

<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性は条件付き属性であり、コンパイル時に CODE_ANALYSIS コンパイル シンボルが定義されている場合にのみ、マネージド コード アセンブリの IL メタデータに組み込まれます。

C++/CLI で属性を追加するには、ヘッダー ファイルでマクロ CA\_SUPPRESS\_MESSAGE または CA\_GLOBAL\_SUPPRESS_MESSAGE を使用します。

> [!NOTE]
> ソース内抑制メタデータが誤って配布されるのを防ぐため、リリース ビルドではソース内抑制を使用しないでください。 また、ソース内抑制には処理コストがかかるため、アプリケーションのパフォーマンスが低下する可能性があります。

::: moniker range="vs-2017"

> [!NOTE]
> プロジェクトを Visual Studio 2017 に移行すると、突然、コード分析の警告が多数表示される場合があります。 警告を修正する準備ができていない場合は、 **[分析]**  >  **[コード分析の実行とアクティブな懸案事項の抑制]** を選択することで、すべての警告を抑制できます。
>
> ![Visual Studio でのコード分析の実行と懸案事項の抑制](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019&quot;

> [!NOTE]
> プロジェクトを Visual Studio 2019 に移行すると、突然、コード分析の警告が多数表示される場合があります。 警告を修正する準備ができていない場合は、 **[分析]**  >  **[アクティブな懸案事項のビルドと抑制]** を選択することで、すべての警告を抑制できます。

::: moniker-end

### <a name=&quot;suppressmessage-attribute&quot;></a>SuppressMessage 属性

コンテキストから、または **[エラー一覧]** のコード分析の警告の右クリック メニューから、 **[抑制]** を選択すると、コード内またはプロジェクトのグローバル抑制ファイルのいずれかに、<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性が追加されます。

<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性の形式は次のとおりです。

```vb
<Scope:SuppressMessage(&quot;Rule Category&quot;, &quot;Rule Id&quot;, Justification = &quot;Justification&quot;, MessageId = &quot;MessageId&quot;, Scope = &quot;Scope&quot;, Target = &quot;Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

属性には次のプロパティがあります。

- **Category** - ルールが定義されているカテゴリ。 コード分析規則のカテゴリの詳細については、[マネージド コードの警告](/dotnet/fundamentals/code-analysis/quality-rules/index)に関する記事を参照してください。

- **Checkid** - 規則の識別子。 規則識別子の短い名前と長い名前の両方がサポートされます。 短い名前は CAXXXX です。長い名前は CAXXXX:FriendlyTypeName です。

- **Justification** - メッセージを抑制する理由を文書化するために使用されるテキストです。

- **MessageId** - 各メッセージの問題の一意の識別子。

- **Scope** - 警告が抑制されているターゲット。 ターゲットを指定しないと、属性のターゲットに設定されます。 サポートされる[スコープ](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope)は次のとおりです。

  - [`module`](#module-suppression-scope) - このスコープを指定すると、アセンブリに対する警告が抑制されます。 これは、プロジェクト全体に適用されるグローバルな抑制です。

  - `resource` - ([レガシ FxCop](../code-quality/static-code-analysis-for-managed-code-overview.md) のみ) このスコープを指定すると、モジュール (アセンブリ) の一部であるリソース ファイルに書き込まれる診断情報の警告が抑制されます。 このスコープは、Roslyn アナライザー診断用の C#/VB コンパイラでは読み取られたり、考慮されたりしません。ソース ファイルが分析されるだけです。

  - `type` - このスコープを指定すると、型に対する警告が抑制されます。

  - `member` - このスコープを指定すると、メンバーに対する警告が抑制されます。

  - `namespace` - このスコープを指定すると、名前空間自体に対する警告が抑制されます。 名前空間内の型に対する警告は抑制されません。

  - `namespaceanddescendants` - (コンパイラ バージョン3.x 以降と Visual Studio 2019 が必要) このスコープを指定すると、名前空間とそのすべての子孫のシンボルで警告が抑制されます。 値 `namespaceanddescendants` は、レガシ分析では無視されます。

- **Target** - 警告が抑制されるターゲットを指定するために使用される識別子。 完全修飾項目名が含まれている必要があります。

Visual Studio で警告を表示するときに、[グローバル抑制ファイルに抑制を追加する](../code-quality/use-roslyn-analyzers.md#suppress-violations)ことで、`SuppressMessage` の例を見ることができます。 抑制属性とその必須プロパティが、プレビュー ウィンドウに表示されます。

### <a name="suppressmessage-usage"></a>SuppressMessage の使用法

コード分析の警告は、<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性が適用されるレベルで抑制されます。 たとえば、アセンブリ、モジュール、型、メンバー、またはパラメーターのレベルで属性を適用できます。 この目的は、違反が発生するコードに対して抑制情報を密接に結合することです。

抑制の一般的な形式には、規則のカテゴリと規則の識別子が含まれ、これには人が判読できる規則名の表現が含まれています。 次に例を示します。

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

パフォーマンス上の厳密な理由があり、ソース内抑制メタデータを最小限に抑える場合は、規則名を省略できます。 規則のカテゴリとその規則 ID により、十分に一意な規則識別子が構成されます。 次に例を示します。

`[SuppressMessage("Microsoft.Design", "CA1039")]`

メンテナンスしやすさの理由で、規則名を省略することは推奨されません。

### <a name="suppress-selective-violations-within-a-method-body"></a>メソッド本体内の選択的違反を抑制する

抑制属性をメソッドに適用することはできますが、メソッド本体内に埋め込むことはできません。 これは、<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性をメソッドに追加した場合に、特定の規則のすべての違反が抑制されることを意味します。

将来のコードがコード分析規則から自動的に除外されないようにするためなど、場合によっては、違反の特定のインスタンスを抑制することが必要になることがあります。 特定のコード分析規則で、<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性の `MessageId` プロパティを使用することにより、これを行うことができます。 一般に、特定のシンボル (ローカル変数またはパラメーター) での違反に関する従来の規則では、`MessageId` プロパティが考慮されます。 [CA1500:VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) は、このような規則の一例です。 ただし、実行可能コード (非シンボル) での違反に関する従来の規則では、`MessageId` プロパティは考慮されません。 また、.NET Compiler Platform ("Roslyn") アナライザーでは、`MessageId` プロパティは考慮されません。

特定のシンボルでの規則の違反を抑制するには、<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性の `MessageId` プロパティでシンボル名を指定します。 次の例で示すコードには、[CA1500:VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) の違反が 2 つあります。1 つは `name` 変数に関するもので、もう 1 つは `age` 変数に関するものです。 抑制されるのは、`age` シンボルに関する違反のみです。

```vb
Public Class Animal
    Dim age As Integer
    Dim name As String

    <CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId:="age")>
    Sub PrintInfo()
        Dim age As Integer = 5
        Dim name As String = "Charlie"

        Console.WriteLine("Age {0}, Name {1}", age, name)
    End Sub

End Class
```

```csharp
public class Animal
{
    int age;
    string name;

    [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId = "age")]
    private void PrintInfo()
    {
        int age = 5;
        string name = "Charlie";

        Console.WriteLine($"Age {age}, Name {name}");
    }
}
```

### <a name="global-level-suppressions"></a>グローバル レベルの抑制

マネージド コード分析ツールでは、アセンブリ、モジュール、型、メンバー、またはパラメーターのレベルで適用されている `SuppressMessage` 属性が調べられます。 また、リソースと名前空間に対する違反も生成されます。 これらの違反は、グローバル レベルで適用される必要があり、スコープおよびターゲットが設定されます。 たとえば、次のメッセージでは、名前空間の違反が抑制されます。

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> `namespace` スコープで警告を抑制すると、名前空間自体に対する警告が抑制されます。 名前空間内の型に対する警告は抑制されません。

明示的なスコープを指定することで、任意の抑制を表現できます。 これらの抑制は、グローバル レベルで指定する必要があります。 型を修飾することによって、メンバー レベルの抑制を指定することはできません。

明示的に提供されたユーザー ソースにマップされないコンパイラ生成のコードを参照するメッセージを抑制する唯一の方法は、グローバル レベルでの抑制です。 たとえば、次のコードは、コンパイラによって出力されたコンストラクターに対する違反を抑制します。

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` には、常に、完全修飾された項目名が含まれます。

#### <a name="global-suppression-file"></a>グローバル抑制ファイル

グローバル抑制ファイルには、グローバル レベルの抑制またはターゲット指定のない抑制のいずれかが保持されます。 たとえば、アセンブリ レベルの違反の抑制は、このファイルに格納されます。 また、フォームの分離コードではプロジェクト レベルの設定を使用できないため、ASP.NET の一部の抑制はこのファイルに格納されます。 **[エラー一覧]** ウィンドウで **[抑制]** コマンドの **[プロジェクト抑制ファイル内]** オプションを初めて選択した時点で、グローバル抑制ファイルが作成されてプロジェクトに追加されます。

#### <a name="module-suppression-scope"></a>モジュールの抑制スコープ

**モジュール** スコープを使用すると、アセンブリ全体のコード品質違反を抑制できます。

たとえば、_GlobalSuppressions_ プロジェクト ファイルで次の属性を指定すると、ASP.NET Core プロジェクトの ConfigureAwait 違反が抑制されます。

`[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Reliability", "CA2007:Consider calling ConfigureAwait on the awaited task", Justification = "ASP.NET Core doesn't use thread context to store request context.", Scope = "module")]`

### <a name="generated-code"></a>生成されたコード

マネージド コードのコンパイラと一部のサードパーティ ツールにより、コードの迅速な開発を容易にするコードが生成されます。 ソース ファイルに含まれるコンパイラ生成コードは、通常、`GeneratedCodeAttribute` 属性でマークされます。

ソース コード分析では、生成されたコードでのメッセージを `.editorconfig` ファイルで抑制できます。 詳細については、「[生成されたコードを除外する](/dotnet/fundamentals/code-analysis/configuration-options#exclude-generated-code)」を参照してください。

従来のコード分析の場合は、生成されたコードに対するコード分析の警告とエラーを抑制するかどうかを選択できます。 そのような警告やエラーを抑制する方法の詳細については、[生成されたコードの警告を抑制する方法](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md)に関する記事を参照してください。

> [!NOTE]
> `GeneratedCodeAttribute` をアセンブリ全体または単一のパラメーターのいずれかに適用すると、コード分析で無視されます。

## <a name="see-also"></a>こちらもご覧ください

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [コード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)
