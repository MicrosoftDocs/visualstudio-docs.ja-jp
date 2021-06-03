---
title: ビルド処理でのコード生成
description: Visual Studio ソリューションのビルド プロセスの一環として、テキスト変換を呼び出す方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: a785bf0fc337d1934efe4f47adaac7efe7f1f1b1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861804"
---
# <a name="invoke-text-transformation-in-the-build-process"></a>ビルド プロセスでテキスト変換を呼び出す

Visual Studio ソリューションの[ビルド プロセス](/azure/devops/pipelines/index)の一環として、[テキスト変換](../modeling/code-generation-and-t4-text-templates.md)を呼び出すことができます。 テキスト変換に特化したビルド タスクがあります。 T4 ビルド タスクはデザイン時テキスト テンプレートを実行し、また、実行時 (前処理済み) テキスト テンプレートをコンパイルします。

使用するビルド エンジンに応じて、ビルド タスクができることには違いが生じます。 Visual Studio でソリューションをビルドすると、[hostspecific="true"](../modeling/t4-template-directive.md) 属性が設定されている場合、テキスト テンプレートでは Visual Studio API (EnvDTE) にアクセスできます。 しかし、コマンド ラインからソリューションをビルドするとき、または、Visual Studio 経由でサーバー ビルドを開始するときは、これは当てはまりません。 このような場合、ビルドは MSBuild によって実行され、別の T4 ホストが使用されます。 つまり、MSBuild を使用してテキスト テンプレートをビルドすると、プロジェクト ファイル名などに同じようにアクセスできないことになります。 ただし、[ビルド パラメーターを使用してテキスト テンプレートとディレクティブ プロセッサに環境情報を渡す](#parameters)ことはできます。

## <a name="configure-your-machines"></a><a name="buildserver"></a> コンピューターを構成する

開発用コンピューターでビルド タスクを有効にするには、Visual Studio 用の Modeling SDK をインストールします。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Visual Studio がインストールされていないコンピューターで[自分のビルド サーバー](/azure/devops/pipelines/agents/agents)が実行されている場合、次のファイルを開発用コンピューターからビルド コンピューターにコピーします。

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\MSBuild\Microsoft\VisualStudio\v16.0\TextTemplating

  - Microsoft.VisualStudio.TextTemplating.Sdk.Host.15.0.dll
  - Microsoft.TextTemplating.Build.Tasks.dll
  - Microsoft.TextTemplating.targets

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

  - Microsoft.VisualStudio.TextTemplating.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.Interfaces.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.VSHost.15.0.dll

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\IDE\PublicAssemblies

  - Microsoft.VisualStudio.TextTemplating.Modeling.15.0.dll

> [!TIP]
> ビルド サーバーで TextTemplating ビルド ターゲットを実行しているときに、Microsoft.CodeAnalysis メソッドの `MissingMethodException` が表示された場合は、Roslyn アセンブリが、ビルド実行可能ファイルと同じディレクトリ (たとえば、*msbuild.exe*) 内の *Roslyn* という名前のディレクトリにあることを確認してください。

## <a name="edit-the-project-file"></a>プロジェクト ファイルを編集する

プロジェクト ファイルを編集して、たとえばテキスト変換ターゲットをインポートして MSBuild の一部の機能を構成します。

**ソリューション エクスプローラー** で、プロジェクトの右クリック メニューから **[アンロード]** を選択します。 これにより XML エディターで .csproj または .vbproj ファイルを編集できるようになります。 編集が完了したら、 **[再読み込み]** を選択します。

## <a name="import-the-text-transformation-targets"></a>テキスト変換ターゲットをインポートする

.vbproj ファイルまたは .csproj ファイルで、次のような行を探します。

`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`

\- または

`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`

この行の後に、テキスト テンプレートのインポートを挿入します。

::: moniker range=">=vs-2019"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets" />
```

::: moniker-end

::: moniker range="vs-2017"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets" />
```

::: moniker-end

## <a name="transform-templates-in-a-build"></a>ビルド時にテンプレートを変換する

プロジェクト ファイルに挿入して変換タスクを制御できるプロパティがいくつかあります。

- すべてのビルドの開始時に変換タスクを実行します。

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

- たとえばチェックアウトされていないために、読み取り専用であるファイルを上書きします。

    ```xml
    <PropertyGroup>
        <OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>
    </PropertyGroup>
    ```

- 毎回、すべてのテンプレートを変換します。

    ```xml
    <PropertyGroup>
        <TransformOutOfDateOnly>false</TransformOutOfDateOnly>
    </PropertyGroup>
    ```

     既定では、次のものより古い場合、T4 MSBuild タスクによって出力ファイルが再生成されます。

     - テンプレート ファイル
     - 含まれているファイル
     - テンプレートによって、またはテンプレートで使用するディレクティブ プロセッサによって前に読み込まれたファイル

     これは、テンプレートと出力ファイルの日付のみを比較する Visual Studio の **[すべてのテンプレートの変換]** コマンドで使用されるよりも、強力な依存関係テストです。

プロジェクトでテキスト変換だけを実行するには、TransformAll タスクを呼び出します。

`msbuild myProject.csproj /t:TransformAll`

特定のテキスト テンプレートを変換するには、次のように実行します。

`msbuild myProject.csproj /t:Transform /p:TransformFile="Template1.tt"`

TransformFile ではワイルドカードを使用できます。

`msbuild dsl.csproj /t:Transform /p:TransformFile="GeneratedCode\**\*.tt"`

## <a name="source-control"></a>ソース管理

ソース管理システムと連携するような専用の機能は組み込まれていません。 ただし、独自の拡張機能を追加して、たとえば生成されたファイルをチェックアウトしてチェックインすることができます。 既定では、テキスト変換タスクでは、読み取り専用としてマークされているファイルの上書きを回避します。 このようなファイルが検出されると、Visual Studio のエラー一覧にエラーが記録され、タスクは失敗します。

読み取り専用ファイルを上書きするには、次のプロパティを挿入します。

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

後処理のステップをカスタマイズしない限り、ファイルが上書きされるとエラー一覧に警告が記録されます。

## <a name="customize-the-build-process"></a>ビルド プロセスをカスタマイズする

テキスト変換は、ビルド処理で他のタスクよりも前に実行されます。 `$(BeforeTransform)` プロパティと `$(AfterTransform)` プロパティを設定して、変換の前後に呼び出すタスクを定義できます。

```xml
<PropertyGroup>
    <BeforeTransform>CustomPreTransform</BeforeTransform>
    <AfterTransform>CustomPostTransform</AfterTransform>
</PropertyGroup>
<Target Name="CustomPreTransform">
    <Message Text="In CustomPreTransform..." Importance="High" />
</Target>
<Target Name="CustomPostTransform">
    <Message Text="In CustomPostTransform..." Importance="High" />
</Target>
```

`AfterTransform` では、ファイルのリストを参照できます。

- GeneratedFiles: 処理中に出力されたファイルのリスト。 既存の読み取り専用ファイルを上書きしたファイルの場合、`%(GeneratedFiles.ReadOnlyFileOverwritten)` は true になります。 これらのファイルは、ソース管理からチェックアウトできます。

- NonGeneratedFiles: 上書きされなかった読み取り専用ファイルのリスト。

たとえば、GeneratedFiles をチェックアウトするタスクを定義します。

## <a name="outputfilepath-and-outputfilename"></a>OutputFilePath と OutputFileName

これらのプロパティを使用するのは MSBuild だけです。 Visual Studio のコード生成には影響しません。 これらは生成された出力ファイルを別のフォルダーまたはファイルにリダイレクトします。 対象となるフォルダーが既に存在する必要があります。

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFilePath>MyFolder</OutputFilePath>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

リダイレクト先として便利なフォルダーは `$(IntermediateOutputPath)` です。

出力ファイル名を指定した場合、テンプレートの出力ディレクティブで指定された拡張子より優先されます。

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFileName>MyOutputFileName.cs</OutputFileName>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

Visual Studio 内部でも **[すべて変換]** を使用してテンプレートを変換している場合、または単一ファイル ジェネレーターを実行している場合、OutputFileName または OutputFilePath を指定することはお勧めできません。 変換をどのようにして開始したのかに応じて、ファイル パスが変わります。 これはややこしい場合があります。

## <a name="add-reference-and-include-paths"></a>参照およびインクルード パスを追加する

ホストには、テンプレートで参照されているアセンブリを検索する既定のパス セットがあります。 このパス セットを追加するには、次のように指定します。

```xml
<ItemGroup>
    <T4ReferencePath Include="$(VsIdePath)PublicAssemblies\" />
    <!-- Add more T4ReferencePath items here -->
</ItemGroup>
```

インクルード ファイルを検索するフォルダーを設定するには、セミコロン区切りのリストを指定します。 通常は、既存のフォルダー リストに追加します。

```xml
<PropertyGroup>
    <IncludeFolders>
$(IncludeFolders);$(MSBuildProjectDirectory)\Include;AnotherFolder;And\Another</IncludeFolders>
</PropertyGroup>
```

## <a name="pass-build-context-data-into-the-templates"></a><a name="parameters"></a> テンプレートにビルド コンテキスト データを渡す

プロジェクト ファイルでパラメーター値を設定できます。 たとえば、[ビルド](../msbuild/msbuild-properties.md) プロパティや[環境変数](../msbuild/how-to-use-environment-variables-in-a-build.md)を渡すことができます。

```xml
<ItemGroup>
  <T4ParameterValues Include="ProjectFolder">
    <Value>$(ProjectDir)</Value>
    <Visible>false</Visible>
  </T4ParameterValues>
</ItemGroup>
```

テキスト テンプレートでは、template ディレクティブで `hostspecific` を設定します。 値を取得するには、[parameter](../modeling/t4-parameter-directive.md) ディレクティブを使用します。

```
<#@template language="c#" hostspecific="true"#>
<#@ parameter type="System.String" name="ProjectFolder" #>
The project folder is: <#= ProjectFolder #>
```

ディレクティブ プロセッサでは、[ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\)) を呼び出すことができます。

