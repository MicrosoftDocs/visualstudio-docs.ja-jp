---
description: Visual C++ プロジェクト システムは、.vcxproj ファイルに使用されます。
title: Visual C++ プロジェクトの機能拡張
ms.date: 04/23/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
author: corob-msft
ms.author: corob
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fc538402ae39753f14a3bccd8bcd17ddb0081078
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221237"
---
# <a name="visual-studio-c-project-system-extensibility-and-toolset-integration"></a>Visual Studio C++ プロジェクト システムの機能拡張とツールセットの統合

Visual C++ プロジェクト システムは、.vcxproj ファイルに使用されます。 これは、[Visual Studio Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md) に基づいており、新しいツールセット、ビルド アーキテクチャ、およびターゲット プラットフォームの統合を容易にするための追加の C++ 固有の機能拡張ポイントを提供します。

## <a name="c-msbuild-targets-structure"></a>C++ MSBuild ターゲットの構造

すべての .vcxproj ファイルは、次のファイルをインポートします。

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.Default.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

これらのファイルが単独で定義されることはほとんどありません。 代わりに、次のプロパティ値に基づいて他のファイルをインポートします。

- `$(ApplicationType)`

   例: Windows Store、Android、Linux

- `$(ApplicationTypeRevision)`

   major.minor[.build[.revision]] 形式の有効なバージョン文字列を指定する必要があります。

   例: 1.0、10.0.0.0

- `$(Platform)`

   歴史的な理由で "プラットフォーム" の名前が付けられたビルド アーキテクチャ。

   例: Win32、x86、x64、ARM

- `$(PlatformToolset)`

   例: v140、v141、v141_xp、llvm

これらのプロパティ値によって、`$(VCTargetsPath)` ルート フォルダーの下にフォルダー名が指定されます。

