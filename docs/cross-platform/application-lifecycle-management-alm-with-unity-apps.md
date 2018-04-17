---
title: Unity アプリを使用したアプリケーション ライフサイクル管理 (ALM) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.technology: vs-unity-tools
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2dc61e63-9ba2-4c16-b1ad-f46249e576b6
author: dantogno
ms.author: v-davian
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 05196d7c9e6b1b441db61f599dcfe39c4d5cba56
ms.sourcegitcommit: fb1fede41d8c5e459dd222755b0497b9d361bc51
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="application-lifecycle-management-alm-with-unity-apps"></a>Unity アプリを使用したアプリケーション ライフサイクル管理 (ALM)
最新のプラットフォーム向けのアプリ開発には、コードを記述するだけでなく、それ以外の多くのアクティビティが関係します。 これらのアクティビティは、アプリの完全なライフサイクルの中で DevOps (開発 + 運用) 期間になされるものあり、たとえば、作業のアジャイルな計画と追跡、コードの設計と実装、ソース コード リポジトリの管理、ビルドの実行、継続的に実行されるインテグレーションと展開の管理、テスト (単体テストと UI テストを含む)、開発環境と運用環境の両方におけるさまざまな形式の診断の実行、製品利用統計情報と分析によるアプリのパフォーマンスとユーザー動作のリアルタイムな監視などがあります。

 Visual Studio、Visual Studio Team Services、および Team Foundation Server は、さまざまな DevOps 機能 (アプリケーション ライフサイクル管理 (ALM) とも呼ばれる) を提供しています。 これらの多くは、特にスクリプト言語として C# を使用している場合の Unity で作成したゲームや没入感のあるグラフィカル アプリなど、プラットフォーム間のプロジェクトに適用されます。 ただし、Unity は、独自の開発環境とランタイム エンジンがあるため、多くの ALM 機能が Visual Studio でビルドされた他の種類のプロジェクトのようには適用されません。

 次の表は、Unity を使用するときの Visual Studio ALM の機能を適用する方法と適用しない方法について示しています。 各機能そのものの詳細については、リンク先のドキュメントを参照してください。

