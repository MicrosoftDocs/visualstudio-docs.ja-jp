---
title: Live Unit Testing
description: サポートされているフレームワークや Live Unit Testing の構成方法など、アプリケーション開発時の Live Unit Testing について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/07/2020
ms.topic: how-to
helpviewer_keywords:
- Live Unit Testing
author: mikejo5000
ms.author: mikejo
ms.workload:
- dotnet
ms.openlocfilehash: b9b78771c36dce26744ba74af63922cf1efa48e2
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798623"
---
# <a name="how-to-configure-and-use-live-unit-testing"></a>Live Unit Testing を構成して使用する方法

アプリケーションの開発中、Live Unit Testing では、影響を受けた単体テストがバックグラウンドで自動的に実行されて、結果とコード カバレッジがリアルタイムに表示されます。 コードを変更すると、Live Unit Testing は、既存のテストへの変更の影響と、新しいコードが 1 つ以上の既存のテストによってカバーされているかどうかに関するフィードバックを提供します。 それにより、バグの修正や新機能の追加を行うと、単体テストを作成する必要があることが示されます。

> [!NOTE]
> Live Unit Testing は、Visual Studio の Enterprise エディションで、.NET Core または .NET Framework を対象とする C# および Visual Basic プロジェクトに使用することができます。

テストで Live Unit Testing を使用すると、テストの状態に関するデータが保持されます。 保持されたデータを使用することにより、Live Unit Testing では、コード変更に対応して動的にテストを実行しながら、優れたパフォーマンスが提供されます。

## <a name="supported-test-frameworks"></a>サポートされるテスト フレームワーク

Live Unit Testing は、次の表に示されている 3 つの一般的な単体テスト フレームワークで動作します。 アダプターやフレームワークのサポートされる最小バージョンも示されています。 単体テスト フレームワークはすべて NuGet.org から入手できます。

|テスト フレームワーク  |Visual Studio アダプターの最小バージョン  |フレームワークの最小バージョン  |
|---------|---------|---------|
|xUnit.net |xunit.runner.visualstudio バージョン 2.2.0-beta3-build1187 |xunit 1.9.2 |
|NUnit |NUnit3TestAdapter バージョン 3.5.1 |NUnit バージョン 3.5.0 |
|MSTest |MSTest.TestAdapter 1.1.4-preview |MSTest.TestFramework 1.0.5-preview |

古い MSTest に基づくテスト プロジェクトで Microsoft.VisualStudio.QualityTools.UnitTestFramework が参照されていて、新しい MSTest NuGet パッケージに移行したくない場合は、Visual Studio 2019 または Visual Studio 2017 にアップグレードしてください。

場合によっては、Live Unit Testing を動作させるため、プロジェクトによって参照されている NuGet パッケージの明示的な復元が必要になります。 そのためには、ソリューションの明示的なビルドを行うか (Visual Studio の最上位メニューから **[ビルド]**  >  **[ソリューションのリビルド]** の順に選択)、またはソリューションのパッケージを復元します (ソリューションを右クリックして **[NuGet パッケージの復元]** を選択)。

## <a name="configure"></a>構成

Live Unit Testing を構成するには、Visual Studio の最上位メニュー バーから **[ツール]**  >  **[オプション]** の順に選択し、 **[オプション]** ダイアログの左側のウィンドウで **[Live Unit Testing]** を選択します。