> `$(VCTargetsPath)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;*Application Type*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationType)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationTypeRevision)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Platforms*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)` \
&nbsp;&nbsp;&nbsp;&nbsp;*Platforms*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`

`$(VCTargetsPath)`\\*Platforms*\\ フォルダーは、`$(ApplicationType)` が空のときに使用されます (Windows デスクトップ プロジェクトの場合)。

### <a name="add-a-new-platform-toolset"></a>新しいプラットフォーム ツールセットの追加

新しいツールセット (既存の Win32 プラットフォーム用の "MyToolset" など) を追加するには、`$(VCTargetsPath)` *\\Platforms\\Win32\\PlatformToolsets\\* の下に *MyToolset* フォルダーを作成し、その中に *Toolset.props* および *Toolset.targets* ファイルを作成します。

*PlatformToolsets* の下にある各フォルダー名が、以下に示すように、指定したプラットフォームの使用可能な **プラットフォーム ツールセット** として **[プロジェクトのプロパティ]** ダイアログに表示されます。

![プロジェクトの [プロパティ ページ] ダイアログの [プラットフォーム ツールセット] プロパティ](media/vc-project-extensibility-platform-toolset-property.png "プロジェクトの [プロパティ ページ] ダイアログの [プラットフォーム ツールセット] プロパティ")

このツールセットでサポートされている既存の各プラットフォーム フォルダーに、同様の *MyToolset* フォルダーと *Toolset.props* および *Toolset.targets* ファイルを作成します。

### <a name="add-a-new-platform"></a>新しいプラットフォームの追加

新しいプラットフォーム ("MyPlatform" など) を追加するには、`$(VCTargetsPath)` *\\Platforms\\* の下に *MyPlatform* フォルダーを作成し、その中に *Platform.default.props*、*Platform.props*、*Platform.targets* の各ファイルを作成します。 また、`$(VCTargetsPath)` *\\Platforms\\* <strong><em>MyPlatform</em></strong> *\\PlatformToolsets\\* フォルダーを作成し、その中にツールセットを少なくとも 1 つ作成します。

各 `$(ApplicationType)` および `$(ApplicationTypeRevision)` の *Platforms* フォルダーの下にあるすべてのフォルダー名が、プロジェクトに使用できる **プラットフォーム** の選択肢として IDE に表示されます。

![[新しいプロジェクト プラットフォーム] ダイアログの [新しいプラットフォーム] の選択肢](media/vc-project-extensibility-new-project-platform.png "[新しいプロジェクト プラットフォーム] ダイアログの [新しいプラットフォーム] の選択肢")

### <a name="add-a-new-application-type"></a>新しいアプリケーションの種類の追加

新しいアプリケーションの種類を追加するには、`$(VCTargetsPath)` *\\Application Type\\* の下に *MyApplicationType* フォルダーを作成し、その中に *Defaults.props* ファイルを作成します。 アプリケーションの種類には少なくとも 1 つのリビジョンが必要であるため、`$(VCTargetsPath)` *\\Application Type\\MyApplicationType\\1.0* フォルダーも作成し、その中に *Defaults.props* ファイルを作成します。 また、`$(VCTargetsPath)` *\\ApplicationType\\MyApplicationType\\1.0\\Platforms* フォルダーを作成し、その中にプラットフォームを少なくとも 1 つ作成する必要もあります。

`$(ApplicationType)` および `$(ApplicationTypeRevision)` プロパティは、ユーザー インターフェイスに表示されません。 それらはプロジェクト テンプレート内に定義され、プロジェクトの作成後は変更できません。

## <a name="the-vcxproj-import-tree"></a>.vcxproj インポート ツリー

Microsoft C++ の props および targets ファイルの簡略化されたインポート ツリーは次のようになります。

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore*\\*Default*\\\*.*props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Application Type*\\`$(ApplicationType)`\\*Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Application Type*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Application Type*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*Platforms*\\`$(Platform)`\\*Platform.default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter*\\*Default*\\\*.*props*

Windows デスクトップ プロジェクトでは `$(ApplicationType)` を定義しないため、以下だけをインポートします

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore*\\*Default*\\\*.*props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Platforms*\\`$(Platform)`\\*Platform.default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter*\\*Default*\\\*.*props*

`$(Platform)` プラットフォーム フォルダーの場所を保持するには、`$(_PlatformFolder)` プロパティを使用します。 このプロパティは、

> `$(VCTargetsPath)`\\*Platforms*\\`$(Platform)`

(Windows デスクトップ アプリの場合)、または

> `$(VCTargetsPath)`\\*Application Type*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*Platforms*\\`$(Platform)`

(その他すべての場合) です。

props ファイルは、次の順序でインポートされます。

> `$(VCTargetsPath)`\\*Microsoft.Cpp.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore*\\\*.*props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets*\\`$(PlatformToolset)`\\*Toolset.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter*\\\*.*props*

targets ファイルは、次の順序でインポートされます。

> `$(VCTargetsPath)`\\*Microsoft.Cpp.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Current.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore*\\\*.*targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets*\\`$(PlatformToolset)`\\*Toolset.target* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter*\\\*.*targets*

お使いのツールセットに既定のプロパティをいくつか定義する必要がある場合は、適切な ImportBefore および ImportAfter フォルダーにファイルを追加できます。

## <a name="author-toolsetprops-and-toolsettargets-files"></a>Toolset.props および Toolset.targets ファイルの作成

*Toolset.props* および *Toolset.targets* ファイルは、このツールセットが使用されているビルド中に発生する処理を完全に制御します。 また、使用可能なデバッガー、一部の IDE ユーザー インターフェイス ( **[プロパティ ページ]** ダイアログの内容など)、およびプロジェクト動作の他の側面も制御できます。

ツールセットはビルド プロセス全体をオーバーライドできますが、通常はお使いのツールセットで一部のビルド ステップを変更または追加したり、別のビルド ツールを既存のビルド プロセスの一部として使用したりする必要があるだけです。 この目標を達成するために、お使いのツールセットでインポートできる一般的な props および targets ファイルが多数あります。 ツールセットで実行する処理に応じて、以下のファイルをインポートまたは例として使用すると便利な場合があります。

- `$(VCTargetsPath)`\\*Microsoft.CppCommon.targets*

  このファイルでは、ネイティブ ビルド プロセスの主要部分を定義し、以下のインポートも行います。

  - `$(VCTargetsPath)`\\*Microsoft.CppBuild.targets*

  - `$(VCTargetsPath)`\\*Microsoft.BuildSteps.targets*

  - `$(MSBuildToolsPath)`\\*Microsoft.Common.Targets*

- `$(VCTargetsPath)`\\*Microsoft.Cpp.Common.props*

   Microsoft コンパイラを使用し、Windows を対象とするツールセットの既定値を設定します。

- `$(VCTargetsPath)`\\*Microsoft.Cpp.WindowsSDK.props*

   このファイルでは、Windows SDK の場所を決定し、Windows を対象とするアプリの重要なプロパティをいくつか定義します。

### <a name="integrate-toolset-specific-targets-with-the-default-c-build-process"></a>ツールセット固有のターゲットを既定の C++ ビルド プロセスと統合する

既定の C++ ビルド プロセスは、*Microsoft.CppCommon.targets* で定義されています。 そこにあるターゲットは特定のビルド ツールを呼び出しません。それらは主要なビルド ステップ、その順序、依存関係を指定するものです。

C++ ビルドには、次のターゲットで表される 3 つの主要ステップがあります。

- `BuildGenerateSources`

- `BuildCompile`

- `BuildLink`

各ビルド ステップは個別に実行される可能性があるため、あるステップで実行されているターゲットが、別のステップの一部として実行されるターゲットで定義されている項目のグループやプロパティを利用することはできません。 こうした区分により、特定のビルド パフォーマンスの最適化が可能になります。 既定では使用されませんが、引き続きこうした区別を受け入れることをお勧めします。

各ステップ内で実行されるターゲットは、以下のプロパティによって制御されます。

- `$(BuildGenerateSourcesTargets)`

- `$(BuildCompileTargets)`

- `$(BeforeBuildLinkTargets)`

各ステップには、Before および After プロパティもあります。

```xml
<Target
  Name="_BuildGenerateSourcesAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildGenerateSourcesTargets);$(BuildGenerateSourcesTargets);$(AfterBuildGenerateSourcesTargets)" />

<Target
  Name="\_BuildCompileAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildCompileTargets);$(BuildCompileTargets);$(AfterBuildCompileTargets)" />

