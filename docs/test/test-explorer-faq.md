---
title: テスト エクスプローラーに関する FAQ
ms.date: 11/07/2018
ms.topic: conceptual
helpviewer_keywords:
- Test Explorer
- Test window
- Visual Studio Test Explorer
- summary line
- unit tests
- Test Explorer FAQ
ms.author: kehavens
ms.workload:
- multiple
author: kendrahavens
manager: jillfra
ms.openlocfilehash: 2efecd936dea0d764058b795457e89cdc700d902
ms.sourcegitcommit: 3d37c2460584f6c61769be70ef29c1a67397cf14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "58323569"
---
# <a name="visual-studio-test-explorer-faq"></a>Visual Studio テスト エクスプローラーに関する FAQ

## <a name="dynamic-test-discovery"></a>動的なテストの検出

**テスト エクスプローラーが、動的に定義されたテストを検出しません(理論、カスタム アダプター、カスタム特性、#ifdefs など)。これらのテストを検出するにはどうすればよいですか?**

プロジェクトをビルドして、**[ツール]** > **[オプション]** > **[テスト]** の順に移動して、アセンブリベースの検出がオンになっていることを確認します。

[リアルタイムのテスト検出](https://go.microsoft.com/fwlink/?linkid=862824)は、ソース ベースのテストの検出です。 理論、カスタム アダプター、カスタム特性、`#ifdef` ステートメントなどは実行時に定義されるため、これらを使うテストは検出できません。 これらのテストを正確に検出するには、ビルドが必要です。 Visual Studio 2017 バージョン 15.6 以降では、アセンブリベースの検出 (従来の検出プログラム) はビルドの後にのみ実行されます。 この設定は、リアルタイムのテスト検出は、ユーザーが編集中にできるだけ多くのテストを検出し、アセンブリベースの検出では、ビルド後に動的に定義されたテストを表示できるようにすることを意味します。 リアルタイムのテスト検出は、応答性を高めながら、ビルド後に完全かつ正確な結果を得ることができます。

## <a name="test-explorer--plus-symbol"></a>テスト エクスプローラーの '+' (プラス) 記号

**テスト エクスプローラーの最初の行に表示される '+' (プラス) 記号は何を意味しているのですか?**

"+" (プラス) 記号は、アセンブリベースの検出がオンになっていると、ビルド後にさらに多くのテストが検出される可能性があることを示しています。 この記号は、プロジェクト内で動的に定義されているテストが検出されると表示されます。

![サマリー行のプラス記号](media/testex-plussymbol.png)

## <a name="assembly-based-discovery"></a>アセンブリベースの検出

**プロジェクトでアセンブリベースの検出が機能しなくなりました。元に戻すにはどうしたらよいですか?**

**[ツール]** > **[オプション]** > **[テスト]** の順に移動して、**[ビルド後にビルド済みアセンブリからテストをさらに探索する]** チェック ボックスをオンにします。

![アセンブリベースのオプション](media/testex-toolsoptions.png)

## <a name="real-time-test-discovery"></a>リアルタイムのテスト検出

**プロジェクトをビルドしなくても、入力中にテストがテスト エクスプローラーに表示されるようになりました。何か変更されたのでしょうか?**

この機能は、[リアルタイムのテスト検出](https://go.microsoft.com/fwlink/?linkid=862824)と呼ばれます。 これは Roslyn アナライザーを使用してテストを検出し、リアルタイムでテスト エクスプローラーに表示します。プロジェクトをビルドする必要はありません。 理論やカスタムの特徴などの動的に定義されたテストに対するテスト検出の動作については、FAQ #1 を参照してください。

## <a name="real-time-test-discovery-compatibility"></a>リアルタイムのテスト検出の互換性

**リアルタイムのテスト検出では、どの言語およびテスト フレームワークを使用できますか?**

[リアルタイムのテスト検出](https://go.microsoft.com/fwlink/?linkid=862824)は、Roslyn コンパイラを使用してビルドされているため、マネージド言語 (C# および Visual Basic) に対してのみ機能します。 今のところ、リアルタイムのテスト検出は xUnit、NUnit、MSTest のフレームワークに対してのみ機能します。

## <a name="test-explorer-logs"></a>テスト エクスプローラーのログ

**どうすればテスト エクスプローラーのログを有効にできますか?**

**[ツール]** > **[オプション]** > **[テスト]** の順に移動し、そこで [ログ] セクションを見つけます。

## <a name="uwp-test-discovery"></a>UWP のテストの検出

**アプリを配置するまで UWP プロジェクトのテストが検出されないのはなぜですか?**

アプリが配置されると、UWP テストは異なるランタイムを対象にします。 つまり、UWP プロジェクトで正確にテストを検出するには、プロジェクトをビルドするだけでなく、配置することも必要です。

## <a name="test-explorer-sorting"></a>テスト エクスプローラーの並べ替え

**階層ビューでテスト結果を並べ替えるにはどうすればよいですか?**

階層ビューでは、結果順ではなくアルファベット順にテストが並べ替えられます。 通常、他のグループ化設定は、テスト結果を結果順に並べ替えてからアルファベット順に並べ替えます。 次の比較図で、オプションによるグループの違いを確認してください。 [この GitHub の問題で](https://github.com/Microsoft/vstest/issues/1425)設計に関するフィードバックを提供できます。

![SortingExamples](media/testex-sortingex.png)

## <a name="test-explorer-hierarchy-view"></a>テスト エクスプローラーの階層ビュー

**階層ビューに、プロジェクト、名前空間、およびクラス グループの横に、合格、失敗、省略、および未実行アイコンがあります。これらのアイコンの意味を教えてください。**

プロジェクト、名前空間、およびクラス グループの横にあるアイコンは、そのグループ内のテストの状態を示します。 次の表を参照してください。

![テスト エクスプローラーの階層のアイコン](media/testex-hierarchyicons.png)

## <a name="search-by-file-path"></a>ファイル パスによる検索

**テスト エクスプローラーの検索ボックスの "ファイル パス" フィルターはもう存在しません。**

**テスト エクスプローラー**の検索ボックスのファイル パス フィルターは、Visual Studio 2017 バージョン 15.7 で削除されました。 この機能は使用頻度が低く、この機能を除外することで、テスト エクスプローラーはテスト メソッドを高速で取得できます。 この変更によって開発フローが中断される場合は、[開発者コミュニティ](https://developercommunity.visualstudio.com/)でフィードバックを送信してその旨をお知らせください。

## <a name="remove-undocumented-interfaces"></a>ドキュメントに記載されていないインターフェイスを削除する

**テストに関連する一部の API は、Visual Studio 2019 には存在していません。何か変更されたのでしょうか?**

Visual Studio 2019 では、前にパブリックとしてマークされていたが、ドキュメントに正式に記載されたことがないいくつかのテスト ウィンドウ API が削除されます。 これらは、拡張機能の管理者に対して早期に警告を発するために、Visual Studio 2017 で "非推奨" としてマークされていました。 弊社の知る限りでは、これらの API を検出して依存関係を築いている拡張機能は、ごくわずかです。 これらのメソッドには、`IGroupByProvider`、`IGroupByProvider<T>`、`KeyComparer`、`ISearchFilter`、`ISearchFilterToken`、`ISearchToken`、および `SearchFilterTokenType` が含まれます。 この変更が拡張機能に影響を与える場合は、[開発者コミュニティ](https://developercommunity.visualstudio.com)でバグを入力して、その旨をお知らせください。

## <a name="test-adapter-nuget-reference"></a>テスト アダプターの NuGet 参照

**Visual Studio 2017 バージョン 15.8 で、テストは検出されますが、実行されません。**

すべてのテスト プロジェクトで、各 .csproj ファイルに .NET テスト アダプターの NuGet 参照を含める必要があります。 含めない場合は、ビルド後にテスト アダプター拡張機能の検出が開始されるとき、またはユーザーが選択したテストを実行しようとするときに、次のテスト出力がプロジェクトに表示されます。

**テスト プロジェクト {} では、いかなる .NET NuGet アダプターも参照されません。このプロジェクトでは、テスト検出または実行が動作しないことがあります。ソリューションの各 .NET テスト プロジェクトで NuGet テスト アダプターを参照することをお勧めします。**

テスト アダプター拡張機能を使用する代わりに、プロジェクトではテスト アダプターの NuGet パッケージを使用する必要があります。 この要件により、パフォーマンスが大幅に向上し、継続的インテグレーションでの問題が減少します。 .NET テスト アダプター拡張機能の非推奨について詳しくは、[リリース ノート](/visualstudio/releasenotes/vs2017-relnotes-v15.8#testadapterextension)をご覧ください。

> [!NOTE]
> NUnit 2 のテスト アダプターを使用していて、NUnit 3 のテスト アダプターに移行できない場合は、Visual Studio バージョン 15.8 で **[ツール]** > **[オプション]** > **[テスト]** の順に選択して、この新しい検出の動作をオフにできます。

![ツール オプションでのテスト エクスプローラー アダプターの動作](media/testex-adapterbehavior.png)

## <a name="uwp-testcontainer-was-not-found"></a>UWP TestContainer が見つかりませんでした

**UWP テストが Visual Studio 2017 バージョン 15.7 以降で実行されなくなりました。**

最近の UWP テスト プロジェクトでは、テスト アプリを識別するためのパフォーマンスを向上させるため、テスト プラットフォームのビルド プロパティを指定します。 Visual Studio バージョン 15.7 より前に初期化された UWP テスト プロジェクトがある場合は、**[出力]** > **[テスト]** でこのエラーが表示される場合があります。

**System.AggregateException: 1 つまたは複数のエラーが発生しました。 ---> System.InvalidOperationException:次の TestContainer が {} Microsoft.VisualStudio.TestWindow.Controller.TestContainerProvider \<GetTestContainerAsync>d__61.MoveNext()** で見つかりませんでした

このエラーを修復するには:

- 次のコードを使用して、テスト プロジェクトのビルド プロパティを更新します。

```XML
<UnitTestPlatformVersion Condition="'$(UnitTestPlatformVersion)' == ''">$(VisualStudioVersion)</UnitTestPlatformVersion>
```

- 次のコードを使用して、TestPlatform SDK バージョンを更新します。

```XML
<SDKReference Include="TestPlatform.Universal, Version=$(UnitTestPlatformVersion)" />
```

## <a name="using-feature-flags"></a>機能フラグの使用

**新しいテスト機能を試すために機能フラグをオンにするにはどうしたらよいですか?**

機能フラグは、機能を公式に出荷する前に、フィードバックを提供する熱心なユーザー向けに、製品の実験用または未完成部分を出荷するために使用されます。 これは IDE エクスペリエンスの安定性を損なう可能性があります。 仮想マシンなどの安全な開発環境でのみ使用してください。 機能フラグの設定は、常に各自の責任で行ってください。 実験用の機能は、[機能フラグの拡張機能](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.FeatureFlagsExtension)を使用するか、開発者コマンド プロンプトを使用してオンにすることができます。

![機能フラグの拡張機能](media/testex-featureflag.png)

Visual Studio 開発者コマンド プロンプトで機能フラグをオンにするには、次のコマンドを使用します。 パスをご使用のコンピューターの Visual Studio のインストール場所に変更し、レジストリ キーを目的の機能フラグに変更します。

```shell
vsregedit set “C:\Program Files (x86)\Microsoft Visual Studio\Preview\Enterprise" HKLM FeatureFlags\TestingTools\UnitTesting\HierarchyView Value dword 1
```

> [!NOTE]
> dword の後の値を 1 ではなく 0 にすると、同じコマンドでフラグをオフにできます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=fullName>
- [既存コードに対する単体テストの作成と実行](https://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173)
- [コードの単体テスト](unit-test-your-code.md)
- [Live Unit Testing に関する FAQ](live-unit-testing-faq.md)
