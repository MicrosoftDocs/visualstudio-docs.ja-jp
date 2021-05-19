---
title: MSBuild | Microsoft Docs
description: Microsoft Build Engine (MSBuild) プラットフォームによって、ビルドを制御するための XML スキーマがプロジェクト ファイルに提供される方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, about MSBuild
- MSBuild, overview
ms.assetid: e39f13f7-1e1d-4435-95ca-0c222bca071c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 372fc5c81b963cbb8e46cab689713e476fcfff7d
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848280"
---
# <a name="msbuild"></a>MSBuild

Microsoft Build Engine は、アプリケーションをビルドするためのプラットフォームです。 MSBuild とも呼ばれるこのエンジンには、ビルド プラットフォームでソフトウェアを処理およびビルドする方法を制御する、プロジェクト ファイル用の XML スキーマが用意されています。 Visual Studio は MSBuild を使用しますが、MSBuild は Visual Studio に依存しません。 プロジェクト ファイルまたはソリューション ファイルに対して *msbuild.exe* を実行すると、Visual Studio がインストールされていない環境で、製品の統合とビルドを実行できます。

 Visual Studio は、マネージド プロジェクトの読み込みとビルドを行う MSBuild をホストしています。 Visual Studio のプロジェクト ファイル ( *.csproj*、*vbproj*、*vcxproj* など) には、IDE を使用してプロジェクトをビルドするときに実行される MSBuild XML コードが含まれています。 Visual Studio プロジェクトには、一般的な開発作業を行う必要なすべての設定とビルド プロセスがインポートされますが、Visual Studio 内のエディターや任意の XML エディターを使用してそれらを拡張または変更することもできます。

 C++ に対する MSBuild の詳細については、「[MSBuild (C++)](/cpp/build/msbuild-visual-cpp)」をご覧ください。

 次の例では、Visual Studio IDE ではなくコマンド ラインから MSBuild を呼び出してビルドを実行する状況について説明します。