<Target
  Name="\_BuildLinkAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildLinkTargets);$(BuildLinkTargets);$(AfterBuildLinkTargets)" />
```

各ステップに含まれているターゲットの例については、*Microsoft.CppBuild.targets* ファイルをご覧ください。

```xml
<BuildCompileTargets Condition="'$(ConfigurationType)'\!='Utility'">
  $(BuildCompileTargets);
  _ClCompile;
  _ResGen;
  _ResourceCompile;
  $(BuildLibTargets);
</BuildCompileTargets>
```

`_ClCompile` などのターゲットを確認すると、単独では何も行わず、その代わりに他のターゲット (`ClCompile` など) に依存していることがわかります。

```xml
<Target Name="_ClCompile"
  DependsOnTargets="$(BeforeClCompileTargets);$(ComputeCompileInputsTargets);MakeDirsForCl;ClCompile;$(AfterClCompileTargets)" >
</Target>
```

`ClCompile` とその他のビルド ツール固有のターゲットは、*Microsoft.CppBuild.targets* で空のターゲットとして定義されます。

```xml
<Target Name="ClCompile"/>
```

`ClCompile` ターゲットは空であるため、ツールセットによってオーバーライドされない限り、実際のビルド アクションは実行されません。 ツールセットのターゲットは `ClCompile` ターゲットをオーバーライドできます。つまり、*Microsoft.CppBuild.targets* のインポート後に、それらに別の `ClCompile` 定義を含めることができます。

```xml
<Target Name="ClCompile"
  Condition="'@(ClCompile)' != ''"
  DependsOnTargets="SelectClCompile">
  <!-- call some MSBuild tasks -->