## <a name="agile-tools"></a>アジャイル ツール
 参照リンク: **[作業](http://msdn.microsoft.com/Library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)** (Visual Studio Team Services または TFS (Team Explorer Everywhere など) を使用)

 一般的なコメント: すべての計画機能と追跡機能は、プロジェクトの種類とコーディング言語には依存しません。

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|バックログとスプリントの管理|[はい]||
|作業の追跡|[はい]||
|チーム ルーム コラボレーション|[はい]||
|かんばんボード|[はい]||
|進行状況のレポートと視覚化|[はい]||

## <a name="modeling"></a>モデリング
 参照リンク: **[アーキテクチャの分析およびモデリング](../modeling/analyze-and-model-your-architecture.md)**

 一般的なコメント: これらのデザイン機能は、コーディング言語に関係がないか、C# などの .NET 言語と共に使用されますが、オブジェクト階層およびクラスのリレーションシップを含む従来のアプリケーションのパラダイムで動作します。 Unity 内でのゲームの設計には、さまざまなパラダイムが含まれ、たとえばグラフィカル オブジェクト、サウンド、シェーダー、スクリプトなどのリレーションシップがあります。 このため、Visual Studio モデリング ダイアグラム ツールが、Unity プロジェクト全体に特に関連するわけではありません。 C# スクリプト内でのリレーションシップを管理するために使用することもできますが、それは全体の中の一部にすぎません。

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|シーケンス図|×||
|依存関係グラフ|×||
|呼び出し階層|×||
|クラス デザイナー|×||
|アーキテクチャ エクスプローラー|×||
|UML 図 (ユース ケース、アクティビティ、クラス、コンポーネント、シーケンス、および DSL)|×||
|レイヤー図|×||
|レイヤー検証|×||

## <a name="code"></a>コード

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|[Team Foundation バージョン管理](http://msdn.microsoft.com/Library/1d629052-c65d-4c5d-81eb-eaa4413fe285) または Visual Studio Team Services を使用|[はい]|Unity プロジェクトは、単に他のプロジェクトのように、バージョン管理システムに配置することができる複数のファイルですが、この表の下に記載したいくつかの特別な考慮事項があります。|
|[Team Services で Git を使用した作業の開始](http://msdn.microsoft.com/Library/32f46ecd-1b03-4ef0-a9c4-8a120da2b03f)|[はい]|表の下の注を参照してください。|
|[コード品質の向上](/visualstudio/test/improve-code-quality)|[はい]||
|[コード変更およびその他の履歴の検索](../ide/find-code-changes-and-other-history-with-codelens.md)|[はい]||
|[コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)|[はい]||

 Unity を使ったバージョン管理に関する注意事項:

1.  Unity は、既定では非表示の 1 つの非透過のライブラリでのゲーム資産に関するメタデータを追跡します。 ファイルとメタデータの同期を保つするには、メタデータを表示してより管理しやすいチャンク単位で格納する必要があります。 詳細については、「[Using External Version Control Systems with Unity](http://docs.unity3d.com/Manual/ExternalVersionControlSystemSupport.html)」 (Unity で外部のバージョン管理システムを使用する) (Unity ドキュメント) を参照してください。

2.  上記のリンクで説明するように、Unity プロジェクトのすべてのファイルとフォルダーがソース管理に適しているわけではありません。 Assets フォルダーと ProjectSettings フォルダーを追加する必要がありますが、Library フォルダーと Temp フォルダーは追加しないでください。 ソース管理にならない生成されたファイルの追加のリストについては、StackOverflow の「[Unity3D ソース管理に Git を使用する方法](http://stackoverflow.com/questions/18225126/how-to-use-git-for-unity3d-source-control)」を参照してください。 多くの開発者が、このテーマについて個別にブログに書いています。

3.  テクスチャやオーディオ ファイルなど、Unity プロジェクトでのバイナリの資産が、大量のストレージを消費することがあります。 Git などのさまざまなソース管理システムは、変更がファイルのごく一部のみに影響する場合でも、すべての変更個所のファイルの一意のコピーを格納します。 これにより、Git リポジトリがいっぱいになる可能性があります。 これに対処するために、Unity 開発者は多くの場合、リポジトリに最終資産のみを追加し、OneDrive、DropBox、git の添付など、資産の作業履歴を保持するために様々な手段を使用しています。 通常このような資産は、ソース コードの変更に伴うバージョン管理を必要としないため、このアプローチが有効です。 また、開発者は、プロジェクト エディターの資産のシリアル化モードを、シーンファイルをバイナリ形式ではなくテキストで保存するためにテキストを強制するよう設定し、これによりソース管理でのマージが可能になります。 詳細については、「[Editor Settings](http://docs.unity3d.com/Manual/class-EditorManager.html)」 (エディターの設定) (Unity ドキュメント) を参照してください。

## <a name="build"></a>ビルド
 参照リンク: **[ビルドとリリース](/vsts/build-release/index)**

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|オンプレミス TFS サーバー|可能|Unity プロジェクトは、Visual Studio が構築したシステムではなく、Unity の環境内で構築されています (Visual Studio Tools for Unity 内で構築すると、スクリプトはコンパイルしますが、実行可能ファイルを生成しません)。 [コマンド ラインから Unity プロジェクトをビルド](http://docs.unity3d.com/Manual/CommandLineArguments.html) (Unity ドキュメント) できるため、Unity 自体がそのコンピューターにインストールされている場合は、TFS サーバーで MSBuild プロセスを構成して、適切な Unity コンポーネントを実行できます。<br /><br /> また、Unity は、[Unity クラウド構築](https://build.cloud.unity3d.com/landing/)も提供し、Git または SVN リポジトリを監視して、定期的なビルドを実行します。 現時点では、Team Foundation バージョン管理または Visual Studio Team Services では動作しません。|
|Visual Studio Team Services にリンクされたオンプレミスのビルド サーバー|可能|上記と同じ状態の場合、Visual Studio Team Services でトリガーされたビルドを指して、オンプレミスの TFS のコンピューターを使用することがさらに可能になります。  手順については、「[Build and release agents](/vsts/build-release/concepts/agents/agents)」 (ビルド エージェントとリリース エージェント) を参照してください。|
|Visual Studio Team Services のホスト コントローラー サービス|×|Unity ビルドは現在サポートされていません。|
|事前スクリプトと事後スクリプトによるビルド定義|[はい]|Unity のコマンドラインを使用してビルドを実行するカスタムのビルド定義は、ビルド前およびビルド後のスクリプトに対して構成することもできます。|
|継続的な統合 (ゲート チェックインを含む)|[はい]|Git としての TFVC へのゲート チェックインのみ、チェックイン モデルではなく、プル要求モデルで機能します。|

## <a name="testing"></a>テスト中

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|テストの計画、テスト ケースの作成、およびテスト スイートの編成|[はい]||
|手動テスト|[はい]||
|テスト マネージャー (テストの記録と再生)|Windows デバイスと Android エミュレーターのみ||
|コード カバレッジ|N/A|単体テストとしての該当なしは、Unity と Visual Studio で発生します。以下を参照してください。|
|[コードの単体テスト](../test/unit-test-your-code.md)|Unity 内。Visual Studio 内ではありません。|Unity は、独自の単体テスト フレームワークを [Unity テスト ツール](https://www.assetstore.unity3d.com/en/#!/content/13802) (Unity Asset Store) の一部として提供しています。 単体テストの結果は、Unity 内でレポートされ、Visual Studio 内では表示されません。|
|[UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)|×|コード化された UI テストは、アプリの UI で読み取り可能なコントロールに依存します。Unity アプリケーションは本質的にはグラフィカルであるため、コンテンツはコード化された UI テストのツールで読み取ることはありません。|

## <a name="improve-code-quality"></a>コード品質の向上

参照リンク: **[コードの品質の向上](/visualstudio/test/improve-code-quality)**

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|[マネージ コードの品質の分析](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)|[はい]|Visual Studio 内の C# スクリプト コードを分析できます。|
|[コード クローン検出を使用した重複コードの検出](http://msdn.microsoft.com/Library/a97cd5a6-5ffa-4104-9627-8e59e513654d)|[はい]|Visual Studio 内の C# スクリプト コードを分析できます。|
|[マネージ コードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)|[はい]|Visual Studio 内の C# スクリプト コードを分析できます。|
|[パフォーマンス エクスプローラー](../profiling/performance-explorer.md)|×|[Unity Profiler](http://docs.unity3d.com/Manual/Profiler.html) の使用 (Unity Web サイト)。|
|[.Net Framework のメモリ分析の問題](https://msdn.microsoft.com/en-us/library/dn342825.aspx)|×|Visual Studio ツールには、(Unity で使用するような) プロファイリング用の Mono フレームワークへのフックはありません。 [Unity Profiler](http://docs.unity3d.com/Manual/Profiler.html) の使用 (Unity ドキュメント)。|

## <a name="release-management"></a>リリース管理
 参照リンク: **[リリース管理による配置の自動化](https://msdn.microsoft.com/library/vs/alm/release/overview)**

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|リリース プロセスの管理|[はい]||
|スクリプトによるサイドローディング用のサーバーへの配置|[はい]||
|アプリ ストアへのアップロード|Partial|一部のアプリ ストアに対して、このプロセスを自動化することができる拡張機能が使用できます。  たとえば、[Google Play の拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play)については、[Visual Studio Team Services の拡張機能](https://marketplace.visualstudio.com/VSTS)を参照してください。|

## <a name="monitor-with-hockeyapp"></a>HockeyApp による監視
 参照リンク: **[HockeyApp による監視](https://www.hockeyapp.net/features/)**

|機能|Unity でサポートされているかどうか|その他のコメント|
|-------------|--------------------------|-------------------------|
|クラッシュ分析、製品利用統計情報、およびベータ版の配布|[はい]|HockeyApp は、主にベータ分布を処理し、クラッシュ レポートを取得するために役立ちます。<br /><br /> C# スクリプトからの製品利用統計情報の場合、Unity によって使用される .NET のバージョンで実行されるときは、分析用のフレームワークを使用することができます。 ただし、ゲームのスクリプト内でのみ分析でき、Unity エンジン内で詳細に分析することはできません。 現時点では、Application Insights のプラグインはありませんが、[Unity Analytics](https://www.assetstore.unity3d.com/en/#!/content/28120) や [Google Analytics](https://github.com/googleanalytics/google-analytics-plugin-for-unity) などの他の分析ソリューションのプラグインが使用できます。 Unity プロジェクトの特性を理解する Unity Analytics のようなサービスは、汎用的なフレームワークもより効果的な分析を提供します。|
