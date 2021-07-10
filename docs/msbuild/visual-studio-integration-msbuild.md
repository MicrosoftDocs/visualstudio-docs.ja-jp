---
title: Visual Studio の統合 (MSBuild)
titleSuffix: ''
description: MSBuild 形式のプロジェクトがさまざまなツールによって作成され、ビルド プロセスがカスタマイズされている場合でも、Visual Studio でそれらをホストする方法について説明します。
ms.custom: seodec18, SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, reference resolution
- MSBuild, well-known target names
- MSBuild, hosting
- MSBuild, editing project files
- MSBuild, Visual Studio integration
- MSBuild, IntelliSense
- MSBuild, output groups
- MSBuild, in-process compilers
- MSBuild, design-time target execution
ms.assetid: 06cd6d7f-8dc1-4e49-8a72-cc9e331d7bca
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 63e78d935d515ccafda461a8f7af77623387940b
ms.sourcegitcommit: 674d3fafa7c9e0cb0d1338027ef419a49c028c36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2021
ms.locfileid: "112602155"
---
# <a name="visual-studio-integration-msbuild"></a>Visual Studio の統合 (MSBuild)

Visual Studio では、マネージド プロジェクトの読み込みとビルドを行うために MSBuild がホストされます。 MSBuild はプロジェクトに対応しているため、そのプロジェクトが他のツールで作成されていたり、ビルド処理がカスタマイズされていたりしても、MSBuild 形式のほとんどすべてのプロジェクトを Visual Studio で問題なく使用できます。

 この記事では、Visual Studio に読み込んでビルドするプロジェクトおよび *.targets* ファイルをカスタマイズする際に考慮する必要がある、Visual Studio による MSBuild のホストに固有な事項について説明します。 これらは、IntelliSense やデバッグなどの Visual Studio の機能をご自分のカスタム プロジェクトで動作させるのに役立ちます。

 C++ プロジェクトの詳細については、「[プロジェクト ファイル](/cpp/build/reference/project-files)」を参照してください。

## <a name="project-file-name-extensions"></a>プロジェクト ファイル名の拡張子

 *MSBuild.exe* は、 *.\*proj* のパターンに一致するすべてのプロジェクト ファイル拡張子を認識します。 ただし、Visual Studio によって認識されるのは、プロジェクトを読み込む言語固有のプロジェクト システムを決定する、これらのプロジェクト ファイル名拡張子のサブセットのみです。 Visual Studio には、言語に依存しない MSBuild ベースのプロジェクト システムは用意されていません。

 たとえば、C# のプロジェクト システムは *.csproj* ファイルを読み込みますが、Visual Studio では *.xxproj* ファイルを読み込むことができません。 任意の言語のソース ファイル用のプロジェクト ファイルには、Visual Studio に読み込む Visual Basic または C# プロジェクト ファイルと同じ拡張子を使用する必要があります。

## <a name="well-known-target-names"></a>既知のターゲット名

 Visual Studio の **[ビルド]** をクリックすると、プロジェクトの既定のターゲットが実行されます。 このターゲットも `Build`という名前になっていることがよくあります。 **[リビルド]** または **[消去]** を選択すると、プロジェクト内の同じ名前のターゲットが実行されます。 **[発行]** をクリックすると、プロジェクト内の `PublishOnly` という名前のターゲットが実行されます。

## <a name="configurations-and-platforms"></a>構成とプラットフォーム

 MSBuild プロジェクトの構成は、`Condition` 属性を含む `PropertyGroup` 要素内にグループ化されているプロパティによって表されます。 表示するプロジェクト構成およびプラットフォームのリストを作成するために、Visual Studio によってこれらの条件が確認されます。 このリストを正常に抽出するには、条件の形式が次のようになっている必要があります。

```xml
Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' "
Condition=" '$(Configuration)' == 'Release' " 
Condition=" '$(Something)|$(Configuration)|$(SomethingElse)' == 'xxx|Debug|yyy' "
```

 Visual Studio ではこの目的のために、`PropertyGroup`、`ItemGroup`、`Import`、プロパティ、およびアイテム要素の条件が確認されます。

## <a name="additional-build-actions"></a>その他のビルド アクション

 Visual Studio では、 **[ファイルのプロパティ]** ウィンドウの **[ビルド アクション]** プロパティを使って、プロジェクト内のファイルのアイテムの種類名を変更できます。 **Compile**、**EmbeddedResource**、**Content**、**None** の各項目の種類名は、プロジェクト内に既に存在する他の項目の種類名と共に、常にこのメニューに表示されます。 このメニューにカスタムの項目の種類名すべてが常に表示されるようにするには、 `AvailableItemName`という項目の種類に名前を追加します。 たとえば、プロジェクト ファイルに次の内容を追加すると、このファイルをインポートするすべてのプロジェクトの当該メニューに、カスタム型 **JScript** が追加されます。