</Target>
```

その名前 (Visual Studio でクロスプラットフォームのサポートを実装する前に作成されたもの) にもかかわらず、`ClCompile` ターゲットでは CL.exe を呼び出す必要がありません。 また、適切な MSBuild タスクを使用して、Clang、gcc、またはその他のコンパイラを呼び出すこともできます。

`ClCompile` ターゲットには、`SelectClCompile` ターゲット (1 つのファイル コンパイル コマンドが IDE で動作するために必要なもの) 以外の依存関係を含めることはできません。

## <a name="msbuild-tasks-to-use-in-toolset-targets"></a>ツールセットのターゲット内で使用する MSBuild タスク

実際のビルド ツールを呼び出すには、ターゲットで MSBuild タスクを呼び出す必要があります。 実行するコマンド ラインを指定できる基本的な [Exec タスク](../msbuild/exec-task.md)があります。 ただし、ビルドツールには通常、 インクリメンタル ビルドに備えて追跡するオプション、入力、出力が多数あるため、それら専用のタスクを用意するほうが理にかなっています。 たとえば、`CL` タスクでは MSBuild プロパティを CL.exe スイッチに変換して応答ファイルに書き込み、CL.exe を呼び出します。 また、後でインクリメンタル ビルドを行えるように、すべての入力および出力ファイルを追跡します。 詳細については、「[インクリメンタル ビルドと最新状態チェック](#incremental-builds-and-up-to-date-checks)」をご覧ください。

Microsoft.Cpp.Common.Tasks.dll には、以下のタスクが実装されています。

- `BSCMake`

- `CL`

- `ClangCompile` (clang-gcc スイッチ)

- `LIB`

- `LINK`

- `MIDL`

- `Mt`

- `RC`

- `XDCMake`

- `CustomBuild` (Exec と同じですが、入力と出力の追跡が含まれます)

- `SetEnv`

- `GetOutOfDateItems`

既存のツールと同じアクションを実行するツールと、(clang-cl や CL で実行するような) 同様のコマンド ライン スイッチを備えたツールがある場合は、両方に同じタスクを使用できます。

ビルド ツール用の新しいタスクを作成する必要がある場合は、次のオプションから選択できます。

1. このタスクをめったに使用しない場合、またはお使いのビルドで数秒が問題にならない場合は、MSBuild の "インライン" タスクを使用できます。

   - Xaml タスク (カスタム ビルド規則)

     Xaml タスク宣言の一例については `$(VCTargetsPath)`\\*BuildCustomizations*\\*masm.xml* を、その使用法については `$(VCTargetsPath)`\\*BuildCustomizations*\\*masm.targets* をそれぞれご覧ください。

   - [Code タスク](../msbuild/msbuild-inline-tasks.md)

1. タスク パフォーマンスを向上させたい場合、またはより複雑な機能を必要とするだけの場合は、通常の MSBuild [タスクの作成](../msbuild/task-writing.md)プロセスを使用します。

   `CL`、`MIDL`、`RC` の場合のように、ツールのすべての入力と出力がツールのコマンド ラインに一覧表示されるとは限らない場合で、自動入力および出力ファイルの追跡と .tlog ファイルの作成が必要な場合は、使用するタスクを `Microsoft.Build.CPPTasks.TrackedVCToolTask` クラスから派生させます。 現時点では、基底の [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) クラスに関するドキュメントはありますが、`TrackedVCToolTask` クラスの詳細についての例やドキュメントはありません。 これについて特別な関心をお持ちの場合は、[Developer Community](https://aka.ms/feedback/suggest?space=62) のリクエストにご意見をお寄せください。

## <a name="incremental-builds-and-up-to-date-checks"></a>インクリメンタル ビルドと最新状態チェック

MSBuild インクリメンタル ビルドの既定のターゲットでは、`Inputs` および `Outputs` 属性を使用します。 これらを指定すると、MSBuild では、いずれかの入力のタイムスタンプがすべての出力よりも新しい場合にのみターゲットを呼び出します。 ソース ファイルには他のファイルが含まれていたり、インポートされていたりすることが多く、またビルド ツールではツールのオプションに応じてさまざまな出力が生成されるため、考えられるすべての入力と出力を MSBuild のターゲット内に指定することは困難です。

この問題を管理するために、C++ のビルドでは、インクリメンタル ビルドをサポートする別の手法を使用します。 ほとんどのターゲットでは入力と出力を指定せず、結果としてそれらは常にビルド中に実行されます。 ターゲットによって呼び出されるタスクでは、すべての入力と出力に関する情報を、.tlog 拡張子を持つ *tlog* ファイルに書き込みます。 この .tlog ファイルは、後のビルドで、変更されたものと再構築が必要なもの、最新のものを確認するために使用されます。 また、.tlog ファイルは、IDE での既定のビルド最新状態チェックに使用される唯一のソースです。

すべての入力と出力を確認するために、ネイティブ ツール タスクでは tracker.exe と、MSBuild によって提供される [FileTracker](/dotnet/api/microsoft.build.utilities.filetracker) クラスを使用します。

Microsoft.Build.CPPTasks.Common.dll では、`TrackedVCToolTask` パブリック抽象基底クラスを定義します。 ほとんどのネイティブ ツール タスクは、このクラスから派生します。

Visual Studio 2017 Update15.8 以降では、Microsoft.Cpp.Common.Tasks.dll に実装されている `GetOutOfDateItems` タスクを使用して、既知の入力と出力を含むカスタム ターゲット用の .tlog ファイルを生成できます。
あるいは、`WriteLinesToFile` タスクを使用してそれらを作成することもできます。 `$(VCTargetsPath)`\\*BuildCustomizations*\\*masm.targets* に含まれる `_WriteMasmTlogs` ターゲットを例としてご覧ください。

## <a name="tlog-files"></a>.tlog ファイル

.tlog ファイルには、"*読み取り*"、"*書き込み*"、"*コマンド ライン*" の 3 つの種類があります。 読み取りと書き込みの .tlog ファイルは、インクリメンタル ビルドと IDE での最新状態チェックによって使用されます。 コマンド ラインの .tlog ファイルは、インクリメンタル ビルドでのみ使用されます。

MSBuild では、読み取りと書き込みの .tlog ファイルに以下のヘルパー クラスを提供します。

- [CanonicalTrackedInputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedinputfiles)

- [CanonicalTrackedOutputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedoutputfiles)

[FlatTrackingData](/dotnet/api/microsoft.build.utilities.flattrackingdata) クラスを使用すると、読み取りと書き込みの両方の .tlog ファイルにアクセスして、出力より新しい入力を特定できます。出力がない場合は、 最新状態チェックで使用されます。

コマンド ラインの .tlog ファイルには、ビルドで使用されるコマンド ラインに関する情報が含まれています。 これらは、最新状態チェックではなく、インクリメンタル ビルドにのみ使用されるため、それらを生成する MSBuild タスクによって内部形式が決定されます。

### <a name="read-tlog-format"></a>読み取りの .tlog の形式

"*読み取り*" の .tlog ファイル (\*.read.\*.tlog) には、ソース ファイルとその依存関係に関する情報が含まれています。

行の先頭にあるキャレット ( **^** ) は、1 つ以上のソースを示します。 同じ依存関係を共有するソースは、縦棒 ( **\|** ) で区切られます。

依存関係ファイルは、ソースの後にそれぞれ独自の行で一覧表示されます。 ファイル名はすべて完全なパスです。

たとえば、プロジェクトのソースが *F:\\test\\ConsoleApplication1\\ConsoleApplication1* にあるとします。 ソース ファイル (*Class1.cpp*) に以下の include が含まれている場合、

```cpp
#include "stdafx.h" //precompiled header
#include "Class1.h"
```

*CL.read.1.tlog* ファイルにはソース ファイルとその後にその依存関係が 2 つ含まれます。

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.CPP
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PCH
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.H
```

ファイル名を大文字で記述する必要はありませんが、一部のツールには便利です。

### <a name="write-tlog-format"></a>書き込みの .tlog の形式

"*書き込み*" の .tlog (\*.write.\*.tlog) ファイルは、ソースと出力を結び付けます。

行の先頭にあるキャレット ( **^** ) は、1 つ以上のソースを示します。 複数のソースは、縦棒 ( **\|** ) で区切られます。

ソースから作成された出力ファイルは、ソースの後にそれぞれ独自の行で一覧表示されます。 ファイル名はすべて完全なパスである必要があります。

