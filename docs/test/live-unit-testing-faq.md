---
title: Live Unit Testing に関する FAQ
description: サポートされているフレームワーク、構成、カスタマイズなど、Live Unit Testing についてよく寄せられる質問をご確認ください。
ms.custom: SEO-VS-2020
ms.date: 10/03/2017
ms.topic: conceptual
helpviewer_keywords:
- Live Unit Testing FAQ
author: mikejo5000
ms.author: mikejo
ms.workload:
- dotnet
ms.openlocfilehash: bb2c9a4cae25b388d5817b04ff54f6e6443b2f44
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800568"
---
# <a name="live-unit-testing-frequently-asked-questions"></a>Live Unit Testing についてよく寄せられる質問

## <a name="supported-frameworks"></a>サポートされるフレームワーク

**Live Unit Testing でサポートされているテスト フレームワークは何ですか? また、サポートされている最小バージョンはいくつですか?**

Live Unit Testing は、次の表に示されている 3 つの一般的な単体テスト フレームワークで動作します。 アダプターやフレームワークのサポートされる最小バージョンも表に示されています。 単体テスト フレームワークはすべて NuGet.org から入手できます。

|テスト フレームワーク  |Visual Studio アダプターの最小バージョン  |フレームワークの最小バージョン  |
|---------|---------|---------|
|xUnit.net |xunit.runner.visualstudio バージョン 2.2.0-beta3-build1187 |xunit 1.9.2 |
|NUnit |NUnit3TestAdapter バージョン 3.7.0 |NUnit バージョン 3.5.0 |
|MSTest |MSTest.TestAdapter 1.1.4-preview |MSTest.TestFramework 1.0.5-preview |

古い MSTest に基づくテスト プロジェクトで `Microsoft.VisualStudio.QualityTools.UnitTestFramework` が参照されていて、新しい MSTest NuGet パッケージに移行したくない場合は、Visual Studio 2019 または Visual Studio 2017 にアップグレードしてください。

場合によっては、Live Unit Testing を動作させるため、ソリューションのプロジェクトによって参照されている NuGet パッケージの明示的な復元が必要になります。 Live Unit Testing を有効にする前に、ソリューションの明示的なビルドを行うか (Visual Studio の最上位メニューから **[ビルド]**  >  **[ソリューションのリビルド]** を選択)、ソリューションを右クリックして **[NuGet パッケージの復元]** を選択することで、パッケージを復元できます。

## <a name="net-core-support"></a>.NET Core サポート

**Live Unit Testing は .NET Core で動作しますか?**

はい。 Live Unit Testing は、.NET Core と .NET Framework で動作します。

## <a name="configuration"></a>構成

**Live Unit Testing を有効にしても動作しないのはなぜですか?**

[出力ウィンドウ] に (Live Unit Testing ドロップダウンを選んだとき)、Live Unit Testing が動作しない理由が表示されているはずです。 Live Unit Testing は、次のいずれかの理由で動作しない可能性があります。

- ソリューションのプロジェクトによって参照されている NuGet パッケージが復元されていない、Live Unit Testing は動作しません。 Live Unit Testing を有効にする前に、ソリューションの明示的なビルドを行うか、ソリューションで NuGet パッケージを復元することにより、この問題は解決するはずです。