> [!TIP]
> Live Unit Testing を有効にすると (次のセクション「[開始、一時停止、停止](#start-pause-and-stop)」を参照)、 **[テスト]**  >  **[Live Unit Testing]**  >  **[オプション]** を選択して **[オプション]** ダイアログを開くこともできます。

次の図では、ダイアログで使用できる Live Unit Testing の構成オプションを示します。

![Live Unit Testing の構成オプション](./media/lut-options.png)

次のオプションを構成できます。

- ソリューションをビルドしてデバッグするときに Live Unit Testing を一時停止するかどうか。

- システムのバッテリ電源が指定したしきい値を下回ったときに Live Unit Testing を一時停止するかどうか。

- ソリューションを開いたら Live Unit Testing を自動的に実行するかどうか。

- デバッグ シンボルと XML ドキュメントのコメント生成を有効にするかどうか。

- 保持されたデータを格納するディレクトリ。

- 保持されたデータをすべて削除できるようにする。 これは、Live Unit Testing で予測不能なまたは予期しない動作が発生している場合に便利です。この状態は、保持されたデータが破損していることを表しています。

- テスト ケースがタイムアウトするまでの時間。既定値は 30 秒です。

- Live Unit Testing が作成するテスト プロセスの最大数。

- Live Unit Testing のプロセスが使用できるメモリの最大容量。

- Live Unit Testing の **[出力]** ウィンドウに書き込まれる情報のレベル。

   オプションは、ログなし ( **[なし]** )、エラー メッセージのみ ( **[エラー]** )、エラーと情報メッセージ ( **[情報]** 、既定値)、またはすべての詳細 ( **[詳細]** ) です。

   `VS_UTE_DIAGNOSTICS` という名前のユーザー レベル環境変数に値 "1" を設定してから Visual Studio を再起動することにより、Live Unit Testing の **[出力]** ウィンドウに詳細な出力を表示することもできます。

   Live Unit Testing からファイルに詳細な MSBuild ログ メッセージをキャプチャするには、`LiveUnitTesting_BuildLog` ユーザー レベル環境変数を、ログを格納するファイルの名前に設定します。

## <a name="start-pause-and-stop"></a>開始、一時停止、停止

Live Unit Testing を有効にするには、Visual Studio の最上位メニューから **[テスト]**  >  **[Live Unit Testing]**  >  **[開始]** の順に選択します。 Live Unit Testing を有効にすると、 **[Live Unit Testing]** メニューで使用可能なオプションが、 **[開始]** の 1 項目から、 **[一時停止]** と **[停止]** に変わります。

- **[一時停止]** では、Live Unit Testing が一時的に中断されます。

  Live Unit Testing を一時停止すると、カバレッジの視覚化はエディターに表示されませんが、収集されたすべてのデータは保持されます。 Live Unit Testing を再開するには、Live Unit Testing メニューから **[続行]** を選びます。 Live Unit Testing で、一時停止中に行われたすべての編集を取得するために必要な作業が実行されて、グリフが適切に更新されます。

- **[停止]** では、Live Unit Testing が完全に停止されます。 Live Unit Testing は収集したすべてのデータを破棄します。

> [!NOTE]
> 単体テスト プロジェクトが含まれていないソリューションで Live Unit Testing を開始する場合、**Live Unit Testing** メニューには **[一時停止]** と **[停止]** の各オプションが表示されますが、Live Unit Testing は開始されません。 **[出力]** ウィンドウには、"このソリューションではサポートされているテスト アダプターが参照されていません..." という内容で始まるメッセージが表示されます。

いつでも、Live Unit Testing を一時停止または完全に停止できます。 たとえば、リファクタリングの途中で、しばらくテストが中断されることがわかっている場合に、これを行うことがあります。

## <a name="view-coverage-visualization"></a>カバレッジの視覚化を表示する

Live Unit Testing を有効にすると、Visual Studio エディターの各コード行が更新されて、記述しているコードが単体テストによってカバーされているかどうか、およびコードをカバーしているテストが合格かどうかが示されます。 次の図では、テストに合格したコード行と不合格のコード行、およびテストでカバーされていないコード行が示されています。 緑の "✓" で示される行は、すべてのテストに合格しています。赤い "x" で示される行は、1 つ以上のテストで不合格になっています。青い "➖" で示される行は、どのテストでもカバーされていません。

![Visual Studio でのコード カバレッジ](./media/lut-codewindow.png)

Live Unit Testing のカバレッジの視覚化は、コード エディターでコードを変更するとすぐに更新されます。 次の図のように、編集を処理している間は、合格、不合格、非カバーのシンボルの下に丸いタイマーのイメージを追加することで、データが最新ではないことが示されます。

![Visual Studio のコード カバレッジとタイマー アイコン](./media/lut-codeupdating.png)

## <a name="get-information-about-test-status"></a>テストの状態に関する情報を取得する

コード ウィンドウの合格または不合格のシンボルをカーソルでポイントすると、その行にヒットしているテストの数を確認できます。 個々のテストの状態を確認するには、記号を選択します。

![Visual Studio での記号に対するテストの状態](./media/lut-failedinfo.png)

テストの名前と結果が示されるのに加えて、ヒントを使用するとテストのセットを再実行またはデバッグできます。 ツールヒントで 1 つ以上のテストを選択して、それらのテストのみを実行またはデバッグすることもできます。 これにより、コード ウィンドウから移動することなくテストをデバッグできます。 デバッグ時には、既に設定してあるブレークポイントを確認するためだけでなく、デバッガーによって実行された <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> メソッドで予期しない結果が返されたときにも、プログラムの実行が一時停止します。

ツールヒントで不合格になったテストをポイントすると、展開されて、次の図に示すような不合格に関する追加情報が表示されます。 失敗したテストに直接移動するには、ヒントでそのテストをダブルクリックします。

![Visual Studio での失敗したテストのヒントの情報](./media/lut-failedmsg.png)

失敗したテストに移動すると、次の状態のテストがメソッドのシグネチャで視覚的に示されます。

- 合格 (中身が半分入ったビーカーと緑の "✓" で示されます)
- 不合格 (中身が半分入ったビーカーと赤い "🞩")
- Live Unit Testing に含まれない (中身が半分入ったビーカーと青い "➖")

テスト以外のメソッドにはシンボルは付きません。 次の図では、メソッドの 4 つの種類がすべて示されています。

![Visual Studio でのテスト メソッドと合格または不合格の記号](media/lut-testsource.png)

## <a name="diagnose-and-correct-test-failures"></a>不合格になったテストの診断と修正

不合格になったテストからは、簡単に製品のコードをデバッグし、編集して、アプリケーションの開発を続けることができます。 Live Unit Testing はバックグラウンドで実行されるため、デバッグ、編集、続行のサイクルの間、Live Unit Testing を停止して再起動する必要はありません。

たとえば、前の図に示した不合格になったテストの原因は、<xref:System.Char.IsLower%2A?displayProperty=fullName> メソッドに非アルファベット文字を渡すと `true` が返るという、テスト メソッドでの誤った想定です。 テスト メソッドを修正した後は、すべてのテストが合格になるはずです。 Live Unit Testing を一時停止または停止する必要はありません。

::: moniker range="vs-2017"
## <a name="test-explorer"></a>テスト エクスプローラー

**テスト エクスプローラー** で提供されるインターフェイスを使用すると、テストを実行してデバッグし、テストの結果を分析することができます。 Live Unit Testing は **テスト エクスプローラー** と統合します。 Live Unit Testing が有効になっていないか、停止されていると、**テスト エクスプローラー** には最後のテスト実行時の単体テストの状態が表示されます。 ソース コードを変更すると、テストを再実行する必要があります。 これに対し、Live Unit Testing が有効になっていると、**テスト エクスプローラー** の単体テストの状態はすぐに更新されます。 単体テストを明示的に実行する必要はありません。

> [!TIP]
> **Live Unit Testing** を開くには、Visual Studio の上部にあるメニューで、 **[テスト]**  >  **[Windows]**  >  **[テスト エクスプローラー]** の順に選択します。

**テスト エクスプローラー** ウィンドウで、一部のテストがフェード アウトしているのに気付くことがあります。たとえば、以前保存したプロジェクトを開いた後に Live Unit Testing を有効にすると、次の図のように、 **[テスト エクスプローラー]** ウィンドウで、不合格となったテストを除くすべてがフェード アウトします。 この場合、Live Unit Testing では、不合格のたテストは再実行されていますが、合格したテストは再実行されていません。 これは、Live Unit Testing の保持されているデータでは、テストが最後に正常に実行されてから変更がなかったことが示されているためです。

![テスト エクスプローラーでの不合格になったテスト](media/lut-test-explorer.png)

フェード表示されているテストは、**テスト エクスプローラー** のメニューから **[すべて実行]** または **[実行]** オプションを選択することによって、再実行できます。 または、**テスト エクスプローラー** のメニューで 1 つ以上のテストを選択し、右クリックして、ポップアップ メニューから **[選択したテストの実行]** または **[選択したテストのデバッグ]** を選択します。 実行中のテストは最上部に表示されます。

Live Unit Testing で自動的にテストを実行してテスト結果を更新するのと、**テスト エクスプローラー** からテストを明示的に実行するのには、いくつかの違いがあります。 こうした違いには、次のようなものがあります。

- [テスト エクスプローラー] ウィンドウからテストを実行またはデバッグすると標準バイナリが実行されますが、Live Unit Testing ではインストルメント化されたバイナリが実行されます。
- Live Unit Testing ではテストを実行するために新しいアプリケーション ドメインは作成されず、既定のドメインからテストが実行されます。 **[テスト エクスプローラー]** ウィンドウからテストを実行すると、新しいアプリケーション ドメインが作成されます。
- Live Unit Testing では、各テスト アセンブリで順番にテストが実行されます。 **[テスト エクスプローラー]** ウィンドウでは、複数のテストを並列に実行できます。
::: moniker-end

::: moniker range=">=vs-2019"
## <a name="live-unit-testing-window"></a>Live Unit Testing ウィンドウ

**Live Unit Testing** で提供されるインターフェイスを使用すると、**テスト エクスプローラー** と同様に、テストを実行してデバッグし、テストの結果を分析することができます。 Live Unit Testing が有効になっていると、**テスト エクスプローラー** の単体テストの状態はすぐに更新されます。 単体テストを明示的に実行する必要はありません。 Live Unit Testing が有効になっていないか、停止されていると、**Live Unit Testing** には最後のテスト実行時の単体テストの状態が表示されます。 Live Unit Testing を再開した後、テストを再実行するにはソース コードを変更する必要があります。

> [!TIP]
> Live Unit Testing を開始するには、Visual Studio の上部にあるメニューから **[テスト]**  >  **[Live Unit Testing]**  >  **[開始]** の順に選びます。 **Live Unit Testing** ウィンドウを開くには、 **[表示]**  >  **[その他のウィンドウ]**  >  **[Live Unit Testing ウィンドウ]** を使用することもできます。

**[Live Unit Testing]** ウィンドウで、一部のテストがフェード アウトしていることがあります。たとえば、Live Unit Testing を停止して再開すると、次の図に示すように、 **[Live Unit Testing]** ウィンドウのすべてのテストがフェード アウトしています。 フェード アウトされたテスト結果は、テストが最新のライブ単体テストの実行に含まれていなかったことを示します。 テストは、テストまたはテストの依存関係に対する変更が検出された場合にのみ実行されます。 変更がない場合は、不必要なテストの実行が回避されます。 この場合、グレー表示されたテスト結果は最新の実行に含まれていなかったものの、"最新の状態" です。

![テスト エクスプローラーでのフェード アウトされたテスト](media/vs-2019/lut-test-explorer.png)

フェードされているテストはどれも、コードを変更すると再実行できます。

Live Unit Testing で自動的にテストを実行してテスト結果を更新するのと、**テスト エクスプローラー** からテストを明示的に実行するのには、いくつかの違いがあります。 こうした違いには、次のようなものがあります。

- [テスト エクスプローラー] ウィンドウからテストを実行またはデバッグすると標準バイナリが実行されますが、Live Unit Testing ではインストルメント化されたバイナリが実行されます。
- Live Unit Testing ではテストを実行するために新しいアプリケーション ドメインは作成されず、既定のドメインからテストが実行されます。 **[テスト エクスプローラー]** ウィンドウからテストを実行すると、新しいアプリケーション ドメインが作成されます。
- Live Unit Testing では、各テスト アセンブリで順番にテストが実行されます。 **[テスト エクスプローラー]** ウィンドウでは、複数のテストを並列に実行できます。
::: moniker-end

## <a name="large-solutions"></a>大規模なソリューション

ソリューションに 10 個以上のプロジェクトがある場合、Visual Studio で以下の操作を行うと、次のダイアログが表示されます。

- 保持されたデータがない状態で、Live Unit Testing を開始します
- **[ツール]**  >  **[オプション]**  >  **[Live Unit Testing]**  >  **[Delete Persisted Data]\(持続データの削除\)** を選択します

![多数のプロジェクト用の Live Unit Testing ダイアログ](media/lut-large-project.png)

そのダイアログでは、大規模なプロジェクトで大量のテストを動的に実行すると、パフォーマンスが著しく低下する可能性があることが警告されます。 **[OK]** を選択すると、Live Unit Testing はそのソリューション内のすべてのテストを実行します。 **[キャンセル]** を選択すると、実行するテストを選択できます。 次のセクションでは、これを行う方法について説明します。

## <a name="include-and-exclude-test-projects-and-test-methods&quot;></a>テスト プロジェクトとテスト メソッドを含めるか除外する

多くのテスト プロジェクトが含まれるソリューションでは、Live Unit Testing に参加するプロジェクトおよびプロジェクト内の個別メソッドを制御できます。 たとえば、数百のテスト プロジェクトを含むソリューションがある場合、Live Unit Testing に参加する対象のテスト プロジェクト セットを選ぶことができます。 これを行う方法は多数あり、プロジェクトまたはソリューション内のすべてのテストを除外するか、大半のテストを含めるか除外するか、テストを個別に除外するかによって決まります。 Live Unit Testing は、包含/除外の状態をユーザー設定として保存し、ソリューションを閉じて再び開くときに記憶しています。

### <a name=&quot;exclude-all-tests-in-a-project-or-solution&quot;></a>プロジェクトまたはソリューション内のすべてのテストを除外する

単体テストで個別のプロジェクトを選ぶには、Live Unit Testing を開始した後で次のようにします。

1. ソリューション全体を除外するには、**ソリューション エクスプローラー** でソリューションを右クリックし、 **[Live Unit Testing]** 、 **[除外する]** の順に選択します。
1. 個別のテスト プロジェクトをテストに含めるには、各テスト プロジェクトを右クリックし、 **[Live Unit Testing]** 、 **[含める]** の順に選択します。

### <a name=&quot;exclude-individual-tests-from-the-code-editor-window&quot;></a>コード エディター ウィンドウからテストを個別に除外する

テスト メソッドを個別に追加または除外する場合には、コード エディター ウィンドウを使います。 コード エディター ウィンドウでテスト メソッドのシグネチャを右クリックして、次のいずれかのオプションを選択します。

- **Live Unit Testing** >  **\<selected method> を含める**
- **Live Unit Testing** >  **\<selected method> を除外する**
- **Live Unit Testing** >  **\<selected method> 以外のすべてを除外する**

### <a name=&quot;exclude-tests-programmatically&quot;></a>プログラムによってテストを除外する

Live Unit Testing でのカバレッジのレポートからメソッド、クラス、または構造体をプログラムによって除外する場合には、<xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute> 属性を適用できます。

Live Unit Testing から個別のメソッドを除外するには、次の属性を使用します。

- xUnit の場合: `[Trait(&quot;Category&quot;, &quot;SkipWhenLiveUnitTesting")]`
- NUnit の場合: `[Category("SkipWhenLiveUnitTesting")]`
- MSTest の場合: `[TestCategory("SkipWhenLiveUnitTesting")]`

Live Unit Testing からテストのアセンブリ全体を除外するには、次の属性を使用します。

- xUnit の場合: `[assembly: AssemblyTrait("Category", "SkipWhenLiveUnitTesting")]`
- NUnit の場合: `[assembly: Category("SkipWhenLiveUnitTesting")]`
- MSTest の場合: `[assembly: TestCategory("SkipWhenLiveUnitTesting")]`

## <a name="see-also"></a>関連項目

- [コード テスト ツール](https://visualstudio.microsoft.com/vs/testing-tools/)
- [Live Unit Testing のブログ](https://devblogs.microsoft.com/visualstudio/live-unit-testing-in-visual-studio-2017-enterprise/)
- [ライブ単体テストに関する FAQ](live-unit-testing-faq.yml)
- [Channel 9 ビデオ: Visual Studio の Live Unit Testing](https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T105)