たとえば、追加のソース ファイル *Class1.cpp* を持つ単純な ConsoleApplication プロジェクトの場合、*link.write.1.tlog* ファイルには以下が含まれている可能性があります。

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CLASS1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\STDAFX.OBJ
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.ILK
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.EXE
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PDB
```

## <a name="design-time-build"></a>デザイン時のビルド

IDE では、.vcxproj プロジェクトは一連の MSBuild ターゲットを使用して、プロジェクトから追加情報を取得し、出力ファイルを再生成します。 これらのターゲットの一部はデザイン時のビルドでのみ使用されますが、その多くは通常のビルドとデザイン時のビルドの両方で使用されます。

デザイン時のビルドに関する一般的な情報については、[デザイン時のビルド](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md)の CPS ドキュメントをご覧ください。 このドキュメントは、Visual C++ プロジェクトに部分的に適用されます。

デザイン時のビルドのドキュメントに記載されている `CompileDesignTime` および `Compile` ターゲットは、.vcxproj プロジェクトでは実行されません。 Visual C++ の .vcxproj プロジェクトでは、さまざまなデザイン時のターゲットを使用して、IntelliSense の情報を取得します。

### <a name="design-time-targets-for-intellisense-information"></a>IntelliSense の情報のためのデザイン時のターゲット

.vcxproj プロジェクトで使用されるデザイン時のターゲットは、`$(VCTargetsPath)`\\*Microsoft.Cpp.DesignTime.targets* で定義されています。

`GetClCommandLines` ターゲットでは、IntelliSense のコンパイラ オプションを収集します。

```xml
<Target
  Name="GetClCommandLines"
  Returns="@(ClCommandLines)"
  DependsOnTargets="$(DesignTimeBuildInitTargets);$(ComputeCompileInputsTargets)">
```

- `DesignTimeBuildInitTargets` – デザイン時のビルドの初期化に必要な、デザイン時のみのターゲット。 特に、これらのターゲットでは、パフォーマンスを向上させるために通常のビルド機能の一部を無効にします。

- `ComputeCompileInputsTargets` – コンパイラのオプションと項目を変更する一連のターゲット。 これらのターゲットは、デザイン時と通常の両方のビルドで実行されます。

このターゲットでは `CLCommandLine` タスクを呼び出して、IntelliSense に使用するコマンド ラインを作成します。 この場合も、その名前にかかわらず、CL オプションだけでなく、Clang や gcc オプションも処理できます。 コンパイラ スイッチの型は、`ClangMode` プロパティによって制御されます。

現在、`CLCommandLine` タスクによって生成されるコマンド ラインでは、IntelliSense エンジンが解析しやすくなるように、常に (Clang モードでも) CL スイッチを使用しています。

コンパイル前に実行されるターゲットを追加する場合は、通常またはデザイン時のどちらであっても、それによってデザイン時のビルドが中断されたり、パフォーマンスに影響したりしないようにしてください。 ターゲットをテストする最も簡単な方法は、開発者コマンド プロンプトを開き、以下のコマンドを実行することです。

```
msbuild /p:SolutionDir=*solution-directory-with-trailing-backslash*;Configuration=Debug;Platform=Win32;BuildingInsideVisualStudio=true;DesignTimebuild=true /t:\_PerfIntellisenseInfo /v:d /fl /fileloggerparameters:PerformanceSummary \*.vcxproj
```

このコマンドによって詳細なビルド ログ (*msbuild.log*) が生成されます。これには、ターゲットとタスクのパフォーマンスの概要が最後に示されます。

デザイン時のビルドではなく、通常のビルドにのみ意味を持つすべての操作では必ず `Condition ="'$(DesignTimeBuild)' != 'true'"` を使用してください。

### <a name="design-time-targets-that-generate-sources"></a>ソースを生成するデザイン時のターゲット

"*この機能はデスクトップのネイティブ プロジェクトでは既定で無効になっており、キャッシュされたプロジェクトでは現在サポートされていません。* "

プロジェクト項目に `GeneratorTarget` メタデータが定義されている場合は、プロジェクトが読み込まれるときとソース ファイルが変更されるときに、ターゲットが自動的に実行されます。

::: moniker range="vs-2017"

たとえば、.xaml ファイルから .cpp または .h ファイルを自動的に生成する場合は、`$(VSInstallDir)`\\*MSBuild*\\*Microsoft*\\*WindowsXaml*\\*v15.0*\\\*\\*Microsoft.Windows.UI.Xaml.CPP.Targets* ファイルで以下のエンティティを定義します。

::: moniker-end

::: moniker range=">=vs-2019"

たとえば、.xaml ファイルから .cpp または .h ファイルを自動的に生成する場合は、`$(VSInstallDir)`\\*MSBuild*\\*Microsoft*\\*WindowsXaml*\\*v16.0*\\\*\\*Microsoft.Windows.UI.Xaml.CPP.Targets* ファイルで以下のエンティティを定義します。

::: moniker-end

```xml
<ItemDefinitionGroup>
  <Page>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </Page>
  <ApplicationDefinition>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </ApplicationDefinition>
