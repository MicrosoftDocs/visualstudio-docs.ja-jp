---
title: IDE またはコマンド ラインからコード メトリックを生成する
ms.date: 11/02/2018
description: Visual Studio でコード メトリック データを生成する方法について説明します。 ソリューション エクスプローラー、ルール セット ファイル、コマンド ライン、またはメニュー コマンドの使用方法を確認します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code metrics data
- code metrics results
- code metrics [Visual Studio]
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aa0512e5d29cb1b5c5a39715e34667803b752795
ms.sourcegitcommit: 04954be0c4373f82f79181e1a5e7812be4d3e1f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2021
ms.locfileid: "100496263"
---
# <a name="how-to-generate-code-metrics-data"></a>方法: コード メトリック データを生成する

コード メトリック データは、次の 3 つの方法で生成できます。

- [.NET コード品質アナライザー](#net-code-quality-analyzers-code-metrics-rules)を有効化し、それに含まれている 4 つのコード メトリック (保守性) ルールを有効化します。

- Visual Studio で [ **[分析]**  >  **[コード メトリックスの計算]** ](#calculate-code-metrics-menu-command) メニュー コマンドを選択します。

- C# および Visual Basic プロジェクトでは[コマンド ライン](#command-line-code-metrics)から。

## <a name="net-code-quality-analyzers-code-metrics-rules"></a>.NET コード品質アナライザーのコード メトリック ルール

.NET コード品質アナライザーには、コード メトリック [アナライザー](roslyn-analyzers-overview.md) ルールがいくつか含まれています。

- [CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)
- [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)
- [CA1505](/dotnet/fundamentals/code-analysis/quality-rules/ca1505)
- [CA1506](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)

これらの規則は既定では無効ですが、[**ソリューション エクスプローラー**](use-roslyn-analyzers.md#set-rule-severity-from-solution-explorer)または [EditorConfig](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file) ファイルで有効にすることができます。 たとえば、ルール CA1502 を警告として有効にするには、EditorConfig ファイルに次のエントリを含めます。

```cs
dotnet_diagnostic.CA1502.severity = warning
```

### <a name="configuration"></a>構成

コード メトリック ルールが起動されるしきい値を構成できます。

1. テキスト ファイルを作成します。 たとえば、*CodeMetricsConfig.txt* という名前を付けます。

2. 必要なしきい値を次の形式でこのテキスト ファイルに追加します。

   ```txt
   CA1502: 10
   ```

   この例では、メソッドのサイクロマティック複雑度が 10 を超えると、ルール [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502) が起動するように構成されます。

3. Visual Studio の **[プロパティ]** ウィンドウまたはプロジェクト ファイルで、構成ファイルのビルド アクションを [**AdditionalFiles**](../ide/build-actions.md#build-action-values) としてマークします。 次に例を示します。

   ```xml
   <ItemGroup>
     <AdditionalFiles Include="CodeMetricsConfig.txt" />
   </ItemGroup>
   ```

## <a name="calculate-code-metrics-menu-command"></a>[コード メトリックスの計算] メニュー コマンド

**[分析]**  >  **[コード メトリックスの計算]** メニューを使用して、IDE で開いているプロジェクトの 1 つまたはすべてのコード メトリックを生成します。

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>ソリューション全体のコード メトリック結果を生成する

ソリューション全体に対するコード メトリック結果は、次のいずれかの方法で生成できます。

- メニュー バーで、 **[分析]**  >  **[コード メトリックスの計算]**  >  **[ソリューション用]** を選択します。

- **ソリューション エクスプローラー** でソリューションを右クリックし、 **[コード メトリックスの計算]** を選択します。

- **[コード メトリックスの結果]** ウィンドウで、 **[ソリューションのコード メトリックスを計算]** ボタンを選択します。

結果が生成され、 **[コード メトリックスの結果]** ウィンドウが表示されます。 結果の詳細を表示するには、 **[階層]** 列でツリーを展開します。

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>1 つ以上のプロジェクトのコード メトリック結果を生成する

1. **ソリューション エクスプローラー** で、1 つ以上のプロジェクトを選択します。

1. メニュー バーで、 **[分析]**  >  **[コード メトリックスの計算]**  >  **[選択したプロジェクト用]** を選択します。

結果が生成され、 **[コード メトリックスの結果]** ウィンドウが表示されます。 結果の詳細を表示するには、 **[階層]** のツリーを展開します。

::: moniker range="vs-2017"

> [!NOTE]
> **[コード メトリックスの計算]** コマンドは、.NET Core および .NET Standard プロジェクトでは機能しません。 .NET Core または .NET Standard プロジェクトのコード メトリックを計算するには、次のようにします。
>
> - 代わりに[コマンド ライン](#command-line-code-metrics)でコード メトリックを計算します。
>
> - [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) にアップグレードします。

::: moniker-end

## <a name="command-line-code-metrics"></a>コマンド ライン コード メトリック

.NET Framework、.NET Core、および .NET Standard アプリの C# および Visual Basic プロジェクトでは、コマンド ラインからコード メトリック データを生成できます。 コマンド ラインからコード メトリックを実行するには、[Microsoft.CodeAnalysis.Metrics NuGet パッケージ](#microsoftcodeanalysismetrics-nuget-package)をインストールするか、[Metrics.exe](#metricsexe) 実行可能ファイルを自らビルドします。

### <a name="microsoftcodeanalysismetrics-nuget-package"></a>Microsoft.CodeAnalysis.Metrics NuGet パッケージ

コマンド ラインからコード メトリック データを生成する最も簡単な方法は、[Microsoft.CodeAnalysis.Metrics](https://www.nuget.org/packages/Microsoft.CodeAnalysis.Metrics/) NuGet パッケージをインストールすることです。 パッケージをインストールしたら、プロジェクト ファイルが格納されているディレクトリで `msbuild /t:Metrics` を実行します。 次に例を示します。

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:29:57 PM.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics\Metrics.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:ClassLibrary3.Metrics.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'ClassLibrary3.Metrics.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

出力ファイル名をオーバーライドするには、`/p:MetricsOutputFile=<filename>` を指定します。 また、`/p:LEGACY_CODE_METRICS_MODE=true` を指定して、[以前のスタイル](#previous-versions)のコード メトリック データを取得することもできます。 次に例を示します。

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics /p:LEGACY_CODE_METRICS_MODE=true /p:MetricsOutputFile="Legacy.xml"
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:31:00 PM.
The "MetricsOutputFile" property is a global property, and cannot be modified.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics.Legacy\Metrics.Legacy.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:Legacy.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'Legacy.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

### <a name="code-metrics-output"></a>コード メトリックの出力

生成される XML 出力の形式は次のとおりです。

::: moniker range=">=vs-2019"

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="SourceLines" Value="11" />
          <Metric Name="ExecutableLines" Value="1" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="SourceLines" Value="11" />
              <Metric Name="ExecutableLines" Value="1" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="SourceLines" Value="7" />
                  <Metric Name="ExecutableLines" Value="1" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="SourceLines" Value="4" />
                      <Metric Name="ExecutableLines" Value="1" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```

::: moniker-end
::: moniker range="vs-2017"

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="LinesOfCode" Value="11" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="LinesOfCode" Value="11" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="LinesOfCode" Value="7" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="LinesOfCode" Value="4" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```

::: moniker-end

### <a name="metricsexe"></a>Metrics.exe

NuGet パッケージをインストールしない場合は、*Metrics.exe* 実行可能ファイルを生成して直接使用することができます。 *Metrics.exe* 実行可能ファイルを生成するには:

1. [dotnet/roslyn-analyzers](https://github.com/dotnet/roslyn-analyzers) リポジトリを複製します。
2. 管理者として Visual Studio 用開発者コマンド プロンプトを開きます。
3. **roslyn-analyzers** リポジトリのルートで、次のコマンドを実行します: `Restore.cmd`
4. *src\Tools\Metrics* ディレクトリに移動します。
5. 次のコマンドを実行して、**Metrics.csproj** プロジェクトをビルドします。

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   *Metrics.exe* という名前の実行可能ファイルが、リポジトリのルートの *artifacts\bin* ディレクトリに生成されます。

#### <a name="metricsexe-usage"></a>Metrics.exe の使用方法

*Metrics.exe* を実行するには、プロジェクトまたはソリューションと出力 XML ファイルを引数として指定します。 次に例を示します。

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

#### <a name="legacy-mode"></a>レガシ モード

"*レガシ モード*" での *Metrics.exe* のビルドを選択できます。 ツールのレガシ モード バージョンでは、[以前のバージョンのツールで生成された](#previous-versions)ものに近いメトリック値が生成されます。 また、レガシ モードでは、以前のバージョンのツールでコード メトリック生成が行われたのと同じ一連のメソッドのタイプに対して、*Metrics.exe* によってコード メトリックが生成されます。 たとえば、フィールドやプロパティ初期化子のコード メトリック データは生成されません。 レガシ モードは、旧バージョンとの互換性を維持したり、コード メトリックの数値に基づいてコード チェックイン ゲートを用意したりする場合に便利です。 レガシ モードで *Metrics.exe* をビルドするコマンドは次のとおりです。

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

詳細については、「[レガシ モードでのコード メトリック生成の有効化](https://github.com/dotnet/roslyn-analyzers/pull/1841)」を参照してください。

### <a name="previous-versions"></a>以前のバージョン

::: moniker range=">=vs-2019"
Visual Studio 2015 には、*Metrics.exe* とも呼ばれるコマンド ライン コード メトリック ツールが含まれていました。 このツールの以前のバージョンでは、バイナリ分析 (アセンブリベースの分析) が行われていました。 新しいバージョンの *Metrics.exe* ツールでは、代わりにソース コードが分析されます。 新しい *Metrics.exe* ツールはソース コードに基づいているため、コマンド ライン コード メトリックの結果が、Visual Studio IDE および以前のバージョンの *Metrics.exe* によって生成されたものと異なる場合があります。 Visual Studio 2019 以降では、Visual Studio IDE はコマンド ライン ツールのようにソース コードを分析し、結果は同じになります。

::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2015 には、*Metrics.exe* とも呼ばれるコマンド ライン コード メトリック ツールが含まれていました。 このツールの以前のバージョンでは、バイナリ分析 (アセンブリベースの分析) が行われていました。 新しい *Metrics.exe* ツールでは、代わりにソース コードが分析されます。 新しい *Metrics.exe* ツールはソース コードに基づいているため、コマンド ライン コード メトリックの結果が、Visual Studio IDE および以前のバージョンの *Metrics.exe* によって生成されたものと異なります。
::: moniker-end

新しいコマンド ライン コード メトリック ツールでは、ソリューションとプロジェクトを読み込むことができる限り、ソース コード エラーが存在する場合でもメトリックを計算します。

#### <a name="metric-value-differences"></a>メトリック値の違い

::: moniker range=">=vs-2019"
Starting in Visual Studio 2019 バージョン 16.4 以降および Microsoft.CodeAnalysis.Metics (2.9.5) では、`SourceLines` および `ExecutableLines` によって以前の `LinesOfCode` メトリックが置き換えられます。 新しいメトリックの詳細については、「[コード メトリックの値](../code-quality/code-metrics-values.md)」を参照してください。 この `LinesOfCode` メトリックは、レガシ モードで使用できます。
::: moniker-end
::: moniker range="vs-2017"
`LinesOfCode` メトリックは、新しいコマンド ライン メトリック ツールで正確さと信頼性が向上しています。 これは codegen の違いに依存せず、ツールセットやランタイムが変更されても変更されません。 新しいツールでは、空白行やコメントも含めて、実際のコード行がカウントされます。
::: moniker-end

`CyclomaticComplexity` や `MaintainabilityIndex` など他のメトリックでは、以前のバージョンの *Metrics.exe* と同じ数式が使用されますが、新しいツールでは中間言語 (IL) 命令ではなく `IOperations` (論理ソース命令) の数がカウントされます。 これらの数は、Visual Studio IDE および以前のバージョンの *Metrics.exe* によって生成される数とは若干異なります。

## <a name="see-also"></a>こちらもご覧ください

- [[コード メトリックスの結果] ウィンドウを使用する](../code-quality/working-with-code-metrics-data.md)
- [コード メトリック値](../code-quality/code-metrics-values.md)