```csharp
string value = Host.ResolveParameterValue("-", "-", "parameterName");
```

```vb
Dim value = Host.ResolveParameterValue("-", "-", "parameterName")
```

> [!NOTE]
> `ResolveParameterValue` では、MSBuild を使用する場合に限り、`T4ParameterValues` からデータを取得します。 Visual Studio を使用してテンプレートを変換すると、パラメーターは既定値になります。

## <a name="use-project-properties-in-assembly-and-include-directives"></a><a name="msbuild"></a> assembly および include ディレクティブでプロジェクト プロパティを使用する

**$(SolutionDir)** などの Visual Studio のマクロは、MSBuild では動作しません。 その代わりに、プロジェクト プロパティを使用できます。

*.csproj* または *.vbproj* ファイルを編集してプロジェクトのプロパティを定義します。 この例では、**myLibFolder** という名前のプロパティを定義します。

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

これで、assembly ディレクティブおよび include ディレクティブでプロジェクト プロパティを使用できます。

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
<#@ include file="$(myLibFolder)\MyIncludeFile.t4" #>
```

これらのディレクティブは、MSBuild ホストおよび Visual Studio ホストの両方で T4parameterValues から値を取得します。

## <a name="q--a"></a>Q & A

**なぜビルド サーバーでテンプレートを変換するのですか。コードをチェックインする前に、Visual Studio で既にテンプレートを変換しました。**

インクルード ファイル、またはテンプレートで読み込まれる別のファイルを更新した場合、Visual Studio ではそのファイルは自動的に変換されません。 ビルドの一部としてテンプレートを変換すると、すべてが最新であることが保証されます。

**テキスト テンプレートを変換する方法は他にもありますか。**

- [TextTransform ユーティリティ](../modeling/generating-files-with-the-texttransform-utility.md)はコマンド スクリプトで使用できます。 ほとんどの場合、MSBuild を使用する方が簡単です。

- [Visual Studio 拡張機能でテキスト変換を呼び出します](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

- [デザイン時テキスト テンプレート](../modeling/design-time-code-generation-by-using-t4-text-templates.md)は Visual Studio によって変換されます。

- [実行時テキスト テンプレート](../modeling/run-time-text-generation-with-t4-text-templates.md)は、アプリケーションで実行時に変換されます。

## <a name="see-also"></a>関連項目

::: moniker range="vs-2017"

- T4 MSbuild テンプレート (`%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\msbuild\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets`) にガイダンスがあります

::: moniker-end

::: moniker range=">=vs-2019"

- T4 MSbuild テンプレート (`%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\msbuild\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets`) にガイダンスがあります

::: moniker-end

- [T4 テキスト テンプレートを作成する](../modeling/writing-a-t4-text-template.md)