</ItemDefinitionGroup>
<Target Name="DesignTimeMarkupCompilation">
  <!-- BuildingProject is used in Managed builds (always true in Native) -->
  <!-- DesignTimeBuild is used in Native builds (always false in Managed) -->
  <CallTarget Condition="'$(BuildingProject)' != 'true' Or $(DesignTimeBuild) == 'true'" Targets="DesignTimeMarkupCompilationCT" />
</Target>
```

`Task.HostObject` を使用してソース ファイルの未保存のコンテンツを取得するには、ターゲットとタスクを、指定されたプロジェクトの [MsbuildHostObjects](/dotnet/api/microsoft.visualstudio.shell.interop.ivsmsbuildhostobject?view=visualstudiosdk-2017&preserve-view=true) として pkgdef に登録する必要があります。

```reg
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\]
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\\DesignTimeMarkupCompilationCT;CompileXaml\]
@="{83046B3F-8984-444B-A5D2-8029DEE2DB70}"
```

## <a name="visual-c-project-extensibility-in-the-visual-studio-ide"></a>Visual Studio IDE での Visual C++ プロジェクトの機能拡張

Visual C++ プロジェクト システムは [VS Project System](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md) に基づいており、その機能拡張ポイントが使用されます。 ただし、プロジェクト階層の実装は Visual C++ に固有であり、CPS に基づくものではないため、階層の機能拡張はプロジェクト項目に限定されます。

### <a name="project-property-pages"></a>[プロジェクト プロパティ] ページ

一般的な設計情報については、[VC++ プロジェクト用のフレームワークのマルチ ターゲット](https://devblogs.microsoft.com/visualstudio/framework-multi-targeting-for-vc-projects/)に関するページをご覧ください。

簡単に言えば、C++ プロジェクトの **[プロジェクト プロパティ]** ダイアログに表示されるプロパティ ページは、"*規則*" ファイルによって定義されます。 規則ファイルでは、プロパティ ページに表示する一連のプロパティ、およびそれらをプロジェクト ファイル内に保存する方法と場所を指定します。 規則ファイルは、Xaml 形式を使用する .xml ファイルです。 それらをシリアル化するために使用される型については、[Microsoft.Build.Framework.XamlTypes](/dotnet/api/microsoft.build.framework.xamltypes) に関するページをご覧ください。 プロジェクトでの規則ファイルの使用について詳しくは、「[プロパティ ページの XML 規則ファイル](/cpp/build/reference/property-page-xml-files)」をご覧ください。

規則ファイルは、`PropertyPageSchema` 項目グループに追加する必要があります。

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` メタデータは規則の可視性を制限し (規則の可視性は規則の種類によっても制御される)、これには以下の値のいずれかを指定できます。

`Project` | `File` | `PropertySheet`

CPS ではコンテキストの種類を表す他の値をサポートしていますが、Visual C++ プロジェクトでは使用されません。

規則が複数のコンテキストで表示されるようにする必要がある場合は、以下に示すように、コンテキスト値をセミコロン ( **;** ) で区切ります。

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>規則の形式と主な種類

規則形式は単純であるため、このセクションでは、ユーザー インターフェイスでの規則の表示方法に影響する属性についてのみ説明します。

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

`PageTemplate` 属性は、 **[プロパティ ページ]** ダイアログでの規則の表示方法を定義します。 この属性には、以下の値のいずれかを指定できます。

| 属性 | 説明 |
|------------| - |
| `generic` | すべてのプロパティが、カテゴリの見出しの下の 1 ページに表示されます。<br/>`Project` および `PropertySheet` コンテキストでは規則を表示できますが、`File` では表示できません。<br/><br/> 例: `$(VCTargetsPath)`\\*1033*\\*general.xml* |
| `tool` | カテゴリがサブページとして表示されます。<br/>すべてのコンテキスト (`Project`、`PropertySheet`、`File`) で規則を表示できます。<br/>規則が [プロジェクト プロパティ] に表示されるのは、その規則名が `ProjectTools` 項目グループに含まれている場合を除いて、`Rule.DataSource` で定義された `ItemType` を持つ項目がプロジェクトにある場合のみです。<br/><br/>例: `$(VCTargetsPath)`\\*1033*\\*clang.xml* |
| `debugger` | ページが、[デバッグ] ページの一部として表示されます。<br/>現在、カテゴリは無視されています。<br/>規則名は、デバッグ ランチャーの MEF オブジェクトの `ExportDebugger` 属性と一致している必要があり ます。<br/><br/>例: `$(VCTargetsPath)`\\*1033*\\*debugger\_local\_windows.xml* |
| *custom* | カスタム テンプレート。 テンプレートの名前は、`PropertyPageUIFactoryProvider` MEF オブジェクトの `ExportPropertyPageUIFactoryProvider` 属性と一致している必要があります。 **Microsoft.VisualStudio.ProjectSystem.Designers.Properties.IPropertyPageUIFactoryProvider** をご覧ください。<br/><br/> 例: `$(VCTargetsPath)`\\*1033*\\*userMacros.xml* |

規則でプロパティ グリッド ベースのテンプレートの 1 つを使用している場合は、以下の機能拡張ポイントをそのプロパティに使用できます。

