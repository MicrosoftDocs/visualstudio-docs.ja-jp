---
title: ビルドのカスタマイズ | Microsoft Docs
description: 標準のビルド プロセスを使用する MSBuild プロジェクトのカスタマイズに使用できる、いくつかの拡張フックについて説明します。
ms.custom: SEO-VS-2020
ms.date: 06/13/2019
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, transforms
- transforms [MSBuild]
ms.assetid: d0bceb3b-14fb-455c-805a-63acefa4b3ed
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 19dafcbb956634eeea5fa0ed967e93a8a8d5e546
ms.sourcegitcommit: 3fe04d5b931ae459a802a1b965f84186757cbc08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2021
ms.locfileid: "111588450"
---
# <a name="customize-your-build"></a>ビルドのカスタマイズ

標準のビルド プロセス (*Microsoft.Common.props* と *Microsoft.Common.targets* のインポート) を使用する MSBuild プロジェクトには、ビルド プロセスのカスタマイズに使用できる拡張フックがいくつかあります。

## <a name="add-arguments-to-command-line-msbuild-invocations-for-your-project"></a>プロジェクトのコマンドライン MSBuild 呼び出しに引数を追加する

ソース ディレクトリの中またはその上にある *Directory.Build.rsp* ファイルがプロジェクトのコマンドライン ビルドに適用されます。 詳細については、「[MSBuild 応答ファイル](../msbuild/msbuild-response-files.md#directorybuildrsp)」を参照してください。

## <a name="directorybuildprops-and-directorybuildtargets"></a>Directory.Build.props と Directory.Build.targets

MSBuild バージョン 15 より前では、ソリューション内のプロジェクトに新しいカスタム プロパティを提供する場合、ソリューション内のすべてのプロジェクト ファイルにそのプロパティへの参照を手動で追加する必要がありました。 または、 *.props* ファイルでプロパティを定義してから、ソリューションのすべてのプロジェクトでその *.props* ファイルを明示的にインポートする必要がありました。

ただし、現在では、ソースが含まれるルート フォルダーにある *Directory.Build.props* という単一のファイルで新しいプロパティを定義することで、1 つのステップですべてのプロジェクトに追加できます。 MSBuild が実行されると、*Microsoft.Common.props* はディレクトリ構造で *Directory.Build.props* ファイルを検索します (また、*Microsoft.Common.targets* は *Directory.Build.targets* を探します)。 該当するものが見つかった場合、プロパティがインポートされます。 *Directory.Build.props* は、ディレクトリの下のプロジェクトをカスタマイズできるようにする、ユーザー定義のファイルです。

> [!NOTE]
> Linux ベースのファイル システムは、大文字小文字を区別します。 Directory.Build.props ファイル名の大文字と小文字が正確に一致していることを確認してください。一致していないと、ビルド プロセス中に検出されません。
>
> 詳細については、[こちらの GitHub の問題](https://github.com/dotnet/core/issues/1991#issue-368441031)のページを参照してください。

### <a name="directorybuildprops-example"></a>Directory.Build.props の例

たとえば、すべてのプロジェクトで新しい Roslyn の **/deterministic** 機能 (プロパティ `$(Deterministic)` によって Roslyn `CoreCompile` ターゲットで公開される) にアクセスできるようにする場合は、次のようにします。

1. リポジトリのルートに *Directory.Build.props* という新しいファイルを作成します。
2. そのファイルに次の XML を追加します。

   ```xml
   <Project>
    <PropertyGroup>
      <Deterministic>true</Deterministic>
    </PropertyGroup>
   </Project>
   ```

3. MSBuild を実行します。 プロジェクトの既存の *Microsoft.Common.props* と *Microsoft.Common.targets* のインポートで、ファイルが検索され、インポートされます。

### <a name="search-scope"></a>検索範囲

*Directory.Build.props* ファイルを検索するときに、MSBuild は *Directory.Build.props* ファイルが見つかるまでプロジェクトの場所 (`$(MSBuildProjectFullPath)`) から上方向にディレクトリ構造を調べます。 たとえば、以下のディレクトリ構造のように、`$(MSBuildProjectFullPath)` が *c:\users\username\code\test\case1* である場合、MSBuild はそこから検索を開始し、*Directory.Build.props* ファイルが見つかるまでディレクトリ構造を上方向に検索します。

```
c:\users\username\code\test\case1
c:\users\username\code\test
c:\users\username\code
c:\users\username
c:\users
c:\
```

ソリューション ファイルの場所は *Directory.Build.props* と関連はありません。

### <a name="import-order"></a>インポートの順序

*Directory.Build.props* は *Microsoft.Common.props* で最初にインポートされ、後で定義されるプロパティを使用することはできません。 そのため、まだ定義されていない (したがって、評価が空になる) プロパティを参照しないようにしてください。

*Directory.Build.props* で設定されたプロパティは、プロジェクト ファイルまたはインポートされたファイル内の他の場所でオーバーライドできます。そのため、プロジェクトの既定値を指定する際に、*Directory.Build.props* の設定を考慮する必要があります。

*Directory.Build.targets* は、NuGet パッケージから *.targets* ファイルがインポートされた後に *Microsoft.Common.targets* からインポートされます。 そのため、ほとんどのビルド ロジックで定義されているプロパティやターゲットをオーバーライドしたり、個々のプロジェクトの設定に関係なく、すべてのプロジェクトのプロパティを設定したりできます。

プロパティを設定するか、前の設定をオーバーライドする個々のプロジェクトのターゲットを定義する必要がある場合は、最後のインポートの後にそのロジックをプロジェクト ファイルに配置します。 SDK スタイルのプロジェクトでこれを行うには、最初に SDK スタイルの属性を同等のインポートに置き換える必要があります。 「[MSBuild プロジェクト SDK の使用方法](how-to-use-project-sdk.md)」を参照してください。

> [!NOTE]
> MSBuild エンジンは、いずれかのプロジェクト (`PreBuildEvent` を含む) のビルド実行を開始する前に、評価中にインポートされたすべてのファイルを読み取ります。そのため、これらのファイルは `PreBuildEvent` やビルド プロセスの他の部分によって変更されることはないと思われます。 変更は、次に *Msbuild.exe* が呼び出されるか、次に Visual Studio がビルドされるまで有効になりません。

### <a name="use-case-multi-level-merging"></a>ユース ケース: マルチレベルの結合

この標準のソリューション構造が用意されているとします。

```
\
  MySolution.sln
  Directory.Build.props     (1)
  \src
    Directory.Build.props   (2-src)
    \Project1
    \Project2
  \test
    Directory.Build.props   (2-test)
    \Project1Tests
    \Project2Tests
```

すべてのプロジェクト *(1)* の共通プロパティ、*src* プロジェクト *(2-src)* の共通プロパティ、*test* プロジェクト *(2-test)* の共通プロパティを用意すると便利な場合があります。

MSBuild で "内" ファイル (*2-src* と *2-test*) と "外" ファイル (*1*) を正しく結合するには、MSBuild で *Directory.Build.props* ファイルが見つかると後続のスキャンが停止することを考慮する必要があります。 スキャンを続行し、外ファイルに結合するには、次のコードを両方の内ファイルに追加します。

`<Import Project="$([MSBuild]::GetPathOfFileAbove('Directory.Build.props', '$(MSBuildThisFileDirectory)../'))" />`

MSBuild の一般的手法をまとめると次のようになります。

- 特定のプロジェクトに対して、MSBuild がソリューション構造の上方で最初の *Directory.Build.props* が見つけると、既定でそれを結合し、後続のスキャンを停止する
- 複数のレベルを見つけ、結合する場合、"内" ファイルから "外" ファイルを [`<Import...>`](../msbuild/property-functions.md#msbuild-getpathoffileabove) する (上のコード参照)
- "外" ファイル自体でその上にある何かもインポートされない場合、そこでスキャンが停止する
- スキャン/結合プロセスを制御するには、`$(DirectoryBuildPropsPath)` と `$(ImportDirectoryBuildProps)` を使用する

もっと簡単にまとめると、何もインポートしない最初の *Directory.Build.props* が MSBuild の停止箇所になります。

### <a name="choose-between-adding-properties-to-a-props-or-targets-file"></a>.props ファイルまたは .targets ファイルのどちらにプロパティを追加するかを選択する

MSBuild はインポートの順序に依存するので、最後のプロパティ (または、`UsingTask` またはターゲット) の定義が使われます。

明示的なインポートを使うときは、いつでも *.props* または *.targets* ファイルからインポートできます。 広く使われている規則を次に示します。

- *.props* ファイルは、インポート順序の早い段階でインポートします。

- *.targets* ファイルは、ビルド順序の後の方でインポートします。

この規則は、`<Project Sdk="SdkName">` のインポートによって適用されます (つまり、*Sdk.props* はファイルのすべての内容の前で最初にインポートされ、*Sdk.targets* はファイルのすべての内容の後で最後にインポートされます)。

プロパティを格納する場所を決定するときは、次の一般的なガイドラインを使います。

- 多くのプロパティについては、上書きされず、実行時にのみ読み取られるため、どこで定義してもかまいません。

- 個々のプロジェクトでカスタマイズされる可能性がある動作については、 *.props* ファイルで既定値を設定します。

- カスタマイズされている可能性のあるプロパティの値を読み取ることによって、 *.props* ファイルで依存プロパティを設定しないでください。カスタマイズは、MSBuild でユーザーのプロジェクトが読み取られるまで行われません。

- 依存プロパティは、 *.targets* ファイルで設定してください。そうすれば、個々のプロジェクトからカスタマイズが取得されます。

- プロパティをオーバーライドする必要がある場合は、ユーザー プロジェクトのすべてのカスタマイズが有効になる機会を持った後の、 *.targets* ファイルの中で行います。 派生プロパティを使うときは注意してください。派生プロパティのオーバーライドも必要な場合があります。

- *.props* ファイルで項目をインクルードします (プロパティの条件に応じて)。 すべての項目の前ですべてのプロパティが考慮されるので、ユーザー プロジェクトのプロパティのカスタマイズが取得され、これにより、ユーザーのプロジェクトでインポートによって取り込まれた項目を `Remove` または `Update` する機会があります。

- ターゲットは *.targets* ファイル内で定義します。 ただし、 *.targets* ファイルが SDK によってインポートされる場合は、ユーザーのプロジェクトによって既定でターゲットをオーバーライドする場所がないため、ターゲットのオーバーライドが難しくなることに注意してください。

- 可能であれば、ターゲット内のプロパティを変更するより、評価時にプロパティをカスタマイズするようにします。 このガイドラインに従うと、プロジェクトを読み込むこと、および何が行われているか理解することが、容易になります。

## <a name="msbuildprojectextensionspath"></a>MSBuildProjectExtensionsPath

既定では、*Microsoft.Common.props* は `$(MSBuildProjectExtensionsPath)$(MSBuildProjectFile).*.props` をインポートし、*Microsoft.Common.targets* は `$(MSBuildProjectExtensionsPath)$(MSBuildProjectFile).*.targets` をインポートします。 `MSBuildProjectExtensionsPath` の既定値は `$(BaseIntermediateOutputPath)`、`obj/` です。 NuGet はこのメカニズムを使って、パッケージに付随するビルド ロジックを参照します。つまり、復元時、パッケージの内容を参照する `{project}.nuget.g.props` ファイルが作成されます。

*Directory.Build.props* において、または *Microsoft.Common.props* をインポートする前に、`ImportProjectExtensionProps` プロパティを `false` に設定することによって、この拡張メカニズムを無効にできます。

> [!NOTE]
> MSBuildProjectExtensionsPath インポートを無効にすると、NuGet パッケージ付属のビルド ロジックがプロジェクトに適用されなくなります。 一部の NuGet パッケージでは、その機能を実行するためにビルド ロジックが必要であり、このインポートが無効になると役に立たなくなります。

## <a name="user-file"></a>.user ファイル

*Microsoft.Common.CurrentVersion.targets* では、存在する場合は `$(MSBuildProjectFullPath).user` がインポートされます。この追加拡張子でプロジェクトの隣にファイルを作成できます。 ソース管理にチェックインする予定の長期的な変更の場合、プロジェクト自体の変更をお勧めします。将来、保守管理を担当する人はこの拡張メカニズムについて知る必要がありません。

## <a name="msbuildextensionspath-and-msbuilduserextensionspath"></a>MSBuildExtensionsPath と MSBuildUserExtensionsPath

> [!WARNING]
> これらの拡張メカニズムを使用すると、コンピューター間で繰り返し可能なビルドを得ることが難しくなります。 ソース管理システムにチェックインし、コードベースのすべての開発者の間で共有できる構成を使用してみてください。

慣例的に、多くのコア ビルド ロジック ファイルでは、

```xml
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\{TargetFileName}\ImportBefore\*.targets
```

そのコンテンツの前、および

```xml
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\{TargetFileName}\ImportAfter\*.targets
```

後にインポートします。 この規則により、インストールされた SDK で、共通プロジェクト タイプのビルド ロジックを拡張できます。

同じディレクトリ構造が `$(MSBuildUserExtensionsPath)` で検索されます。これはユーザー別フォルダー *%LOCALAPPDATA%\Microsoft\MSBuild* です。 そのフォルダーに置かれたファイルは、そのユーザーの資格情報の下で実行される、該当するプロジェクト タイプのすべてのビルドでインポートされます。 このユーザー拡張は、パターン `ImportUserLocationsByWildcardBefore{ImportingFileNameWithNoDots}` でインポート ファイルに基づいて名前が付けられたプロパティを設定することで無効にできます。 たとえば、`ImportUserLocationsByWildcardBeforeMicrosoftCommonProps` を `false` に設定すると、`$(MSBuildUserExtensionsPath)\$(MSBuildToolsVersion)\Imports\Microsoft.Common.props\ImportBefore\*` がインポートされません。

## <a name="customize-the-solution-build"></a>ソリューション ビルドをカスタマイズする

> [!IMPORTANT]
> この方法によるソリューション ビルドのカスタマイズは、*MSBuild.exe* を持つコマンドライン ビルドにのみ適用されます。 Visual Studio 内のビルドには適用 **されません**。 このため、カスタマイズをソリューション レベルで行うことはお勧めしません。 ソリューション内のすべてのプロジェクトをカスタマイズする場合に推奨される代替手段は、この記事の他の部分で説明されているように、ソリューション フォルダー内の *Directory.Build.props* および *Directory.build.targets* ファイルを使用することです。

MSBuild でソリューション ファイルがビルドされるとき、最初に内部でプロジェクト ファイルに変換され、それからビルドされます。 生成されたプロジェクト ファイルは、ターゲットを定義する前に `before.{solutionname}.sln.targets` をインポートし、ターゲットをインポートした後に `after.{solutionname}.sln.targets` をインポートします。ターゲットには、`$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportBefore` ディレクトリと `$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportAfter` ディレクトリにインストールされたターゲットが含まれます。

たとえば、次のコードを含む *after.MyCustomizedSolution.sln.targets* という名前の同じディレクトリにファイルを作成することで、*MyCustomizedSolution.sln* のビルド後にカスタム ログ メッセージを書き込む新しいターゲットを定義できます。

```xml
<Project>
 <Target Name="EmitCustomMessage" AfterTargets="Build">
   <Message Importance="High" Text="The solution has completed the Build target" />
 </Target>
</Project>
```

ソリューション ビルドはプロジェクト ビルドとは別個のものなので、ここでの設定はプロジェクト ビルドには影響しません。

## <a name="customize-all-net-builds"></a>すべての .NET ビルドをカスタマイズする

ビルド サーバーを管理する場合は、サーバー上のすべてのビルドに対してグローバルに MSBuild 設定を構成することが必要な場合があります。  原理的には、グローバルな *Microsoft.Common.Targets* ファイルまたは *Microsoft.Common.Props* ファイルを変更することができますが、より優れた方法があります。 特定の MSBuild プロパティを使用し、特定のカスタムの `.targets` および `.props` ファイルを追加することで、特定のプロジェクト タイプ (すべての C# プロジェクトなど) のすべてのビルドに影響を与えることができます。

MSBuild または Visual Studio のインストールによって管理されているすべての C# または Visual Basic ビルドに影響を与えるには、*Microsoft.Common.targets* の前後に実行されるターゲットを使用してファイル *Custom.Before.Microsoft.Common.Targets* または *Custom.After.Microsoft.Common.Targets* を作成するか、*Microsoft.Common.props* の前後に処理されるプロパティを使用してファイル *Custom.Before.Microsoft.Common.Props* または *Custom.After.Microsoft.Common.Props* を作成します。

次の MSBuild プロパティを使用して、これらのファイルの場所を指定できます。

- CustomBeforeMicrosoftCommonProps
- CustomBeforeMicrosoftCommonTargets
- CustomAfterMicrosoftCommonProps
- CustomAfterMicrosoftCommonTargets
- CustomBeforeMicrosoftCSharpTargets
- CustomBeforeMicrosoftVisualBasicTargets
- CustomAfterMicrosoftCSharpTargets
- CustomAfterMicrosoftVisualBasicTargets

これらのプロパティの *Common* バージョンは、C# プロジェクトおよび Visual Basic プロジェクトの両方に影響を与えます。 これらのプロパティは、MSBuild コマンド ラインで設定できます。

```cmd
msbuild /p:CustomBeforeMicrosoftCommonTargets="C:\build\config\Custom.Before.Microsoft.Common.Targets" MyProject.csproj
```

最適な方法はご自身のシナリオによって異なります。 Visual Studio の機能拡張を使用して、ビルド システムをカスタマイズし、カスタマイズしたシステムのインストールおよび管理を行うためのメカニズムを提供できます。

専用のビルド サーバーがあり、そのサーバー上で実行される適切なプロジェクト タイプのすべてのビルドにおいて、特定のターゲットが必ず実行されるようにする場合は、グローバルなカスタムの `.targets` または `.props` ファイルを使用することをお勧めします。  特定の条件が適用される場合にのみカスタム ターゲットを実行したい場合は、別のファイルの場所を使用し、必要な場合にのみ MSBuild コマンド ラインで適切な MSBuild プロパティを設定することで、そのファイルへのパスを設定します。

> [!WARNING]
> Visual Studio では、一致する型のプロジェクトをビルドするときに MSBuild フォルダー内でカスタムの `.targets` または `.props` ファイルが見つかった場合、必ずそれらを使用します。 これにより、意図しない結果が生じる可能性があります。正しく実行されないと、コンピューター上での Visual Studio のビルド機能が無効になる場合があります。

## <a name="customize-c-builds"></a>C++ ビルドのカスタマイズ

C++ プロジェクトの場合、以前に説明したカスタム *.targets* と *.props* ファイルを同じ方法で使用して、既定の設定をオーバーライドすることはできません。 *Directory.Build.props* は、`Microsoft.Cpp.Default.props` でインポートされる *Microsoft.Common.props* によってインポートされます。一方、ほとんどの既定値は *Microsoft.Cpp.props* で定義されおり、多くのプロパティは既に定義されているため、"if not yet defined" 条件を使用できませんが、`PropertyGroup` で `Label="Configuration"` に定義されている特定のプロジェクト プロパティについては、既定値が異なっている必要があります (「[.vcxproj と .props ファイル構造](/cpp/build/reference/vcxproj-file-structure)」を参照してください)。

ただし、以下のプロパティを使用して、*Microsoft.Cpp.\** ファイルの前後に自動的にインポートされる *.props* ファイルを指定できます。

- ForceImportAfterCppDefaultProps
- ForceImportBeforeCppProps
- ForceImportAfterCppProps
- ForceImportBeforeCppTargets
- ForceImportAfterCppTargets

すべての C++ ビルドのプロパティの既定値をカスタマイズするには、別の *props* ファイル (たとえば、*MyProps.props*) を作成し、それを指す `Directory.Build.props` の `ForceImportAfterCppProps` プロパティを定義します。

<PropertyGroup> <ForceImportAfterCppProps>$(MsbuildThisFileDirectory)\MyProps.props<ForceImportAfterCppProps>
</PropertyGroup>

*MyProps.props* は、*Microsoft.Cpp.props* の末尾に自動的にインポートされます。

## <a name="customize-all-c-builds"></a>すべての C++ ビルドをカスタマイズする

このようなカスタマイズを追跡するのは簡単ではないため、Visual studio のインストールをカスタマイズすることは推奨されていません。特定のプラットフォームの C++ ビルドをカスタマイズするために Visual Studio を拡張する場合は、各プラットフォームの `.targets` ファイルを作成し、Visual studio 拡張機能の一部としてそれらのプラットフォーム用の適切なインポートフォルダーにそれらのファイルを配置します。

Win32 プラットフォーム用の `.targets` ファイルである *Microsoft.Cpp.Win32.targets* には、次の `Import` 要素が含まれています。

```xml
<Import Project="$(VCTargetsPath)\Platforms\Win32\ImportBefore\*.targets"
        Condition="Exists('$(VCTargetsPath)\Platforms\Win32\ImportBefore')"
/>
```

同じファイルの末尾付近にも、似た要素があります。

```xml
<Import Project="$(VCTargetsPath)\Platforms\Win32\ImportAfter\*.targets"
        Condition="Exists('$(VCTargetsPath)\Platforms\Win32\ImportAfter')"
/>
```

他のターゲット プラットフォーム用の似たインポート要素は、"*%ProgramFiles32%\MSBuild\Microsoft.Cpp\v{バージョン}\Platforms\*" に存在します。

プラットフォームに応じて適切な `ImportAfter` フォルダーに `.targets` ファイルを配置すると、MSBuild によって、そのプラットフォーム用のすべての C++ ビルドにファイルがインポートされます。 必要に応じて、複数の `.targets` ファイルをそこに置くことができます。 

Visual Studio の機能拡張を使用すると、新しいプラットフォームの定義など、さらに多くのカスタマイズを行うことができます。 詳細については、[C++ プロジェクトの拡張機能](../extensibility/visual-cpp-project-extensibility.md)に関するページを参照してください。

### <a name="specify-a-custom-import-on-the-command-line"></a>コマンド ラインでカスタム インポートを指定する

C++ プロジェクトの特定のビルドに追加したいカスタムの `.targets` のために、コマンド ラインでプロパティ `ForceImportBeforeCppTargets`、`ForceImportAfterCppTargets` のいずれかまたは両方を設定します。

```cmd
msbuild /p:ForceImportBeforeCppTargets="C:\build\config\Custom.Before.Microsoft.Cpp.Targets" MyCppProject.vcxproj
```

グローバル設定の場合 (たとえば、ビルド サーバー上の 1 つのプラットフォーム用のすべての C++ ビルドに影響を与える場合)、2 つの方法があります。 まず、常に設定されるシステム環境変数を使用して、これらのプロパティを設定できます。 これが機能するのは、MSBuild によって常に環境が読み取られ、すべての環境変数に対するプロパティが作成 (またはオーバーライド) されるためです。

## <a name="see-also"></a>関連項目

- [MSBuild の概念](../msbuild/msbuild-concepts.md)

- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