- Visual Studio 2013 がインストールされていません。 ([Visual Studio なしの MSBuild をダウンロードする](https://visualstudio.microsoft.com/downloads/?q=build+tools))。

- MSBuild の 64 ビット バージョンを使用することを希望しています。 通常は MSBuild のこのバージョンは不要ですが、このバージョンを使用すると、MSBuild はより多くのメモリにアクセスできます。

- 複数のプロセスでビルドを実行することを希望しています。 ただし、C++ および C# で記述したプロジェクトに関しては、同じ結果を達成するために IDE を使用することもできます。

- ビルド システムを変更することを希望しています。 たとえば、次の操作を有効にすることを希望する場合があります。

  - コンパイラに渡す前に、ファイルを前処理します。

  - ビルド出力を別の場所にコピーします。

  - ビルド出力から圧縮ファイルを作成します。

  - 後処理手順を実行します。 たとえば、1 つのアセンブリに対して、異なる複数のバージョンをスタンプとして割り当てることがあります。

Visual Studio IDE でコードを作成し、MSBuild を使用してビルドを実行することもできます。 別の方法として、開発用コンピューターの IDE でコードをビルドすることもできますが、コマンド ラインから MSBuild を実行して、複数の開発者から取得して統合したコードをビルドすることもできます。 また、MSBuild を使用する [.NET Core コマンドライン インターフェイス (CLI)](/dotnet/core/tools/) を使用して、.NET Core プロジェクトをビルドすることもできます。

> [!NOTE]
> Azure Pipelines を使用して、アプリケーションを自動的にコンパイル、テスト、および配置することができます。 開発者がコードをチェックインしたとき (たとえば、継続的インテグレーションの手法の一環として)、またはスケジュールに従って (たとえば、夜間のビルド確認テストの一部として)、ビルド システムがビルドを自動的に実行ですることもできます。 Azure Pipelines では MSBuild を使用してコードをコンパイルします。 詳細については、「[Azure Pipelines](/azure/devops/pipelines/index?view=vsts&preserve-view=true)」を参照してください。

この記事では、MSBuild の概要について説明します。 入門チュートリアルについては、[チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)に関するページを参照してください。

## <a name="use-msbuild-at-a-command-prompt"></a>コマンド プロンプトでの MSBuild の使用

 MSBuild をコマンド プロンプトで実行するには、適切なコマンド ライン オプションと共に、プロジェクト ファイルを *MSBuild.exe* に渡します。 コマンド ライン オプションでは、プロパティを設定したり、特定のターゲットを実行したりできるほか、ビルド処理を制御するその他のオプションも設定できます。 たとえば、`Configuration` プロパティを `Debug` に設定して *MyProj.proj* ファイルをビルドするには、次のコマンド ライン構文を使用します。

```cmd
MSBuild.exe MyProj.proj -property:Configuration=Debug
```

 MSBuild のコマンド ライン オプションの詳細については、[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)をご覧ください。

> [!IMPORTANT]
> プロジェクトをダウンロードする前に、コードが信頼できるものかどうかを確認してください。

## <a name="project-file"></a>プロジェクト ファイル

 MSBuild では、簡単で拡張性がある XML ベースのプロジェクト ファイル形式が使用されています。 MSBuild のプロジェクト ファイル形式では、ビルドする項目のほか、それらをさまざまなオペレーティング システムや構成用にビルドする方法も、開発者が指定できます。 また、異なるファイルに適用できるビルド規則を記述しておき、製品を構成するさまざまなプロジェクトで再利用することにより、一貫したビルド作業を行うことができます。

 以下のセクションでは、MSBuild プロジェクト ファイル形式のいくつかの基本要素について説明します。 基本的なプロジェクト ファイルを作成する方法のチュートリアルについては、[チュートリアル:MSBuild プロジェクト ファイルのゼロからの作成](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)に関するページを参照してください。

### <a name="properties"></a><a name="BKMK_Properties"></a> プロパティ

 プロパティはビルドを設定するためのキーと値のペアです。 プロパティを宣言するには、そのプロパティの名前を持つ要素を [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) 要素の子として作成します。 たとえば、次の コードでは、`BuildDir` という名前のプロパティを作成し、`Build` を値として設定しています。

```xml
<PropertyGroup>
    <BuildDir>Build</BuildDir>
</PropertyGroup>
```

 要素内に `Condition` 属性を配置して、プロパティを条件付きで定義することもできます。 条件が `true` と評価されないと、条件付き要素の内容は無視されます。 次の例では、`Configuration` 要素がまだ定義されていない場合に、この要素を定義します。

```xml
<Configuration  Condition=" '$(Configuration)' == '' ">Debug</Configuration>
```

 プロジェクト ファイルでプロパティを参照するには、$(\<PropertyName>) という構文を使用します。 たとえば、前の例に示したプロパティを参照するには、`$(BuildDir)` および `$(Configuration)` と記述します。

 プロパティの詳細については、「[MSBuild プロパティ](../msbuild/msbuild-properties.md)」をご覧ください。

### <a name="items"></a><a name="BKMK_Items"></a> 項目

 項目はビルド システムへの入力であり、通常はファイルを表します。 項目はユーザー定義の項目名に基づいて項目の種類にグループ化されます。 これらの項目の種類は、タスクのパラメーターとして使用できます。タスクでは、個々の項目を使用してビルド処理の各ステップを実行します。

 項目は、その項目の種類名を名前に持つ要素を、[ItemGroup](../msbuild/itemgroup-element-msbuild.md) 要素の子として作成することにより、プロジェクト ファイルで宣言します。 たとえば、次のコードでは、`Compile` という名前の項目の種類を作成し、2 つのファイルを含めています。

```xml
<ItemGroup>
    <Compile Include = "file1.cs"/>
    <Compile Include = "file2.cs"/>
</ItemGroup>
```

 プロジェクト ファイルで項目の種類を参照するには、@(\<ItemType>) という構文を使用します。 たとえば、この例に示した項目の種類を参照するには、`@(Compile)` と記述します。

 MSBuild では、要素名および属性名では大文字と小文字が区別されますが、 プロパティ名、項目名、メタデータ名では、大文字と小文字は区別されません。 次の例では、`Compile`、`comPile`、または大文字小文字が異なるさらに別の項目の種類のいずれかを作成し、項目の種類に対して "one.cs;two.cs" という値を割り当てます。

```xml
<ItemGroup>
  <Compile Include="one.cs" />
  <Compile Include="two.cs" />
</ItemGroup>
```

 項目はワイルドカード文字を使って宣言できるほか、メタデータを追加することで、より高度なビルド作業を行うことができます。 項目の詳細については、「[項目](../msbuild/msbuild-items.md)」をご覧ください。

### <a name="tasks"></a><a name="BKMK_Tasks"></a> タスク

 タスクとは、MSBuild プロジェクトでビルド処理を実行するために使用される実行可能コードの単位です。 たとえば、タスクでは入力ファイルをコンパイルしたり、外部ツールを実行したりします。 タスクは再利用が可能で、複数の開発者が複数のプロジェクトで共有できます。

 タスクの実行ロジックはマネージド コードで記述され、[UsingTask](../msbuild/usingtask-element-msbuild.md) 要素を使用して MSBuild にマップされます。 <xref:Microsoft.Build.Framework.ITask> インターフェイスを実装するマネージド型を記述することにより、独自のタスクを作成できます。 タスクを記述する方法の詳細については、「[タスクの作成](../msbuild/task-writing.md)」をご覧ください。

 MSBuild には、ご自分の要件に合わせて変更できる一般的なタスクが含まれています。 例は、ファイルをコピーする [Copy](../msbuild/copy-task.md)、ディレクトリを作成する [MakeDir](../msbuild/makedir-task.md)、Visual C# ソース コード ファイルをコンパイルする [Csc](../msbuild/csc-task.md) などです。 使用可能なタスクと使用法については、「[タスク リファレンス](../msbuild/msbuild-task-reference.md)」をご覧ください。

 MSBuild プロジェクト ファイルでタスクを実行するには、そのタスクの名前を持つ要素を、[Target](../msbuild/target-element-msbuild.md) 要素の子として作成します。 一般に、タスクは、要素の属性として渡されるパラメーターを受け取ります。 MSBuild のプロパティと項目の両方をパラメーターとして使用できます。 たとえば、次のコードでは、[MakeDir](../msbuild/makedir-task.md) タスクを呼び出し、先ほどの例で宣言した `BuildDir` プロパティの値を渡しています。

```xml
<Target Name="MakeBuildDirectory">
    <MakeDir  Directories="$(BuildDir)" />
</Target>
```

 タスクの詳細については、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。

### <a name="targets"></a><a name="BKMK_Targets"></a> ターゲット

 ターゲットは、タスクを特定の順序でグループ化し、プロジェクト ファイルの各セクションを、ビルド プロセスのエントリ ポイントとして公開する役割を果たします。 読みやすさや拡張性を高める目的で、複数のターゲットを論理的なセクションとしてグループ化することもできます。 ビルド ステップを複数のターゲットに分割することにより、他のターゲットから、一部のビルド処理だけを呼び出すことができ、そのコード セクションをすべてのターゲットに逐一コピーする手間をなくすことができます。 たとえば、ビルド処理の複数のエントリ ポイントで、参照をビルドする必要がある場合、参照をビルドするターゲットを作成しておけば、必要なすべてのエントリ ポイントからそのターゲットを実行できます。

 ターゲットは、プロジェクト ファイル内で、[Target](../msbuild/target-element-msbuild.md) 要素を使用して宣言します。 たとえば、次のコードでは、先ほどの例で宣言した項目のリストをパラメーターに指定して [Csc](../msbuild/csc-task.md) タスクを呼び出す、`Compile` という名前のターゲットを作成しています。

```xml
<Target Name="Compile">
    <Csc Sources="@(Compile)" />
</Target>
```

 ターゲットを使用して相互の関係を定義し、依存関係の分析を実行するなど、より高度なシナリオにも対応しています。これにより、ターゲットが最新のものである場合に、ビルド処理からセクション全体をスキップするようなことが可能となります。 ターゲットの詳細については、「[MSBuild ターゲット](../msbuild/msbuild-targets.md)」をご覧ください。

## <a name="build-logs"></a>ビルド ログ

 コンソールまたは別の出力デバイスにビルド エラー、警告、およびメッセージを記録できます。 詳細については、「[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)」と「[MSBuild でのログ](../msbuild/logging-in-msbuild.md)」をご覧ください。

## <a name="use-msbuild-in-visual-studio"></a>Visual Studio で MSBuild を使用する

 Visual Studio では、マネージド プロジェクトに関するビルド情報を保存するために、MSBuild プロジェクト ファイル形式が使用されます。 Visual Studio インターフェイスを使用してプロジェクト設定に追加や変更を加えると、プロジェクトごとに生成される *.\*proj* ファイルにその内容が反映されます。 Visual Studio では、MSBuild のホスト インスタンスを使用して、マネージド プロジェクトがビルドされます。 つまり、マネージド プロジェクトは、Visual Studio でも、コマンド プロンプトでも (Visual Studio がインストールされていない場合でも) ビルドすることができ、結果は同じになります。

 Visual Studio で MSBuild を使用する方法のチュートリアルについては、[チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)に関するページを参照してください。

## <a name="multitargeting"></a><a name="BKMK_Multitargeting"></a> マルチ ターゲット

 Visual Studio を使用すると、いくつかのバージョンの .NET Framework のうち、任意のバージョンで動作するようにアプリケーションをコンパイルできます。 たとえば、あるアプリケーションを 32 ビット プラットフォーム上の .NET Framework 2.0 で動作するようにコンパイルしたり、これと同じアプリケーションを 64 ビット プラットフォーム上の .NET Framework 4.5 で動作するようにコンパイルしたりできます。 複数のフレームワークに対してコンパイルする機能をマルチ ターゲットといいます。

 マルチ ターゲットには、次のような利点があります。

- バージョン 2.0、3.0、3.5 などの以前のバージョンの .NET Framework を対象とするアプリケーションを開発できます。

- Silverlight など、.NET Framework 以外のフレームワークを対象にできます。

- ターゲット フレームワークの定義済みのサブセットである *フレームワーク プロファイル* を対象にできます。

- 現在のバージョンの .NET Framework 用サービス パックがリリースされた場合、そのバージョンを対象にできます。

- 複数バージョン対応により、アプリケーションが、対象となるフレームワークやプラットフォームのみで利用できる機能を使うことができます。

詳細については、[MSBuild のマルチ ターゲット](../msbuild/msbuild-multitargeting-overview.md)に関する記事をご覧ください。

## <a name="see-also"></a>関連項目

| Title | 説明 |
| - | - |
| [チュートリアル: MSBuild プロジェクト ファイルのゼロからの作成](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md) | テキスト エディターのみを使用して、基本的なプロジェクト ファイルをインクリメント方式で作成する方法について説明します。 |
| [チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md) | MSBuild のビルド ブロックについて説明し、Visual Studio IDE を閉じずに MSBuild プロジェクトを記述、操作、およびデバッグする方法について説明します。 |
| [MSBuild の概念](../msbuild/msbuild-concepts.md) | MSBuild の 4 つのビルド ブロックであるプロパティ、項目、ターゲット、およびタスクについて説明します。 |
| [項目](../msbuild/msbuild-items.md) | MSBuild ファイル形式の一般的な概念と、各構成要素の組み合わせ方について説明します。 |
| [MSBuild プロパティ](../msbuild/msbuild-properties.md) | プロパティとプロパティ コレクションについて説明します。 プロパティはビルドを設定するためのキーと値のペアです。 |
| [ターゲット](../msbuild/msbuild-targets.md) | タスクを特定の順序でグループ化し、コマンド ラインからビルド処理のセクションを呼び出すことができるようにする方法について説明します。 |
| [タスク](../msbuild/msbuild-tasks.md) | 分割不可能なビルド操作を実行するために MSBuild で使用される、実行可能コードの単位を作成する方法について説明します。 |
| [条件](../msbuild/msbuild-conditions.md) | MSBuild の要素で `Condition` 属性を使用する方法について説明します。 |
| [詳細な概念](../msbuild/msbuild-advanced-concepts.md) | バッチ処理、変換の実行、複数バージョン対応など、高度な利用法を紹介します。 |
| [MSBuild でのログ](../msbuild/logging-in-msbuild.md) | ビルド イベント、メッセージ、およびエラーを記録する方法について説明します。 |
| [MSBuild によってプロジェクトがビルドされる方法](build-process-overview.md) | MSBuild 内で使用される内部ビルド プロセスについて説明します |
| [その他のリソース](https://social.msdn.microsoft.com/forums/vstudio/home?forum=msbuild) | MSBuild に関する詳細な情報を提供するコミュニティやサポートのリソースを紹介します。 |

## <a name="reference"></a>関連項目

- [MSBuild リファレンス](../msbuild/msbuild-reference.md)\
 リファレンス情報を示すトピックへのリンクを提供します。

- [用語集](msbuild-glossary.md)\
 MSBuild で共通に使用される用語を定義します。