- [プロパティ値のエディター](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [列挙値の動的プロバイダー](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>規則の拡張

既存の規則を使用したいが、いくつかのプロパティだけを追加または削除する必要がある場合は、[拡張規則](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md)を作成できます。

#### <a name="override-a-rule"></a>規則のオーバーライド

お使いのツールセットで、プロジェクトの既定の規則のほとんどを使用するが、そのうちの 1 つまたは一部だけは置き換えたいと考える場合があります。 たとえば、異なるコンパイラ スイッチを表示するように C/C++ の規則のみを変更するとします。 既存の規則と同じ名前と表示名を持つ新しい規則を指定し、既定の cpp ターゲットのインポート後にそれを `PropertyPageSchema` 項目グループに含めることができます。 プロジェクトでは所定の名前を持つ規則が 1 つだけ使用され、`PropertyPageSchema` 項目グループに含められた最後のものが優先されます。

#### <a name="project-items"></a>プロジェクト項目

*ProjectItemsSchema.xml* ファイルでは、プロジェクト項目として扱われる項目の `ContentType` および `ItemType` 値を定義し、新しいファイルの追加先となる項目グループを決定する `FileExtension` 要素を定義します。

既定の ProjectItemsSchema ファイルは `$(VCTargetsPath)`\\*1033*\\*ProjectItemsSchema.xml* にあります。 それを拡張するには、新しい名前 (*MyProjectItemsSchema.xml* など) でスキーマ ファイルを作成する必要があります。

```xml
<ProjectSchemaDefinitions xmlns="http://schemas.microsoft.com/build/2009/properties">

  <ItemType Name="MyItemType" DisplayName="C/C++ compiler"/>

  <ContentType
    Name="MyItems"
    DisplayName="My items"
    ItemType=" MyItemType ">
  </ContentType>

  <FileExtension Name=".abc" ContentType=" MyItems"/>

</ProjectSchemaDefinitions>
```

次に、ターゲット ファイルに以下を追加します。

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

例: `$(VCTargetsPath)`\\*BuildCustomizations*\\*masm.xml*

### <a name="debuggers"></a>デバッガー

Visual Studio のデバッグ サービスでは、デバッグ エンジンの機能拡張をサポートしています。 詳細については、以下のサンプルをご覧ください。

- [MIEngine (lldb デバッグをサポートするオープン ソース プロジェクト)](https://github.com/Microsoft/MIEngine)

- [Visual Studio デバッグ エンジンのサンプル](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

デバッグ セッション用のデバッグ エンジンとその他のプロパティを指定するには、[デバッグ ランチャー](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md)の MEF コンポーネントを実装し、`debugger` 規則を追加する必要があります。 例については、`$(VCTargetsPath)`\\1033\\debugger\_local\_windows.xml ファイルをご覧ください。

### <a name="deploy"></a>デプロイ

.vcxproj プロジェクトでは、[デプロイ プロバイダー](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md)に Visual Studio プロジェクト システムの機能拡張を使用します。

### <a name="build-up-to-date-check"></a>ビルドの最新状態チェック

既定では、ビルドの最新状態チェックには、ビルド中に `$(TlogLocation)` フォルダーに作成される、すべてのビルド入力および出力用の読み取り .tlog および書き込み .tlog ファイルが必要です。

カスタムの最新状態チェックを使用するには:

1. *Toolset.targets* ファイルに `NoVCDefaultBuildUpToDateCheckProvider` 機能を追加して、既定の最新状態チェックを無効にします。

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. 独自の [IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md) を実装します。

## <a name="project-upgrade"></a>プロジェクトのアップグレード

### <a name="default-vcxproj-project-upgrader"></a>既定の .vcxproj プロジェクト アップグレード プログラム

既定の .vcxproj プロジェクト アップグレード プログラムでは、`PlatformToolset`、`ApplicationTypeRevision`、MSBuild ツールセットのバージョン、.Net Framework を変更します。 最後の 2 つは常に Visual Studio バージョンの既定値に変更されますが、`PlatformToolset` と `ApplicationTypeRevision` は特別な MSBuild プロパティによって制御できます。

このアップグレード プログラムでは、以下の基準を使用して、プロジェクトをアップグレードできるかどうかを判断します。

1. `ApplicationType` と `ApplicationTypeRevision` を定義するプロジェクトの場合、リビジョン番号が現在のものよりも高いフォルダーが存在する。

1. 現在のツールセットに `_UpgradePlatformToolsetFor_<safe_toolset_name>` プロパティが定義されており、その値が現在のツールセットと等しくない。

   これらのプロパティ名で、 *\<safe_toolset_name>* は英数字以外のすべて文字がアンダースコア ( **\_** ) で置き換えられたツールセット名を表します。

プロジェクトをアップグレードできる場合は、"*ソリューションの再ターゲット*" に加えられます。 詳細については、[IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2) に関するページをご覧ください。

プロジェクトで特定のツールセットを使用する場合に **ソリューション エクスプローラー** でプロジェクト名を装飾するには、`_PlatformToolsetShortNameFor_<safe_toolset_name>` プロパティを定義します。

`_UpgradePlatformToolsetFor_<safe_toolset_name>` および `_PlatformToolsetShortNameFor_<safe_toolset_name>` プロパティの定義の例については、*Microsoft.Cpp.Default.props* ファイルをご覧ください。 使用例については、`$(VCTargetPath)`\\*Microsoft.Cpp.Platform.targets* ファイルをご覧ください。

### <a name="custom-project-upgrader"></a>カスタムのプロジェクト アップグレード プログラム

カスタムのプロジェクト アップグレード プログラム オブジェクトを使用するには、以下に示すように MEF コンポーネントを実装します。

```csharp
/// </summary>
[Export("MyProjectUpgrader", typeof(IProjectRetargetHandler))]
[Export(typeof(IProjectRetargetHandler))]
[ExportMetadata("Name", "MyProjectUpgrader")]
[OrderPrecedence(20)]
[PartMetadata(ProjectCapabilities.Requires, ProjectCapabilities.VisualC)]

internal class MyProjectUpgrader: IProjectRetargetHandler
{
    // ...
}
```

コードでは、既定の .vcxproj アップグレード プログラム オブジェクトをインポートして呼び出すことができます。

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` は *Microsoft.VisualStudio.ProjectSystem.VS.dll* で定義され、`IVsRetargetProjectAsync` に似ています。

`VCProjectUpgraderObjectName` プロパティを定義して、プロジェクト システムにカスタムのアップグレード プログラム オブジェクトを使用するよう指示します。

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>MyProjectUpgrader</VCProjectUpgraderObjectName>
</PropertyGroup>
```

#### <a name="disable-project-upgrade"></a>プロジェクトのアップグレードの無効化

プロジェクトのアップグレードを無効にするには、`NoUpgrade` 値を使用します。

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>NoUpgrade</VCProjectUpgraderObjectName>
</PropertyGroup>
```

## <a name="project-cache-and-extensibility"></a>プロジェクト キャッシュと機能拡張

Visual Studio 2017 で大規模な C++ ソリューションを使用するときのパフォーマンスを向上させるために、[プロジェクト キャッシュ](https://devblogs.microsoft.com/cppblog/faster-c-solution-load-with-vs-15/)が導入されました。 これは、プロジェクト データを格納する SQLite データベースとして実装された後、MSBuild または CPS プロジェクトをメモリに読み込まずにプロジェクトを読み込むために使用されます。

キャッシュから読み込まれた .vcxproj プロジェクトには CPS オブジェクトが存在しないため、`UnconfiguredProject` または `ConfiguredProject` をインポートする拡張機能の MEF コンポーネントを作成できません。 機能拡張をサポートするため、プロジェクトで MEF 拡張機能が使用される (または使用される可能性がある) かどうかを Visual Studio で検出するときに、プロジェクト キャッシュは使用されません。

以下の種類のプロジェクトは常に完全に読み込まれ、メモリ内に CPS オブジェクトが存在するため、すべての MEF 拡張機能が作成されます。

- スタートアップ プロジェクト

- カスタムのプロジェクト アップグレード プログラムを持つ (つまり、`VCProjectUpgraderObjectName` プロパティが定義されている) プロジェクト

- Desktop Windows を対象としない (つまり、`ApplicationType` プロパティが定義されている) プロジェクト

- 共有項目プロジェクト (.vcxitems) と、.vcxitems プロジェクトのインポートによってそれらを参照するすべてのプロジェクト。

これらの条件がいずれも検出されない場合は、プロジェクト キャッシュが作成されます。 このキャッシュには、`VCProjectEngine` インターフェイス上で `get` クエリに応答するために必要な MSBuild プロジェクトからのデータがすべて含まれています。 これは、拡張機能によって実行される、MSBuild の props および targets ファイル レベルでの変更がすべて、キャッシュから読み込まれたプロジェクトでのみ機能する必要があることを意味します。

## <a name="shipping-your-extension"></a>拡張機能の配布

VSIX ファイルを作成する方法については、「[Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」をご覧ください。 特別なインストール場所にファイルを追加する (たとえば、`$(VCTargetsPath)` の下にファイルを追加する) 方法については、「[拡張機能フォルダー外でのインストール](../extensibility/set-install-root.md)」をご覧ください。

## <a name="additional-resources"></a>その他の技術情報

Microsoft Build System ([MSBuild](../msbuild/msbuild.md)) は、ビルド エンジンと拡張可能な XML ベースの形式をプロジェクト ファイルに提供します。 Visual C++ プロジェクト システムを拡張するためには、基本的な [MSBuild の概念](../msbuild/msbuild-concepts.md)と [Visual C++ 向け MSBuild](/cpp/build/reference/msbuild-visual-cpp-overview) のしくみを理解しておく必要があります。

Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) には、CPS および Visual C++ プロジェクト システムで使用される拡張機能 API が用意されています。 CPS による MEF の使用方法の概要については、[VSProjectSystem での MEF の 概要](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md)のページに記載されている [CPS と MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef) に関するセクションをご覧ください。

既存のビルド システムをカスタマイズして、ビルド ステップまたは新しいファイルの種類を追加できます。 詳細については、[MSBuild (Visual C++) の概要](/cpp/build/reference/msbuild-visual-cpp-overview)と[プロジェクト プロパティの操作](/cpp/build/working-with-project-properties)に関するそれぞれのページをご覧ください。