- MSTest ベースのテストをプロジェクトで使っている場合、`Microsoft.VisualStudio.QualityTools.UnitTestFramework` への参照を削除し、最新の MSTest NuGet パッケージ `MSTest.TestAdapter` (1.1.11 以降のバージョンが必要) および `MSTest.TestFramework` (1.1.11 以降のバージョンが必要) への参照を追加してあることを確認します。 詳しくは、「[Visual Studio での Live Unit Testing](live-unit-testing.md#supported-test-frameworks)」記事の「サポートされるテスト フレームワーク」セクションをご覧ください。

- ソリューションの少なくとも 1 つのプロジェクトに、NuGet の参照、または xUnit、NUnit、MSTest のいずれかのテスト フレームワークへの直接参照が存在する必要があります。 このプロジェクトは、対応する Visual Studio テスト アダプター NuGet パッケージを参照する必要もあります。 Visual Studio テスト アダプターは、 *.runsettings* ファイルから参照することもできます。 *.runsettings* ファイルには、次の例のようなエントリが必要です。

```xml
<RunSettings>
    <RunConfiguration>
          <TestAdaptersPaths>path-to-your-test-adapter</TestAdaptersPaths>
     </RunConfiguration>
</RunSettings>
```

## <a name="incorrect-coverage-after-upgrade"></a>アップグレード後の正しくないカバレッジ

**Visual Studio プロジェクトで参照されているテスト アダプターをサポートされているバージョンにアップグレードした後、Live Unit Testing に正しくないカバレッジが表示されるのはなぜですか?**

- ソリューションの複数のプロジェクトが NuGet テスト アダプター パッケージを参照している場合は、それぞれをサポートされるバージョンにアップグレードする必要があります。

- テスト アダプター パッケージからインポートされた MSBuild の *.props* ファイルも正しく更新されていることを確認してください。 インポートの NuGet パッケージのバージョン/パスを確認します。通常これは、次のように、プロジェクト ファイルの上部近くに表示されます。

   ```xml
    <Import Project="..\packages\xunit.runner.visualstudio.2.2.0\build\net20\xunit.runner.visualstudio.props" Condition="Exists('..\packages\xunit.runner.visualstudio.2.2.0\build\net20\xunit.runner.visualstudio.props')" />
   ```

## <a name="customize-builds"></a>ビルドのカスタマイズ

**Live Unit Testing のビルドをカスタマイズできますか?**

"標準の" インストルメント化されていないビルドには必要ないインストルメンテーション (Live Unit Testing) 用にビルドするためのカスタム手順がソリューションに必要な場合は、`BuildingForLiveUnitTesting` プロパティを調べてビルド前/後のカスタム手順を行うコードを、プロジェクトまたは *.targets* ファイルに追加できます。 また、このプロジェクト プロパティに基づいて、Live Unit Testing のビルドから特定のビルド手順 (パッケージの発行や生成など) を削除したり、Live Unit Testing にビルド手順 (前提条件のコピーなど) を追加したりすることもできます。 このプロパティに基づいてビルドをカスタマイズしても、標準のビルドは変更されず、Live Unit Testing のビルドのみが影響を受けます。

たとえば、標準のビルドの間に NuGet パッケージを生成するターゲットがあるものとします。 おそらく、編集のたびに NuGet パッケージを生成する必要はありません。 そのような場合、次のようにして、Live Unit Testing のビルドでそのターゲットを無効にできます。  

```xml
<Target Name="GenerateNuGetPackages" BeforeTargets="AfterBuild" Condition="'$(BuildingForLiveUnitTesting)' != 'true'">
    <Exec Command='"$(MSBuildThisFileDirectory)..\tools\GenPac" '/>
</Target>
```

## <a name="error-messages-with-outputpath-outdir-or-intermediateoutputpath"></a>\<OutputPath>、\<OutDir> または \<IntermediateOutputPath> を含むエラー メッセージ

**Live Unit Testing がソリューションのビルドを試みると、次のようなエラー メッセージが表示されるのはなぜですか? "...appears to unconditionally set `<OutputPath>` or `<OutDir>`.Live Unit Testing will not execute tests from the output assembly" (... が <OutputPath> または <OutDir> を無条件に設定したようです。Live Unit Testing は出力アセンブリからテストを実行しません)**

ソリューションのビルド プロセスに、バイナリの生成先を指定するカスタム ロジックがある場合、このエラーが発生することがあります。 既定のバイナリの場所は、`<OutputPath>`、`<OutDir>`、または `<IntermediateOutputPath>` だけでなく、`<BaseOutputPath>` または `<BaseIntermediateOutputPath>` によって変わります。

Live Unit Testing を使うと、これらの変数をオーバーライドし、ビルドの成果物が Live Unit Testing の成果物フォルダーに確実にドロップすることができます。また、ビルド プロセスでもこれらの変数がオーバーライドされた場合は失敗します。

Live Unit Testing のビルドを成功させるには、主に 2 つの方法があります。 簡易なビルド構成の場合は、`<BaseIntermediateOutputPath>` に基づいた出力パスにすることができます。 より複雑な構成の場合は、`<LiveUnitTestingBuildRootPath>` に基づいた出力パスにすることができます。

### <a name="overriding-outputpathintermediateoutputpath-conditionally-based-on-baseoutputpath-baseintermediateoutputpath"></a>`<OutputPath>`/`<IntermediateOutputPath>` のオーバーライドは、条件によっては `<BaseOutputPath>`/ `<BaseIntermediateOutputPath>` に基づいています。

> [!NOTE]
> この方法を使用するには、各プロジェクトを互いに独立してビルドできる必要があります。 ビルド中に、あるプロジェクトから別のプロジェクトの成果物を参照しないでください。 実行時に、あるプロジェクトで別のプロジェクトのアセンブリを動的に読み込まないでください (たとえば、`Assembly.Loadfile("..\..\Project2\Release\Project2.dll")` を呼び出すなど)。

ビルド中に、Live Unit Testing によって `<BaseOutputPath>`/`<BaseIntermediateOutputPath>` 変数が自動的にオーバーライドされ、Live Unit Testing の成果物フォルダーをターゲットにされます。

たとえば、次のように <OutputPath> をオーバーライドするものとします。

```xml
<Project>
  <PropertyGroup>
    <OutputPath>$(SolutionDir)Artifacts\$(Configuration)\bin\$(MSBuildProjectName)</OutputPath>
  </PropertyGroup>
</Project>
```

これは、次の XML で置き換えることができます。

```xml
<Project>
  <PropertyGroup>
    <BaseOutputPath Condition="'$(BaseOutputPath)' == ''">$(SolutionDir)Artifacts\$(Configuration)\bin\$(MSBuildProjectName)\</BaseOutputPath>
    <OutputPath Condition="'$(OutputPath)' == ''">$(BaseOutputPath)</OutputPath>
  </PropertyGroup>
</Project>
```

これにより、`<OutputPath>` は `<BaseOutputPath>` フォルダー内に存在するようになります。

ビルド プロセスで `<OutDir>` を直接オーバーライドしないでください。ビルド成果物を特定の場所に格納するには、代わりに `<OutputPath>` をオーバーライドします。

### <a name="overriding-your-properties-based-on-the-liveunittestingbuildrootpath-property"></a>`<LiveUnitTestingBuildRootPath>` プロパティに基づいたプロパティのオーバーライド。

> [!NOTE]
> この方法では、ビルド中に生成されない成果物フォルダー以下に追加されたファイルに注意する必要があります。 以下の例は、成果物以下にパッケージ フォルダーを配置するときの処理を示しています。 このフォルダーの内容はビルド中に生成されないため、MSBuild プロパティを **変更しないでください**。

Live Unit Testing のビルド中に、`<LiveUnitTestingBuildRootPath>` プロパティは Live Unit Testing の成果物フォルダーの場所に設定されます。

たとえば、次のようなプロジェクトの構造だとします。

```
.vs\...\lut\0\b
artifacts\{binlog,obj,bin,nupkg,testresults,packages}
src\{proj1,proj2,proj3}
tests\{testproj1,testproj2}
Solution.sln
```
Live Unit Testing のビルド中に、`<LiveUnitTestingBuildRootPath>` プロパティは `.vs\...\lut\0\b` の完全パスに設定されます。 ソリューション ディレクトリにマップされる `<ArtifactsRoot>` プロパティがプロジェクトで定義されている場合は、次のように MSBuild プロジェクトを更新できます。

```xml
<Project>
    <PropertyGroup Condition="'$(LiveUnitTestingBuildRootPath)' == ''">
        <SolutionDir>$([MSBuild]::GetDirectoryNameOfFileAbove(`$(MSBuildProjectDirectory)`, `YOUR_SOLUTION_NAME.sln`))\</SolutionDir>

        <ArtifactsRoot>Artifacts\</ArtifactsRoot>
        <ArtifactsRoot Condition="'$(LiveUnitTestingBuildRootPath)' != ''">$(LiveUnitTestingBuildRootPath)</ArtifactsRoot>
    </PropertyGroup>

    <PropertyGroup>
        <BinLogPath>$(ArtifactsRoot)\BinLog</BinLogPath>
        <ObjPath>$(ArtifactsRoot)\Obj</ObjPath>
        <BinPath>$(ArtifactsRoot)\Bin</BinPath>
        <NupkgPath>$(ArtifactsRoot)\Nupkg</NupkgPath>
        <TestResultsPath>$(ArtifactsRoot)\TestResults</TestResultsPath>

        <!-- Note: Given that a build doesn't generate packages, the path should be relative to the solution dir, rather than artifacts root, which will change during a Live Unit Testing build. -->
        <PackagesPath>$(SolutionDir)\artifacts\packages</PackagesPath>
    </PropertyGroup>
</Project>
```

## <a name="build-artifact-location"></a>ビルド成果物の場所

**Live Unit Testing のビルド成果物を、 *.vs* フォルダーの下の既定の場所ではない特定の場所に格納する必要があります。どうすれば変更できますか?**

`LiveUnitTesting_BuildRoot` ユーザー レベル環境変数を、Live Unit Testing のビルド成果物を格納するパスに設定します。 

## <a name="test-explorer-versus-live-unit-testing"></a>テスト エクスプローラーと Live Unit Testing

**[テスト エクスプローラー] ウィンドウと Live Unit Testing では、テストの実行方法はどのように違いますか?**

いくつか違いがあります。

- **[テスト エクスプローラー]** ウィンドウからテストを実行またはデバッグすると標準バイナリが実行されますが、Live Unit Testing ではインストルメント化されたバイナリが実行されます。 インストルメント化されたバイナリをデバッグする場合、テスト メソッドに [Debugger.Launch](xref:System.Diagnostics.Debugger.Launch) メソッドの呼び出しを追加し、そのメソッドが実行されると常にデバッガーが起動されるようにすることで (Live Unit Testing によって実行される場合を含みます)、インストルメント化されたバイナリをアタッチしてデバッグできます。 しかし、ほとんどのユーザー シナリオについてインストルメンテーションが透過的で、インストルメント化されたバイナリをデバッグする必要がないようにするのが理想的です。

- Live Unit Testing ではテストを実行するための新しいアプリケーション ドメインは作成されませんが、 **[テスト エクスプローラー]** ウィンドウから実行されたテストでは新しいアプリケーション ドメインが作成されます。

- Live Unit Testing では、各テスト アセンブリで順番にテストが実行されます。 **テスト エクスプローラー** で、複数のテストの並列実行を選択できます。

- 既定では、**テスト エクスプローラー** によるテストはシングルスレッド アパートメント (STA) で実行されるのに対し、Live Unit Testing によるテストはマルチスレッド アパートメント (MTA) で実行されます。 Live Unit Testing において MSTest テストを STA で実行するには、テスト メソッドまたはそれを含むクラスを、`MSTest.STAExtensions 1.0.3-beta` NuGet パッケージに含まれる `<STATestMethod>` または `<STATestClass>` 属性で修飾します。 NUnit の場合はテスト メソッドを `<RequiresThread(ApartmentState.STA)>` 属性で修飾し、xUnit の場合は `<STAFact>` 属性で修飾します。

## <a name="exclude-tests"></a>テストの除外

**Live Unit Testing からテストを除外するにはどうすればよいですか?**

ユーザー固有の設定については、「[Visual Studio での Live Unit Testing](live-unit-testing.md#include-and-exclude-test-projects-and-test-methods)」記事の「テスト プロジェクトとテスト メソッドを含めるか除外する」セクションをご覧ください。 テストを含めるまたは除外すると、特定の編集セッションに対して特定のテスト セットを実行したい場合、または個人設定を維持したい場合に便利です。

ソリューション固有の設定では、<xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute?displayProperty=fullName> 属性をプログラムで適用することにより、Live Unit Testing によるインストルメント化からメソッド、プロパティ、クラス、構造体を除外できます。 さらに、プロジェクト ファイルで `<ExcludeFromCodeCoverage>` プロパティを `true` に設定して、プロジェクト全体をインストルメント化から除外することもできます。 それでも Live Unit Testing はインストルメント化されていないテストを実行しますが、カバレッジは視覚化されません。

`Microsoft.CodeAnalysis.LiveUnitTesting.Runtime` が現在のアプリケーション ドメインに読み込まれているかどうかを確認し、理由に基づいてテストを無効にすることもできます。 たとえば、xUnit では次のような処理を行うことができます。

```csharp
[ExcludeFromCodeCoverage]
public class SkipLiveFactAttribute : FactAttribute
{
   private static bool s_lutRuntimeLoaded = AppDomain.CurrentDomain.GetAssemblies().Any(a => a.GetName().Name ==
                                            "Microsoft.CodeAnalysis.LiveUnitTesting.Runtime");
   public override string Skip => s_lutRuntimeLoaded ? "Test excluded from Live Unit Testing" : "";
}

public class Class1
{
   [SkipLiveFact]
   public void F()
   {
      Assert.True(true);
   }
}
```

::: moniker range="vs-2017"

## <a name="win32-pe-headers"></a>Win32 PE ヘッダー

**Live Unit Testing によってビルドされたインストルメント化されたアセンブリでは Win32 PE ヘッダーが異なるのはなぜですか?**

この問題は解消されており、Visual Studio 2017 バージョン 15.3 以降では発生しません。

以前のバージョンの Visual Studio 2017 の場合、Live Unit Testing のビルドで次の Win32 PE ヘッダー データの埋め込みが失敗する既知のバグがあります。

- ファイル バージョン (コードで @System.Reflection.AssemblyFileVersionAttribute によって指定)。

- Win32 アイコン (コマンド ラインで `/win32icon:` によって指定)。

- Win32 マニフェスト (コマンド ラインで `/win32manifest:` によって指定)。

これらの値に依存するテストは、Live Unit Testing で実行すると失敗する場合があります。

::: moniker-end

## <a name="continuous-builds"></a>連続的なビルド

**編集を行わなかった場合でも Live Unit Testing で常にソリューションがビルドされるのはなぜですか?**

編集を行っていなくても、ビルド プロセスによってソリューション自体の一部であるソース コードが生成され、ビルド ターゲット ファイルにおいて適切な入力と出力が指定されていない場合は、ソリューションがビルドされる場合があります。 MSBuild が適切な最新状態チェックを実行し、新しいビルドが必要かどうかを判断できるように、ターゲットに入力と出力のリストを提供する必要があります。

Live Unit Testing は、ソース ファイルが変更されたことを検出すると常に、ビルドを開始します。 ソリューションのビルドでソース ファイルが生成されるので、Live Unit Testing は無限ビルド ループになります。 ただし、Live Unit Testing で (前のビルドで新しく生成されたソース ファイルを検出した後) 2 回目のビルドが開始されるときに、ターゲットの入力と出力が調べられる場合は、入力と出力のチェックですべてが最新であることが示されるため、ビルド ループから抜け出します。

## <a name="editor-icons"></a>エディターのアイコン

**出力ウィンドウのメッセージでは Live Unit Testing が実行しているようなのに、エディターにアイコンが表示されないのはなぜですか?**

Live Unit Testing が動作しているアセンブリが何らかの理由でインストルメント化されていない場合に、エディターにアイコンが表示されない場合があります。 たとえば、Live Unit Testing は `<UseHostCompilerIfAvailable>false</UseHostCompilerIfAvailable>` を設定するプロジェクトと互換性がありません。 この場合、Live Unit Testing を動作させるには、ビルド プロセスを更新してこの設定を削除する、または `true` に変更する必要があります。 

## <a name="capture-logs"></a>ログのキャプチャ

**ファイル バグ レポートに詳細なログを収集するにはどうすればよいですか?**

詳細なログを収集するにはいくつかの方法があります。

- **[ツール]**  >  **[オプション]**  >  **[Live Unit Testing]** の順に移動し、ログ オプションを **[詳細]** に変更します。 詳細ログにより、より詳細なログが **[出力]** ウィンドウに表示されます。

- `LiveUnitTesting_BuildLog` ユーザー環境変数に、MSBuild ログのキャプチャに使うファイルの名前を設定します。 このようにすると、Live Unit Testing のビルドからの詳細な MSBuild ログ メッセージを、そのファイルから取得できます。

- `LiveUnitTesting_TestPlatformLog` ユーザー環境変数を `1` に設定して、テスト プラットフォームのログをキャプチャします。 このようにすると、Live Unit Testing の実行からの詳細なテスト プラットフォームのログ メッセージを `[Solution Root]\.vs\[Solution Name]\log\[VisualStudio Process ID]` から取得できます。

- `VS_UTE_DIAGNOSTICS` という名前のユーザー レベル環境変数を作成し、1 (または任意の値) に設定して、Visual Studio を再起動します。 Visual Studio の **[出力 - テスト]** タブに多くのログが表示されるようになります。

## <a name="see-also"></a>関連項目

- [ライブ単体テスト](live-unit-testing.md)