```xml
<ItemGroup>
    <AvailableItemName Include="JScript"/>
</ItemGroup>
```

アイテムの種類 `AvailableItemName` にアイテムの種類の名前を付けると、その種類のアイテムが **ソリューション エクスプローラー** に表示されます。

> [!NOTE]
> 一部のアイテムの種類名は Visual Studio 特有のものですが、このドロップダウンには表示されません。

## <a name="in-process-compilers"></a>インプロセス コンパイラ

 可能な場合、Visual Studio では、パフォーマンス向上のためにインプロセス バージョンの Visual Basic コンパイラが使用されます。 (C# には適用されません。)これが正しく機能するためには、次の条件が満たされている必要があります。

- プロジェクトのターゲットに、Visual Basic プロジェクト用の `Vbc` という名前のタスクが存在すること。

- このタスクの `UseHostCompilerIfAvailable` パラメーターが true に設定されていること。

## <a name="design-time-intellisense"></a>デザイン時における IntelliSense のサポート

 ビルドによって出力アセンブリが生成される前に、Visual Studio で IntelliSense がサポートされるようにするには、次の条件が満たされている必要があります。

- `Compile`という名前のターゲットが存在すること。

- `Compile` ターゲットまたはその依存関係のいずれかによって、 `Csc` や `Vbc`などの、プロジェクトのコンパイラ タスクが呼び出されること。

- `Compile` ターゲットまたはその依存関係のいずれかによって、IntelliSense に必要なすべてのパラメーター (特にすべての参照) をコンパイラが受け取ること。

- 「[インプロセス コンパイラ](#in-process-compilers)」のセクションに示した条件が満たされていること。

## <a name="build-solutions"></a>ソリューションをビルドする

 Visual Studio 内では、ソリューション ファイルおよびプロジェクトのビルドの順序は Visual Studio 自体によって制御されます。 コマンド ラインで *msbuild.exe* を使用してソリューションをビルドすると、MSBuild によってソリューション ファイルが解析され、プロジェクトのビルドの順序が決定されます。 どちらの場合も、プロジェクトは依存関係の順序で個別にビルドされ、プロジェクト間参照は走査されません。 逆に、*msbuild.exe* を使用して個々のプロジェクトをビルドする場合は、プロジェクト間参照が走査されます。

 Visual Studio の内部でビルドする場合は、`$(BuildingInsideVisualStudio)` プロパティを `true` に設定します。 これをプロジェクトまたは *.targets* ファイル内で使用することにより、ビルドの動作を変更できます。

## <a name="display-properties-and-items"></a>プロパティと項目の表示

 Visual Studio では、特定のプロパティの名前と値が認識されます。 たとえば、プロジェクト内で次のプロパティを使用すると、 **プロジェクト デザイナー** の **[アプリケーションの種類]** ボックスに **Windows アプリケーション** が表示されます。

```xml
<OutputType>WinExe</OutputType>
```

 プロパティ値は、 **プロジェクト デザイナー** で編集してプロジェクト ファイルに保存できます。 このようなプロパティを手動で編集することによって無効な値が指定された場合、プロジェクトを読み込む際に Visual Studio によって警告メッセージが表示され、無効な値が既定値に置き換えられます。

 Visual Studio では、一部のプロパティの既定値が認識されています。 これらのプロパティは、既定値以外の値を持つ場合だけプロジェクト ファイルに保存されます。

 恣意的な名前のプロパティは Visual Studio には表示されません。 Visual Studio で恣意的なプロパティを変更するには、XML エディターでプロジェクト ファイルを開き、それらを手動で編集する必要があります。 詳細については、このトピックで後述する「[Visual Studio でプロジェクト ファイルを編集する](#edit-project-files-in-visual-studio)」を参照してください。

 任意の項目の種類名を使用してプロジェクト内で定義された項目は、既定では、**ソリューション エクスプローラー** のプロジェクト ノードの下に表示されます。 項目が表示されないようにするには、 `Visible` メタデータを `false`に設定します。 たとえば、次の項目はビルド処理に参加しますが、**ソリューション エクスプローラー** には表示されません。

```xml
<ItemGroup>
    <IntermediateFile Include="cache.temp">
        <Visible>false</Visible>
    </IntermediateFile>
</ItemGroup>
```

> [!NOTE]
> C++ プロジェクトの場合、`Visible` のメタデータは **ソリューション エクスプローラー** で無視されます。 `Visible` が false に設定されている場合でも、項目は常に表示されます。

 プロジェクトにインポートしたファイルで宣言されている項目は、既定では表示されません。 ビルド処理中に作成された項目が **ソリューション エクスプローラー** に表示されることは決してありません。

## <a name="conditions-on-items-and-properties"></a>項目とプロパティの条件

 ビルド時には、すべての条件が完全に遵守されます。

 表示するプロパティ値を決定する際、Visual Studio によって構成に依存すると見なされたプロパティは、構成に依存しないと見なされたプロパティとは異なる方法で評価されます。 構成に依存すると見なされたプロパティの場合、Visual Studio によって `Configuration` プロパティと `Platform` プロパティが適切に設定され、MSBuild に対してプロジェクトを再評価するように指示されます。 構成に依存しないと見なされるプロパティの場合、条件の評価方法は不確定です。

 項目の条件式は、その項目を **ソリューション エクスプローラー** に表示するかどうかを決めるという目的では常に無視されます。

## <a name="debugging"></a>デバッグ

 出力アセンブリを見つけて起動し、デバッガーをアタッチするには、Visual Studio で `OutputPath`、`AssemblyName`、および `OutputType` プロパティが正しく定義されている必要があります。 ビルド処理においてコンパイラが *.pdb* ファイルを生成しない場合、デバッガーはアタッチされません。

## <a name="design-time-target-execution"></a>デザイン時におけるターゲットの実行

 Visual Studio では、プロジェクトが読み込まれると、特定の名前を持つターゲットの実行が試みられます。 このようなターゲットとしては、`Compile`、`ResolveAssemblyReferences`、`ResolveCOMReferences`、`GetFrameworkPaths`、`CopyRunEnvironmentFiles` などがあります。 IntelliSense を使用できるようにコンパイラを初期化し、デバッガーを初期化し、ソリューション エクスプローラーに表示される参照を解決するために、Visual Studio によってこれらのターゲットが実行されます。 これらのターゲットが存在しない場合、プロジェクトは正常に読み込まれてビルドされますが、Visual Studio のデザイン時のエクスペリエンスは完全には機能しません。

## <a name="edit-project-files-in-visual-studio"></a>Visual Studio でプロジェクト ファイルを編集する

 MSBuild プロジェクトを直接編集するには、Visual Studio の XML エディターでプロジェクト ファイルを開きます。

#### <a name="to-unload-and-edit-a-project-file-in-visual-studio"></a>Visual Studio でプロジェクト ファイルをアンロードして編集するには

1. **ソリューション エクスプローラー** で、プロジェクトのショートカット メニューを開き、 **[プロジェクトのアンロード]** をクリックします。

     プロジェクトに **(利用不可)** のマークが付きます。

2. **ソリューション エクスプローラー** で、利用不可のプロジェクトのショートカット メニューを開き、 **[\<Project File> の編集]** を選択します。

     Visual Studio XML エディターでプロジェクト ファイルが開きます。

3. プロジェクト ファイルを編集し、保存して閉じます。

4. **ソリューション エクスプローラー** で、利用不可のプロジェクトのショートカット メニューを開き、 **[プロジェクトの再読み込み]** をクリックします。

## <a name="intellisense-and-validation"></a>IntelliSense と検証

 XML エディターを使用してプロジェクト ファイルを編集する際、MSBuild のスキーマ ファイルによって IntelliSense と検証が実行されます。 これらは、 *\<Visual Studio installation directory>\Xml\Schemas\1033\MSBuild* にあるスキーマ キャッシュにインストールされます。

 MSBuild の中心となる型は *Microsoft.Build.Core.xsd* で定義され、Visual Studio によって使用される共通の型は *Microsoft.Build.CommonTypes.xsd* で定義されます。 カスタムの項目の種類名、プロパティ、およびタスク用に IntelliSense と検証を使用できるようにスキーマをカスタマイズするには、*Microsoft.Build.xsd* を編集するか、CommonTypes スキーマまたは Core スキーマを含む独自のスキーマを作成します。 独自のスキーマを作成する場合は、 **[プロパティ]** ウィンドウを使用してこのスキーマを見つけるように XML エディターに指示する必要があります。

## <a name="edit-loaded-project-files"></a>読み込んだプロジェクト ファイルの編集

 Visual Studio では、プロジェクト ファイルやプロジェクト ファイルによってインポートされたファイルの内容がキャッシュされます。 読み込んだプロジェクト ファイルを編集すると、プロジェクトを再読み込みして変更を有効にするように求めるメッセージが Visual Studio によって自動的に表示されます。 ただし、読み込んだプロジェクトによってインポートされたファイルを編集した場合は、再読み込みを求めるメッセージが表示されないため、手動でプロジェクトのアンロードと再読み込みを行い、変更内容を有効にする必要があります。

## <a name="output-groups"></a>出力グループ

 *Microsoft.Common.targets* で定義したいくつかのターゲットの名前は、最後の部分が `OutputGroups` または `OutputGroupDependencies` となります。 Visual Studio ではこれらのターゲットが呼び出され、特定のプロジェクト出力のリストが取得されます。 たとえば、`SatelliteDllsProjectOutputGroup` ターゲットを呼び出すと、ビルドが作成したすべてのサテライト アセンブリのリストが作成されます。 これらの出力グループは、発行、配置、およびプロジェクト間参照などの機能によって使用されます。 これらが定義されていなくても、プロジェクトは Visual Studio に読み込まれてビルドされますが、一部の機能が正常に動作しない場合があります。

## <a name="reference-resolution"></a>参照の解決

 参照の解決とは、プロジェクト ファイルに格納されている参照項目を使用して、実際のアセンブリを検索する処理をいいます。 Visual Studio では、 **[プロパティ]** ウィンドウに各参照の詳細なプロパティを表示するために、参照の解決をトリガーする必要があります。 次の一覧では、3 種類の参照とその解決方法について説明します。

- アセンブリ参照

   プロジェクト システムは、 `ResolveAssemblyReferences`という既知の名前を持つターゲットを呼び出します。 このターゲットは、 `ReferencePath`という項目の種類名を持つ項目を生成します。 これらの項目のそれぞれが、参照への完全パスを含む項目規定 (項目の `Include` 属性の値) を持ちます。 これらの項目には、以下の新しいメタデータに加え、入力項目のすべてのメタデータも渡されます。

  - アセンブリを出力フォルダーにコピーするかどうかを示す`CopyLocal`。true または false に設定されます。

  - 参照の元の項目規定を格納している`OriginalItemSpec`。

  - .NET Framework ディレクトリから解決された場合に "{TargetFrameworkDirectory}" に設定される `ResolvedFrom`。

- COM 参照

   プロジェクト システムは、 `ResolveCOMReferences`という既知の名前を持つターゲットを呼び出します。 このターゲットは、 `ComReferenceWrappers`という項目の種類名を持つ項目を生成します。 これらの項目のそれぞれが、COM 参照のための相互運用機能アセンブリへの完全パスを含む項目規定を持ちます。 これらの項目には、アセンブリを出力フォルダーにコピーするかどうかを示す `CopyLocal` という名前の新しいメタデータ (true または false に設定) に加え、入力項目のすべてのメタデータも渡されます。

- ネイティブ参照

   プロジェクト システムは、 `ResolveNativeReferences`という既知の名前を持つターゲットを呼び出します。 このターゲットは、 `NativeReferenceFile`という項目の種類名を持つ項目を生成します。 これらの項目には、参照の元の項目規定を格納する `OriginalItemSpec`という名前の新しいメタデータに加え、入力項目のすべてのメタデータも渡されます。

## <a name="performance-shortcuts"></a>パフォーマンスに関するヒント

 Visual Studio IDE を使用して (F5 キーを選択するか、メニュー バーの **[デバッグ]**  >  **[デバッグの開始]** を選択するかのいずれかを行うことで) デバッグを開始する場合、またはプロジェクト (例: **[ビルド]**  >  **[ソリューションのビルド]** ) をビルドする場合、パフォーマンスを向上させるために、ビルド処理で高速更新チェックを使用します。 カスタマイズされたビルドで、順次ビルドするファイルを作成した場合、高速更新チェックでは変更されたファイルが正しく識別されません。 徹底した更新プログラムのチェックを必要とするプロジェクトでは、 `DISABLEFASTUPTODATECHECK=1`環境変数を設定することで高速チェックを無効にできます。 また、プロジェクトまたはプロジェクトでインポートしたファイルで、MSBuild プロパティとしてこれを設定することもできます。

 Visual Studio の通常のビルドでは、高速更新チェックは適用されず、コマンド プロンプトでビルドを開始する場合と同じ方法でプロジェクトがビルドされます。

## <a name="see-also"></a>関連項目

- [方法: Visual Studio ビルド処理を拡張する](../msbuild/how-to-extend-the-visual-studio-build-process.md)
- [IDE 内からのビルドの開始](../msbuild/starting-a-build-from-within-the-ide.md)
- [.NET Framework の拡張機能の登録](../msbuild/registering-extensions-of-the-dotnet-framework.md)
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [Item 要素 (MSBuild)](../msbuild/item-element-msbuild.md)
- [Property 要素 (MSBuild)](../msbuild/property-element-msbuild.md)
- [Target 要素 (MSBuild)](../msbuild/target-element-msbuild.md)
- [Csc タスク](../msbuild/csc-task.md)
- [Vbc タスク](../msbuild/vbc-task.md)
