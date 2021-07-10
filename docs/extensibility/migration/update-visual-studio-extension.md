---
title: Visual Studio の拡張機能を更新する
description: Visual Studio の拡張機能を Visual Studio 2022 で動作するように更新する方法について説明します。
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 512e9a71cde5ca29c737c1623aa0c8f9c37dd60d
ms.sourcegitcommit: 0499d813d5c24052c970ca15373d556a69507250
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "113046132"
---
# <a name="update-a-visual-studio-extension-for-visual-studio-2022"></a>Visual Studio の拡張機能を Visual Studio 2022 用に更新する

> [!IMPORTANT]
> このガイドのアドバイスは、Visual Studio 2019 と 2022 の両方で動作させるために大きな変更を必要とする拡張機能の移行について、開発者にガイドを示すことを目的としています。 そのような場合は、2 つの VSIX プロジェクトと条件付きコンパイルを使用することをお勧めします。
> 多くの拡張機能は、軽微な変更を行えば Visual Studio 2019 と 2022 の両方で動作するようになり、このガイドにある拡張機能の最新化に関するアドバイスに従う必要はありません。
> ご自身の拡張機能を Visual Studio 2022 で試し、ご自身の拡張機能に最適なオプションは何かを評価してください。

このガイドに従って、拡張機能を Visual Studio 2022 Preview で動作するように更新できます。 Visual Studio 2022 Preview は 64 ビット アプリケーションであり、VS SDK にいくつかの破壊的変更が加えられています。 このガイドでは、Visual Studio 2022 の現在のプレビューで拡張機能を動作させるために必要な手順について説明します。これにより、Visual Studio 2022 が GA に達する前にユーザーが拡張機能をインストールできるようになります。

## <a name="installing"></a>インストール

Visual Studio 2022 Preview は、[Visual Studio 2022 Preview のダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022)からインストールします。

### <a name="extensions-written-in-a-net-language"></a>.NET 言語で記述された拡張機能

マネージド拡張機能用の Visual Studio 2022 をターゲットとする VS SDK は、NuGet に "*のみ*" 用意されています。

- [Microsoft.VisualStudio.Sdk](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) (17.x バージョン) メタパッケージには、必要な参照アセンブリのほとんどまたはすべてが含まれています。
- [Microsoft.VSSDK.BuildTools](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools/) (17.x バージョン) パッケージは、Visual Studio 2022 準拠の VSIX をビルドできるように VSIX プロジェクトから参照する必要があります。

拡張機能は、"任意の CPU" または "x64" プラットフォームでコンパイルする "*必要があります*"。 "x86" プラットフォームは、Visual Studio 2022 の 64 ビット プロセスと互換性がありません。

### <a name="extensions-written-in-c"></a>C++ で記述された拡張機能

C++ でコンパイルした拡張機能の VS SDK は、通常どおり、インストールした Visual Studio SDK で使用できます。

拡張機能は、Visual Studio 2022 SDK および amd64 専用にコンパイルする "*必要があります*"。

### <a name="update-your-extension-to-visual-studio-2022"></a>拡張機能を Visual Studio 2022 に更新する

#### <a name="extensions-with-running-code"></a>実行されるコードを含む拡張機能

実行されるコードを含む拡張機能は、Visual Studio 2022 専用にコンパイルする "*必要があります*"。 Visual Studio 2022 を専用ターゲットとしない拡張機能は Visual Studio 2022 に読み込まれません。

Visual Studio 2022 以前の拡張機能を Visual Studio 2022 に移行する方法は次のとおりです。

1. [プロジェクトを最新化します](#modernize-your-vsix-project)。
1. Visual Studio 2022 およびそれ以前のバージョンをターゲットにできるように、[ソース コードを共有プロジェクトにリファクタリング](#use-shared-projects-for-multi-targeting)します。
1. [Visual Studio 2022 をターゲットにした VSIX プロジェクト](#add-a-visual-studio-2022-target)と、[パッケージまたはアセンブリの再マッピング テーブル](migrated-assemblies.md)を追加します。
1. [必要なコード調整を行います](#handle-breaking-api-changes)。
1. [Visual Studio 2022 拡張機能をテストします](#test-your-extension)。
1. [Visual Studio 2022 拡張機能を公開します](#publish-your-extension)。

#### <a name="extensions-without-running-code"></a>実行されるコードを含まない拡張機能

実行されるコード (プロジェクトまたは項目テンプレートなど) を含まない拡張機能は、2 つの異なる VSIX の生成を含む上記の手順に従う必要は "*ありません*"。

代わりに、1 つの VSIX を変更して、次のように 2 つのインストール ターゲットを `source.extension.vsixmanifest` ファイルで宣言する必要があります。

```xml
<Installation>
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0,17.0)">
      <ProductArchitecture>x86</ProductArchitecture>
   </InstallationTarget>
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
</Installation>
```

この記事にある共有プロジェクトと複数の VSIX の使用についての手順は省略できます。 [テスト](#test-your-extension)を続行できます。

> [!NOTE]
> Visual Studio 2022 Preview を使用して *新しい* Visual Studio 拡張機能を作成し、(同時に) Visual Studio 2019 またはそれ以前のバージョンもターゲットとする場合は、[こちらのガイド](target-previous-versions.md)を参照してください。

### <a name="msbuild-tasks"></a>MSBuild タスク

MSBuild タスクを作成する場合は、Visual Studio 2022 では、64 ビットの MSBuild.exe プロセスに読み込まれる可能性が高いことに注意してください。 タスクの実行に 32 ビット プロセスが必要な場合は、[こちらの MSBuild ドキュメント](../../msbuild/how-to-configure-targets-and-tasks.md#usingtask-attributes-and-task-parameters)を参照し、MSBuild でタスクが 32 ビット プロセスに読み込まれるようにしてください。

## <a name="modernize-your-vsix-project"></a>VSIX プロジェクトを最新化する

拡張機能に Visual Studio 2022 のサポートを追加する前に、ここで時間を取って、既存のプロジェクトに次のようなクリーンアップと最新化を行ってから先に進むことを強くお勧めします。

1. [packages.config から `PackageReference` に移行します](/nuget/consume-packages/migrate-packages-config-to-package-reference)。

1. 直接アセンブリの VS SDK アセンブリ参照を PackageReference 項目に置き換えます。

   ```diff
   -<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   +<PackageReference Include="Microsoft.VisualStudio.OLE.Interop" Version="..." />
   ```

   > [!TIP]
   > "*複数*" のアセンブリ参照を、メタパッケージへの "*1 個*" の PackageReference だけで置き換えることができます。
   >
   >```diff
   >-<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop.8.0" />
   >+<PackageReference Include="Microsoft.VisualStudio.Sdk" Version="..." />
   >```

   必ず、ターゲットとする Visual Studio の最小バージョンと一致するパッケージのバージョンを選択します。

   VS SDK に固有ではない一部のアセンブリ (Newtonsoft.Json.dll など) は、Visual Studio 2022 以前は単純な `<Reference Include="Newtonsoft.Json" />` 参照を使用して検出できていたかもしれませんが、Visual Studio 2022 ではパッケージ参照とする必要があります。これは、Visual Studio 2022 では MSBuild の既定のアセンブリ検索パスから一部の Visual Studio ランタイムおよび SDK ディレクトリが削除されたためです。

   直接アセンブリ参照から NuGet パッケージ参照に切り替える場合に、NuGet で依存関係の推移閉包が自動的にインストールされるため、追加のアセンブリ参照とアナライザー パッケージを選択することがあります。 これは通常は問題ありませんが、ビルド中に追加の警告フラグが設定される可能性があります。 このような警告を確認し、できるだけ多くを解決して、解決できない警告はコード内の `#pragma warning disable <id>` 領域を使用して抑制することを検討してください。

## <a name="use-shared-projects-for-multi-targeting"></a>マルチターゲット用に共有プロジェクトを使用する

[共有プロジェクト](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows)は、Visual Studio 2015 で導入されたプロジェクトの種類です。 Visual Studio の共有プロジェクトを使用すると、ソース コード ファイルを複数のプロジェクト間で共有し、条件付きコンパイル シンボルと一意の参照セットを使用して、異なる方法でビルドできます。

Visual Studio 2022 では、以前のすべてのバージョンの個別の参照アセンブリが必要です。そのため、このガイダンスでは共有プロジェクトを使用して簡便に、Visual Studio 2022 以前と Visual Studio 2022 (および以降のバージョン) を拡張機能のマルチターゲットとします。これにより、コードを共有しつつ個別の参照となります。

Visual Studio 拡張機能のコンテキストでは、Visual Studio 2022 以降用に 1 つの VSIX プロジェクトと、Visual Studio 2019 以前用に 1 つの VSIX プロジェクトを使用できます。 これらの各プロジェクトには、`source.extension.vsixmanifest` と、16.x SDK または 17.x SDK へのパッケージ参照が含まれています。 また、これらの VSIX プロジェクトには、2 つの VS バージョン間で共有できるすべてのソース コードをホストする新しい共有プロジェクトへの共有プロジェクト参照も含まれています。

開始点として、このドキュメントでは、Visual Studio 2019 をターゲットとする VSIX プロジェクトが既に存在し、拡張機能を Visual Studio 2022 で機能させると想定しています。

これらの手順はすべて Visual Studio 2019 を使用して完了できます。

1. まだ行ってない場合は、[プロジェクトを最新化](#modernize-your-vsix-project)してください。この更新プロセスの後の手順が容易になります。

1. VS SDK を参照する既存のプロジェクトごとに、ソリューションに新しい共有プロジェクトを追加します。
   ![新しいプロジェクトを追加するコマンド](media/update-visual-studio-extension/add-new-project.png)
   ![新しいプロジェクトのテンプレート](media/update-visual-studio-extension/new-shared-project-template.png)

1. 各 VS SDK 参照プロジェクトから、対応する共有プロジェクトへの参照を追加します。
   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="共有プロジェクト参照を追加する" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. 各 VS SDK 参照プロジェクトから対応する共有プロジェクトにすべてのソース コード (.cs、.resx を含む) を移動します。
`source.extension.vsixmanifest` ファイルは VSIX プロジェクトに残しておきます。
   ![すべてのソース ファイルが含まれている共有プロジェクト](media/update-visual-studio-extension/source-files-in-shared-project.png)

1. メタデータ ファイル (リリース ノート、ライセンス、アイコンなど) と VSCT ファイルを共有ディレクトリに移動し、リンク ファイルとして VSIX プロジェクトに追加する必要があります。
   ![メタデータおよび VSCT ファイルをリンク ファイルとして追加する](media/update-visual-studio-extension/add-linked-items-to-vsix.png)
    - メタデータ ファイルの場合は、BuildAction を `Content` に設定し、[VSIX に含める] を `true` に設定します。

      ![VSIX にメタデータ ファイルを含める](./media/update-visual-studio-extension/include-metadata-files-in-vsix.png)
    - VSCT ファイルの場合は、BuildAction を `VSCTCompile` に設定し、VSIX には含めません。
      この設定がサポートされていないと Visual Studio に表示される場合がありますが、プロジェクトをアンロードして `Content` を `VSCTCompile` に変更することによって、ビルド アクションを変更できます。

    ```diff
    -<Content Include="..\SharedFiles\VSIXProject1Package.vsct">
    -  <Link>VSIXProject1Package.vsct</Link>
    -</Content>
    +<VSCTCompile Include="..\SharedFiles\VSIXProject1Package.vsct">
    +  <Link>VSIXProject1Package.vsct</Link>
    +  <ResourceName>Menus.ctmenu</ResourceName>
    +</VSCTCompile>
    ```

      ![VSCT ファイルを VSCTCompile として設定する](media/update-visual-studio-extension/build-linked-vsct-files.png)

1. プロジェクトをビルドし、新しいエラーが発生していないことを確認します。

これで、プロジェクトに Visual Studio 2022 のサポートを追加する準備ができました。

## <a name="add-a-visual-studio-2022-target"></a>Visual Studio 2022 のターゲットを追加する

このドキュメントは、[共有プロジェクトを使用して Visual Studio 拡張機能を組み込む](#use-shared-projects-for-multi-targeting)手順を完了していることを前提としています。

Visual Studio 2022 のサポートを拡張機能に追加する手順に進みます。この手順は Visual Studio 2019 を使用して実行できます。

1. ソリューションに新しい VSIX プロジェクトを追加します。 これは、Visual Studio 2022 をターゲットとするプロジェクトです。 テンプレートにあらかじめ含まれているソース コードは削除しますが、" *`source.extension.vsixmanifest` ファイルは残しておきます*"。

1. 新しい VSIX プロジェクトで、Visual Studio 2019 をターゲットとする VSIX で参照しているのと同じ共有プロジェクトへの共有プロジェクト参照を追加します。

   ![1 つの共有プロジェクトと 2 つの VSIX プロジェクトを含むソリューション](media/update-visual-studio-extension/shared-project-with-two-heads.png)

1. 新しい VSIX プロジェクトが正しくビルドされることを確認します。 コンパイラ エラーを解決するために、元の VSIX プロジェクトと一致する参照を追加することが必要になる場合があります。

1. マネージド VS 拡張機能の場合は、NuGet パッケージ マネージャーを使用するか、プロジェクト ファイルを直接編集して、Visual Studio 2022 をターゲットとするプロジェクト ファイル内のパッケージ参照を 16.x (またはそれ以前) から 17.x パッケージ バージョンに更新します。

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    ```

   nuget.org から実際に使用できるバージョンを使用することになります。前に使用したものはデモンストレーションのみを目的としています。

   多くの場合、パッケージ ID は変更されています。 Visual Studio 2022 での変更点の一覧については、[パッケージまたはアセンブリのマッピング テーブル](migrated-assemblies.md)を参照してください。

   C++ で記述された拡張機能には、コンパイルに使用できる SDK がまだありません。

1. C++ プロジェクトの場合は、amd64 用にコンパイルする必要があります。 マネージド拡張機能の場合は、Visual Studio 2022 で拡張機能が常に 64 ビット プロセスに読み込まれることを反映するように、プロジェクトを任意の CPU 用のビルドから `x64` をターゲットにするよう変更することを検討してください。 `Any CPU` でも問題はありませんが、x64 専用のネイティブ バイナリを参照すると警告が生成される場合があります。

   拡張機能にネイティブ モジュールに対する依存関係がある場合、それを x86 イメージから amd64 イメージに更新する必要があります。

1. `source.extension.vsixmanifest` ファイルを編集し、ターゲットの Visual Studio 2022 が反映されるようにします。 `<InstallationTarget>` タグを設定し、Visual Studio 2022 が反映され、amd64 ペイロードが示されるようにします。

   ```xml
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
   ```

   Visual Studio 2019 では、このファイルのデザイナーに新しい `ProductArchitecture` 要素が公開されないので、この変更は、**ソリューション エクスプローラー** で **[ファイルを開くアプリケーションの選択]** コマンドを使用してアクセスできる xml エディターで行う必要があります。

   この `ProductArchitecture` 要素は重要です。 それがないと、拡張機能が Visual Studio 2022 にインストール "*されません*"。

   | 要素 | 値 | 説明 |
   | - | - | - |
   | ProductArchitecture | X86、AMD64 | この VSIX でサポートされているプラットフォーム。 大文字と小文字は区別されません。 要素ごとに 1 つのプラットフォーム、InstallTarget ごとに 1 つの要素。 製品バージョンが 17.0 未満の場合、既定値は x86 であり、省略できます。  製品バージョン 17.0 以上の場合、この要素は必須であり、既定値はありません。 Visual Studio 2022 の場合、この要素の有効なコンテンツは "amd64" のみです。 |

1. source.extension.vsixmanifest で、Visual Studio 2019 をターゲットとするものに一致するように、必要なその他の調整 (ある場合) を行います。 マニフェストの `Identity` 要素にある VSIX の ID が、両方の拡張機能で同一であることが重要です。

この時点で、Visual Studio 2022 をターゲットにした拡張機能の VSIX ができます。 Visual Studio 2022 をターゲットにした VSIX プロジェクトをビルドし、[表示されるビルドの中断を処理する](#handle-breaking-api-changes)必要があります。 Visual Studio 2022 をターゲットにした VSIX プロジェクトにビルドの中断がなければ、テストの準備ができています。

## <a name="handle-breaking-api-changes"></a>API の破壊的変更を処理する

Visual Studio 2022 には [API の破壊的変更](breaking-api-list.md)があり、コードに対して、以前のバージョンで実行していたときとは異なる変更が必要になる場合がます。 それぞれの場合にコードを更新する方法に関するヒントについては、そのドキュメントを参照してください。

コードを調整する場合は、[条件付きコンパイル](#use-conditional-compilation-symbols)を使用することをお勧めします。そうすれば、Visual Studio 2022 のサポートを追加しながら、2022 より前の Visual Studio を引き続きサポートできるコードになります。

Visual Studio 2022 をターゲットにした拡張機能をビルドしたら、[テスト](#test-your-extension)に進みます。

## <a name="use-conditional-compilation-symbols"></a>条件付きコンパイル シンボルを使用する

Visual Studio 2022 と以前のバージョンに同じソース コードを使用する場合は、同じファイルであっても、破壊的変更に適応するためにコードをフォークできるように、条件付きコンパイルを使用することが必要な場合があります。 条件付きコンパイルは、C#、Visual Basic、および C++ 言語の機能であり、特定の場所で固有の API に対応しながら、ほとんどのコードを共有するために使用できます。

プリプロセッサ ディレクティブと条件付きコンパイル シンボルの使用方法の詳細については、Microsoft docs の [#if プリプロセッサ ディレクティブ](/dotnet/csharp/language-reference/preprocessor-directives#conditional-compilation)に関するページを参照してください。

以前のバージョンの Visual Studio をターゲットとするプロジェクトには、条件付きコンパイル シンボルが必要です。それを使用してコードをフォークし、さまざまな API を使用できます。 次の図に示すように、プロジェクトのプロパティ ページで条件付きコンパイル シンボルを設定できます。

![条件付きコンパイル シンボルを設定する](media/update-visual-studio-extension/conditional-compilation-symbols.png)

既定では入力したシンボルが 1 つの構成だけに適用される可能性があるため、必ず "*すべて*" の構成に対してコンパイル シンボルを設定します。

### <a name="c-techniques"></a>C\# の手法

それから、次のコードに示すように、そのシンボルをプリプロセッサ ディレクティブ (`#if`) として使用できます。 その後、コードをフォークして、異なる Visual Studio バージョン間で破壊的変更を処理できます。

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
#if Visual Studio 2019
    shell.LoadUILibrary(myGuid, myFlags, out uint ptrLib);
#else
    shell.LoadUILibrary(myGuid, myFlags, out IntPtr ptrLib);
#endif
```

場合によっては、`var` を使用することで、型に名前を付けることを避け、したがって `#if` 領域の必要性を回避できます。 上記のスニペットは、次のように記述することもできます。

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
    shell.LoadUILibrary(myGuid, myFlags, out var ptrLib);
```

`#if` 構文を使用する場合は、次に示すドキュメントの言語サービス コンテキスト ドロップダウンを使用して構文の強調表示を変更する方法と、言語サービスで提供される他のヘルプを使用して、この拡張機能と別のものについて 1 つのターゲットである Visual Studio バージョンに注目する方法があります。

![共有プロジェクトでの条件付きコンパイル](media/update-visual-studio-extension/conditional-compilation-if-region.png)

### <a name="xaml-sharing-techniques"></a>XAML での共有の手法

XAML には、プリプロセッサ シンボルに基づいてコンテンツをカスタマイズできるプリプロセッサはありません。 Visual Studio 2022 と以前のバージョンとの間でコンテンツが異なる必要がある 2 つの XAML ページをコピーしてメンテナンスすることが必要になる場合があります。

ただし、場合によっては、Visual Studio 2022 か以前のバージョンかにかかわらず個別のアセンブリに存在する型への参照は、アセンブリを参照している名前空間を削除することで、1 つの XAML ファイルで引き続き表現できる場合があります。

```diff
-xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
-Value="{DynamicResource {x:Static vsui:TreeViewColors.SelectedItemActiveBrushKey}}"
+Value="{DynamicResource TreeViewColors.SelectedItemActiveBrushKey}"
```

## <a name="test-your-extension"></a>拡張機能をテストする

Visual Studio 2022 をターゲットとする拡張機能をテストするには、Visual Studio 2022 Preview がインストールされている必要があります。
Visual Studio 2022 Preview よりも前のバージョンの Visual Studio で 64 ビットの拡張機能を実行することはできません。

Visual Studio 2022 Preview を使用して拡張機能をビルドし、Visual Studio 2022 と以前のバージョンのどちらをターゲットにしているかをテストできます。 Visual Studio 2022 から VSIX プロジェクトを起動すると、Visual Studio の実験インスタンスが起動します。

拡張機能でサポートする予定の Visual Studio バージョンごとにテストすることを強くお勧めします。

これで、[拡張機能を公開する](#publish-your-extension)準備ができました。

## <a name="publish-your-extension"></a>拡張機能の公開

順調です。ターゲットである Visual Studio 2022 を拡張機能に追加してテストしました。 これで、世界から賞賛される拡張機能を公開する準備ができました。

### <a name="visual-studio-marketplace"></a>Visual Studio Marketplace

拡張機能を [Visual Studio Marketplace](https://marketplace.visualstudio.com/) に公開することは、新しいユーザーに拡張機能を見つけてインストールしてもらう優れた方法です。 拡張機能のターゲットが Visual Studio 2022 だけか、以前の VS バージョンもターゲットとするかにかかわらず、Marketplace でサポートされます。

今後、Marketplace では、複数の VSIX を 1 つの Marketplace 登録情報にアップロードできるようになります。これにより、Visual Studio 2022 をターゲットにした VSIX と、Visual Studio 2022 より前の VSIX をアップロードできます。 VS 拡張機能マネージャーを使用すると、ユーザーはインストールした VS バージョンに対して適切な VSIX を自動的に取得します。

Visual Studio 2022 のプレビュー リリースについては、Marketplace において Marketplace 登録ごとに 1 つの VSIX ファイルのみがサポートされます。 Visual Studio 2022 がプレビュー段階にある間は、拡張機能のために Visual Studio 2022 のみの別個の Marketplace 登録を行うことをお勧めします。 そうすることで、以前のバージョンの Visual Studio のユーザーに影響を与えることなく、必要に応じて Visual Studio 2022 の拡張機能を反復できます。 また、拡張機能を "プレビュー" としてマークすることで、それがメインストリームの拡張機能よりも信頼性が低い可能性がある (信頼性の低い原因が Visual Studio 2022 であったとしても) という想定を設定できます。

### <a name="custom-installer"></a>カスタム インストーラー

拡張機能をインストールするための MSI または EXE をビルドする場合、および拡張機能 (の一部分) をインストールするための vsixinstaller.exe を生成する場合は、Visual Studio 2022 の VSIX インストーラーが更新されたことに注意してください。 開発者は、Visual Studio 2022 に拡張機能をインストールするために、Visual Studio 2022 に付属しているバージョンの VSIX インストーラーを使用する必要があります。 Visual Studio 2022 の VSIX インストーラーによって、同じコンピューター上に Visual Studio 2022 とサイド バイ サイドでインストールされている、以前のバージョンの Visual Studio をターゲットとする適用可能な拡張機能もインストールされます。

### <a name="network-share"></a>ネットワーク共有

LAN または他の方法で拡張機能を共有できます。 Visual Studio 2022 および Visual Studio 2022 以前をターゲットとする場合は、複数の VSIX を個別に共有し、ファイル名を指定 (または一意のフォルダーに配置) する必要があります。これは、インストールされている Visual Studio のバージョンに基づいてインストールする VSIX をユーザーが把握するのに役立ちます。

### <a name="other-considerations"></a>その他の考慮事項

#### <a name="dependencies"></a>依存関係

ご自身の VSIX で `<dependency>` 要素を使用して別の VSIX を依存関係として指定する場合、参照した各 VSIX は、ご自身の VSIX と同じターゲットおよび製品アーキテクチャにインストールされる必要があります。 依存する VSIX がターゲットの Visual Studio のインストールをサポートしていない場合、ご自身の VSIX は正しく実行されません。 依存する VSIX で、ご自身のものより多くのターゲットとアーキテクチャがサポートされていることは問題ありません (少ないのは不可)。 この制限は、依存関係を持つ VSIX の配置と配布のアプローチが、依存関係の配置と配布のアプローチを反映している必要があることを意味します。

## <a name="q--a"></a>Q & A

**Q**: データ (テンプレートなど) を提供するだけの拡張機能なので相互運用のための変更は必要ないのですが、Visual Studio 2022 も含む 1 つの拡張機能を作成できますか?

**A**: はい。  詳細については、「[実行されるコードを含まない拡張機能](#extensions-without-running-code)」を参照してください。

**Q**: NuGet の依存関係によって古い相互運用機能アセンブリが持ち込まれ、クラスのクラッシュを引き起こしています。

**A**: .csproj ファイルに次の行を追加して、アセンブリが重複しないようにします。

```xml
    <PackageReference Include="<Name of offending assembly>" ExcludeAssets="compile" PrivateAssets="all" />
```

これにより、パッケージ参照によって他の依存関係から古いバージョンのアセンブリがインポートされなくなります。

**Q**: ソース ファイルを共有プロジェクトに切り替た後、Visual Studio でコマンドとホットキーが機能していません。

**A**: イメージ オプティマイザー サンプルの[ステップ 2.4](samples.md#step-2---refactor-source-code-into-a-shared-project) には、VSCT ファイルをリンク項目として追加し、VSCT ファイルにコンパイルする方法が示されています。

## <a name="next-steps"></a>次のステップ

ステップごとのプロジェクトとコード変更へのリンクが記載された、[ImageOptimizer](samples.md) の操作手順の例に従ってください。
