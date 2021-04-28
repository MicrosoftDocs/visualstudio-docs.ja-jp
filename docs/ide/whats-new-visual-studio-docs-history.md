---
title: 'Visual Studio のドキュメント:新機能の履歴 '
titleSuffix: ''
description: Visual Studio ドキュメントの新機能に関する履歴
ms.date: 03/08/2021
helpviewer_keywords:
- Visual Studio, what's new, docs
- what's new [Visual Studio]
ms.assetid: 511DAFC7-896E-449A-BFF7-0E8F7BBA8A78
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: d29c8be82ba0461231d9cd02eb6799dd38a690ed
ms.sourcegitcommit: 5fb684ff8729eb118aa91ce9f049c79eeb9747b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2021
ms.locfileid: "107913034"
---
# <a name="history-of-whats-new-in-visual-studio-docs"></a>Visual Studio ドキュメントの新機能に関する履歴

Visual Studio ドキュメントの新機能に関する履歴へようこそ。この記事には、2021 年 3 月より前 (2020 年 7 月以降) のドキュメントに対する主な変更点が含まれます。 最新の新機能については、[Visual Studio の最新情報](whats-new-visual-studio-docs.md)に関するドキュメントを参照してください。

## <a name="february-2021"></a>2021 年 2 月

### <a name="debugger"></a>デバッガー

**更新された記事**

- [Visual Studio デバッガーでブレークポイントを使用する](../debugger/using-breakpoints.md) - アクセシビリティの更新

### <a name="get-started"></a>作業開始

**更新された記事**

- [チュートリアル: Visual Studio 2017 でリポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo-visual-studio-2017.md) - VS2017 を使ってリポジトリからプロジェクトを開く方法に関するセクションの関連項目リンクの更新
- [チュートリアル: リポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo-visual-studio-2019.md) - 「リポジトリからプロジェクトを開く」ページに VS2017 バージョンへのリンクを追加

### <a name="ide"></a>IDE

**更新された記事**

- [MSBuild に関する問題のトラブルシューティングとログ記録](./msbuild-logs.md) - プロジェクト システム ツールの拡張機能の使用に関する手順の追加

### <a name="install"></a>インストール

**更新された記事**

- [最小限のオフライン レイアウトを使用して Visual Studio を更新する](../install/update-minimal-layout.md)
  - オプション テーブルに 2017 の例を追加
  - VS2017 の例を追加

### <a name="msbuild"></a>MSBuild

**新しい記事**

- [MSB3644: 'FrameworkVersion' の参照アセンブリが見つかりませんでした](../msbuild/errors/msb3644.md) - MSBuild エラー
- [MSB8036: Windows SDK' バージョン' が見つかりませんでした](../msbuild/errors/msb8036.md) - MSBuild エラー

### <a name="test"></a>テスト

**更新された記事**

- [Visual Studio で C++ 用の Microsoft 単体テスト フレームワークを使用する](../test/how-to-use-microsoft-test-framework-for-cpp.md) - 小さいコンテンツの更新と編集
- [Visual Studio で C++ DLL 用の単体テストを作成する](../test/how-to-write-unit-tests-for-cpp-dlls.md) - 小さいコンテンツの更新と編集
- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md) - アクセシビリティの更新
- [チュートリアル: マネージド コードの単体テストを作成し、実行する](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md) - アクセシビリティの更新
- [Microsoft Fakes を使用したテストでコードを分離する](../test/isolating-code-under-test-with-microsoft-fakes.md) - Fakes ドキュメントで .NET 5.0 を明示的に記述する

## <a name="january-2021"></a>2021 年 1 月
### <a name="azure"></a>Azure

**新しい記事**

- [Visual Studio で Cloud Services (拡張サポート) を作成してデプロイする (プレビュー)](../azure/cloud-services-extended-support.md) - Cloud Services の拡張サポート - テンプレートなし

### <a name="code-quality"></a>コード品質

**新しい記事**

- [コード メトリックス - クラスの結合](../code-quality/code-metrics-class-coupling.md) - コード メトリックスを更新
- [コード メトリックス - 保守容易性インデックスの範囲と意味](../code-quality/code-metrics-maintainability-index-range-and-meaning.md) - コード メトリックスを更新

### <a name="debugger"></a>デバッガー

**新しい記事**

- [Visual Studio を使用して WSL 2 で .NET Core アプリをデバッグする](../debugger/debug-dotnet-core-in-wsl-2.md) - .NET Core WSL2 でのデバッグ

**更新された記事**

- [Natvis フレームワークを使用してデバッガーで C++ オブジェクトのカスタム ビューを作成する](../debugger/create-custom-views-of-native-objects.md)- Natvis での特殊文字の XML 書式設定の説明
- [セキュリティ警告: 信頼されていないユーザーが所有するプロセスにアタッチするには危険が伴います。以下の情報に関して疑わしい点がある場合や、不明な場合は、このプロセスにアタッチしないでください](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md) - 信頼されていないプロセスへのアタッチ時のセキュリティ警告を更新

### <a name="deployment"></a>デプロイ

**更新された記事**

- [&lt;InstallChecks&gt; 要素 (ブートストラップ)](../deployment/installchecks-element-bootstrapper.md) - 新しい BeforeInstallChecks 要素を含めるためにブートストラップ パッケージのドキュメントを更新

### <a name="extensibility"></a>機能拡張

**更新された記事**

- [チュートリアル: Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md) - [PUBLIC_MOVE] パブリック PR 6214 からコミット

### <a name="get-started"></a>はじめに

**新しい記事**

- [チュートリアル: Visual Studio 2017 でリポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo-visual-studio-2017.md) - 「リポジトリからプロジェクトを開く」チュートリアルを更新

**更新された記事**

- [チュートリアル: リポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo.md) - 「リポジトリからプロジェクトを開く」チュートリアルを更新

### <a name="ide"></a>IDE

**新しい記事**

- [Visual Studio の JavaScript の F1 ヘルプ](./not-in-toc/default-f1-javascript.md) - JS と TS の既定の F1 ページを追加
- [Visual Studio の TypeScript F1 ヘルプ](./not-in-toc/default-f1-typescript.md) - JS と TS の既定の F1 ページを追加

**更新された記事**

- [Visual Studio のソリューションとプロジェクト](./solutions-and-projects-in-visual-studio.md) - Visual Studio Image Library へのリンクを追加

### <a name="install"></a>インストール

**更新された記事**

- [Visual Studio のビルド番号とリリース日](../install/visual-studio-build-numbers-and-release-dates.md) - 月例パッチを更新

### <a name="msbuild"></a>MSBuild

**更新された記事**

- [MSBuild 用語集](../msbuild/msbuild-glossary.md) - 用語集のキーを H2 にレベル上げ

### <a name="profiling"></a>プロファイル

**新しい記事**

- [Visual Studio プロファイラーから dotnet カウンターを視覚化する](../profiling/dotnet-counters-tool.md) - .NET カウンター ツールのドキュメントを追加

### <a name="test"></a>テスト

**更新された記事**

- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md) - 「オーディオ キューのテスト」ドキュメントを追加

## <a name="december-2020"></a>2020 年 12 月
### <a name="azure"></a>Azure

**新しい記事**

- [Visual Studio 接続済みサービスを使用した Azure App Configuration の追加](../azure/vs-azure-tools-connected-services-app-configuration.md) - App Configuration 接続済みサービスのチュートリアル

### <a name="code-quality"></a>コード品質

**更新された記事**

- [概要](../code-quality/use-roslyn-analyzers.md) - editorconfig を使用したコマンド ラインからのビルド
- [ファーストパーティの .NET アナライザーを有効またはインストールする](../code-quality/install-net-analyzers.md)
  - FxCopAnalyzers から NetAnalyzers への移行に関するドキュメントをより明確にする
  - .NET アナライザーの目次を再配置する
- [FxCop アナライザーから .NET アナライザーに移行する](../code-quality/migrate-from-fxcop-analyzers-to-net-analyzers.md) - FxCopAnalyzers から NetAnalyzers への移行に関するドキュメントをより明確にする

### <a name="containers"></a>コンテナー

**更新された記事**

- [Docker を使用した Visual Studio 開発のトラブルシューティング](../containers/troubleshooting-docker-errors.md) - Docker for Visual Studio トラブルシューティング ガイドの更新

### <a name="debugger"></a>デバッガー

**更新された記事**

- [FAQ - Visual Studio で必要なデバッグ機能を見つける](../debugger/find-your-debugging-task.md) - デバッグ タスクおよび概要のトピックを見つけるための検出作業

### <a name="get-started"></a>作業開始

**更新された記事**

- [チュートリアル: Visual Studio でシンプルな C# コンソール アプリを作成する](../get-started/csharp/tutorial-console.md) - C# コンソール チュートリアル: VS 2019 にはパート 2 のみ適用されます

### <a name="ide"></a>IDE

**更新された記事**

- [Visual Studio でのソリューションとプロジェクト](./solutions-and-projects-in-visual-studio.md) - ソリューションおよびプロジェクトのトピックに対する更新
- [Visual Studio での新しいプロジェクトの作成](./create-new-project.md)
  - スクリーンショットおよび図用の代替テキストの調整
  - ソリューションおよびプロジェクトのトピックに対するその他の更新
- [IDE エラーのトラブルシューティング用のリソース](./reference/resources-for-troubleshooting-integrated-development-environment-errors.md) - 古くなったフォーラム リソース セクションの改訂
- [ソリューションとプロジェクトの使用](./creating-solutions-and-projects.md) - ソリューションとプロジェクトのトピックに対するその他の更新
- [Visual Studio または Visual Studio Installer に関する問題を報告する方法](./how-to-report-a-problem-with-visual-studio.md)
  - スクリーンショットの更新
  - 開発者コミュニティの変更
- [Visual Studio のパフォーマンスに関するヒントとテクニック](./visual-studio-performance-tips-and-tricks.md) - 「診断ツールを無効にする」セクションの更新
- [プロジェクトとソリューションの概要](../get-started/tutorial-projects-solutions.md)
  - ソリューションおよびプロジェクトのトピックに対する更新
  - tutorial-projects-solutions.md の更新
  - メニュー オプションで見つからない

### <a name="test"></a>テスト

**更新された記事**

- [単体テストの概要](../test/getting-started-with-unit-testing.md) - テスト ツールの検出作業とその他の機能強化
- [初めて Visual Studio のテスト ツールを検討する](../test/improve-code-quality.md) - テスト ツールの検出作業とその他の機能強化
- [Visual Studio でのテスト ツール (番号が必要)、ページ タイトルを検索結果に表示。60 文字以内でブランド名を追加。](../test/index.yml) テスト ツールの検出作業とその他の機能強化
- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md) - さまざまなフレームワークに合わせて動的なプレイリスト xml を追加する

## <a name="november-2020"></a>2020 年 11 月
### <a name="code-quality"></a>コード品質

**新しい記事**

- [.NET アナライザーの有効化またはインストール](../code-quality/install-net-analyzers.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [FxCop アナライザーから .NET アナライザーに移行する](../code-quality/migrate-from-fxcop-analyzers-to-net-analyzers.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [従来の分析 (FxCop) からソース分析 (.NET アナライザー) に移行する](../code-quality/migrate-from-legacy-analysis-to-net-analyzers.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [従来の FxCop と .NET アナライザーについてよく寄せられる質問](../code-quality/net-analyzers-faq.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加

**更新された記事**

- [コード分析の FAQ](../code-quality/analyzers-faq.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [FxCop ルール ポートの状態](../code-quality/fxcop-rule-port-status.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [非推奨のルール](../code-quality/fxcop-unported-deprecated-rules.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [未移植で移植可能なルール](../code-quality/fxcop-unported-rules-may-get-ported.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [未移植のルール](../code-quality/fxcop-unported-rules.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [サードパーティーのアナライザーをインストールする](../code-quality/install-roslyn-analyzers.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加
- [概要](../code-quality/use-roslyn-analyzers.md) - FxCop アナライザーから .NET アナライザーに移行するためのドキュメントを追加

### <a name="containers"></a>コンテナー

**更新された記事**

- [Bridge to Kubernetes のしくみ](../containers/overview-bridge-to-kubernetes.md) -Kubernetes のアクセス許可のセクション

### <a name="debugger"></a>デバッガー

**新しい記事**

- [Docker コンテナーで実行されているプロセスにアタッチする](../debugger/attach-to-process-running-in-docker-container.md) - Linux のシナリオのプロセス ドキュメントへのリファクタリングのアタッチ

**更新された記事**

- [Visual Studio デバッガーを使用して実行中のプロセスにアタッチする](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md) - Linux のシナリオのプロセス ドキュメントへのリファクタリングのアタッチ
- [Linux でプロセスへのアタッチにより SSH を使用して .NET Core をデバッグする](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md) - Linux のシナリオのプロセス ドキュメントへのリファクタリングのアタッチ

### <a name="deployment"></a>デプロイ

**新しい記事**

- [ClickOnce を使用して .NET Windows デスクトップ アプリケーションを配置する](../deployment/quickstart-deploy-using-clickonce-folder.md) - .NET Windows プロジェクト用 ClickOnce のクイック スタートを追加

**更新された記事**

- [Visual Studio での配置の概要](../deployment/deploying-applications-services-and-components.md)
  - パスを編集する
  - .NET 5 の探索可能性とリンクの更新
- [Visual Studio での配置 (番号が必要)、ページ タイトルを検索結果に表示。60 文字以内でブランド名を追加。](../deployment/index.yml) - .NET 5 の探索可能性とリンクの更新
- [コマンド ラインから ClickOnce アプリケーションをビルドする](../deployment/building-clickonce-applications-from-the-command-line.md) - .NET Windows プロジェクト用 ClickOnce のクイック スタートを追加
- [フォルダー、IIS、Azure、別の送信先にアプリを展開する](../deployment/deploying-applications-services-and-components-resources.md) - .NET Windows プロジェクト用 ClickOnce のクイック スタートを追加
- [Visual Studio を使用してフォルダーにアプリを配置する](../deployment/quickstart-deploy-to-local-folder.md) - .NET Windows プロジェクト用 ClickOnce のクイック スタートを追加

### <a name="designers"></a>デザイナー

**更新された記事**

- [チュートリアル: Windows フォーム デザイナーを使ってみる](../designers/walkthrough-windows-forms-designer.md) - タイポを修正

### <a name="get-started"></a>作業開始

**更新された記事**

- [プロジェクトとソリューションについて理解する](../get-started/tutorial-projects-solutions.md) - 代替テキストとメタデータを更新、空のソリューション テンプレートに関するメモを追加
- [チュートリアル: リポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo.md) - 新しい Git エクスペリエンスに関するメモと関連項目を追加

### <a name="ide"></a>IDE

**新しい記事**

- [Visual Studio で GitHub アカウントを使用する](./work-with-github-accounts.md) -GitHub の操作のページと、GitHub の他のページへのサインインに関する情報を追加
- [基底クラスを抽出する](./reference/extract-base-class.md) - dotnet の生産性機能を追加
- [インライン メソッド](./reference/inline-method.md) - dotnet の生産性機能を追加
- [クラスを抽象化する](./reference/make-class-abstract.md) - dotnet の生産性機能を追加
- [`new()` を使用する](./reference/use-new.md) - dotnet の生産性機能を追加
- [パターン マッチングを使用する](./reference/use-pattern-matching.md) - dotnet の生産性機能を追加

**更新された記事**

- [Visual Studio での Git エクスペリエンス](../version-control/git-with-visual-studio.md)
  - 代替テキストとメタデータを更新
  - 16.8 GA 用の新しい Git エクスペリエンス コンテンツに更新
- [Visual Studio 2019 の新機能](./whats-new-visual-studio-2019.md)
  - 代替テキストとメタデータを更新
  - 16.8 GA の Visual Studio 2019 ページの新機能を更新
- [チーム エクスプローラーのプロジェクトに接続する](./connect-team-project.md) - 新しい Git エクスペリエンスのメモとリンクでチーム エクスプローラー ページを更新
- [複数のユーザー アカウントを使用する](./work-with-multiple-user-accounts.md) - 他のページへの GitHub のサインインに関する情報を追加
- [C++ EditorConfig の書式規則](./cpp-editorconfig-properties.md)
  - C++ .editorconfig 設定の場合、プレフィックスは cpp_ であり、_cpp_ _ ではありません
  - C++ .editorconfig の例で正しくない文字を削除
- [`typeof` を `nameof` に変換する](./reference/convert-typeof-to-nameof.md) - dotnet の生産性機能を追加

### <a name="install"></a>インストール

**更新された記事**

- [Visual Studio のビルド番号とリリース日](../install/visual-studio-build-numbers-and-release-dates.md)
  - 16.8.2 データを追加
  - 16.8.1 を追加
  - 16.8 GA 以上のビルド番号を更新
- [Azure の Visual Studio イメージ](../install/using-visual-studio-vm.md) - 発行日を変更し、マイナー リビジョン バージョンを更新
- [Visual Studio のワークロードとコンポーネントの ID](../install/workload-and-component-ids.md) - 16.8 のコンポーネントのドキュメントを更新
- [Visual Studio Build Tools のコンポーネント ディレクトリ](../install/workload-component-id-vs-build-tools.md) - 16.8 のコンポーネントのドキュメントを更新
- [Visual Studio Community のコンポーネント ディレクトリ](../install/workload-component-id-vs-community.md) - 16.8 のコンポーネントのドキュメントを更新
- [Visual Studio Enterprise のコンポーネント ディレクトリ](../install/workload-component-id-vs-enterprise.md) - 16.8 のコンポーネントのドキュメントを更新
- [Visual Studio チーム エクスプローラーのコンポーネント ディレクトリ](../install/workload-component-id-vs-team-explorer.md) - 16.8 のコンポーネントのドキュメントを更新
- [Visual Studio テスト エージェントのコンポーネント ディレクトリ](../install/workload-component-id-vs-test-agent.md) - 16.8 のコンポーネントのドキュメントを更新
- [Visual Studio テスト コントローラーのコンポーネント ディレクトリ](../install/workload-component-id-vs-test-controller.md) - 16.8 のコンポーネントのドキュメントを更新
- [ファイアウォールまたはプロキシ サーバーの内側で Visual Studio および Azure Services をインストールして使用する](../install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md) - 不足していたドメインを追加

### <a name="msbuild"></a>MSBuild

**新しい記事**

- [変更ウェーブ](../msbuild/change-waves.md) - MSBuild: 変更ウェーブの新しいトピック

**更新された記事**

- [プロパティ関数](../msbuild/property-functions.md) - リリース 16.8
- [一般的な MSBuild プロジェクト項目](../msbuild/common-msbuild-project-items.md) -InternalsVisibleTo 項目のコンテンツを復元

### <a name="profiling"></a>プロファイル

**更新された記事**

- [コマンド ラインからアプリケーションのパフォーマンスを測定する](../profiling/profile-apps-from-command-line.md) - コマンド ラインからのプロファイリングのドキュメントを更新

### <a name="test"></a>テスト

**更新された記事**

- [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md) - xml 形式のプレイリストに短いセクションを追加
- [Microsoft Fakes でテスト中のコードを分離する](../test/isolating-code-under-test-with-microsoft-fakes.md) - .NET Core サポートで更新されたドキュメント
- [shim を使用して単体テスト用にアプリを分離する](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md) - .NET Core サポートで更新されたドキュメント

### <a name="xaml-tools"></a>XAML ツール

**更新された記事**

- [Visual Studio の XAML デザイナーでデザイン時のデータを使用する](../xaml-tools/xaml-designtime-data.md)
  - 16.8 GA の要件セクションを更新
  - 要件セクションを変更
  - 16.8 プレビュー コメントの更新と GA へのリンク

## <a name="october-2020"></a>2020 年 10 月
### <a name="code-quality"></a>コード品質

**更新された記事**
- [コード アナライザー](../code-quality/index.yml) - .NET 5 用の CA リファクター

### <a name="containers"></a>コンテナー

**更新された記事**

- [クイック スタート: Visual Studio で React シングルページ アプリを含む Docker を使用する](../containers/container-tools-react.md)
  - コンテナー ツール: 古いイメージ リポジトリへの参照を削除
  - .NET 3.1 および VS 16.7 用のコンテナーの React に関するチュートリアルを更新
- [Bridge to Kubernetes のしくみ](../containers/overview-bridge-to-kubernetes.md) - Bridge to Kubernetes: 制限事項を追加
- [ローカルの Docker コンテナーでアプリをデバッグする](../containers/edit-and-refresh.md) - Docker ツールボックス

### <a name="debugger"></a>デバッガー

**新しい記事**

- [Visual Studio での DirectX 12 のサポート](../debugger/graphics/visual-studio-graphics-diagnostics-directx-12.md) - Vsdg dx12

**更新された記事**

- [Visual Studio で ASP.NET または ASP.NET Core アプリをデバッグする](../debugger/how-to-enable-debugging-for-aspnet-applications.md) - GitHub イシューのデバッガー コンテンツの修正
- [Visual Studio デバッガーでブレークポイントを使用する](../debugger/using-breakpoints.md) - GitHub イシューのデバッガー コンテンツの修正
- [Visual Studio で Azure サービスをデバッグする](../debugger/debug-azure-apps.md) - スナップショット デバッガーの SEO とリンクの更新
- [スナップショット デバッガーを使用してライブ ASP.NET Azure アプリをデバッグする](../debugger/debug-live-azure-applications.md) - スナップショット デバッガーの SEO とリンクの更新
- [リモートデバッグ](../debugger/remote-debugging.md) - スナップショットデバッガーの SEO とリンクの更新
- [Visual Studio グラフィックス診断の概要](../debugger/graphics/overview-of-visual-studio-graphics-diagnostics.md) - Vsdg dx12
- [Visual Studio グラフィックス診断](../debugger/graphics/visual-studio-graphics-diagnostics.md) - Vsdg dx12

### <a name="get-started"></a>作業開始

**更新された記事**

- [チュートリアル: シンプルな C# コンソール アプリを拡張する](../get-started/csharp/tutorial-console-part-2.md) - 拡張 C# チュートリアルのデバッグの追加

### <a name="ide"></a>IDE

**新しい記事**

- [Visual Studio 検索を使用する](./visual-studio-search.md) - VS の検索に関するドキュメント

### <a name="install"></a>インストール

**更新された記事**

- [Visual Studio のビルド番号とリリース日](../install/visual-studio-build-numbers-and-release-dates.md)
  - 16.7.7 および 16.8 Preview 6 のデータを追加
  - 16.8 Preview 5 の情報を追加

### <a name="msbuild"></a>MSBuild

**更新された記事**

- [チュートリアル: MSBuild を使用する](../msbuild/walkthrough-using-msbuild.md) - MSBuild チュートリアル: スタンドアロン インストール手順を追加

### <a name="profiling"></a>プロファイル

**更新された記事**

- [メモリ使用量の分析](../profiling/analyze-memory-usage.md)
  - プロファイル用のメモリ使用量の更新 - リンクと説明
  - メモリ使用量ツールの更新
- [パフォーマンス プロファイラーでメモリ使用量をデバッグなしで分析する](../profiling/memory-usage-without-debugging2.md)
  - プロファイル用のメモリ使用量の更新 - リンクと説明
  - メモリ使用量ツールの更新
- [プロファイル ツールの概要](../profiling/profiling-feature-tour.md)
  - プロファイル用のメモリ使用量の更新 - リンクと説明
  - メモリ使用量ツールの更新
- [デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
  - プロファイル用のメモリ使用量の更新 - リンクと説明
  - メモリ使用量ツールの更新
- [パフォーマンス プロファイラーで CPU 使用量をデバッグなしで分析する](../profiling/cpu-usage.md) - メモリ使用量ツールの更新

### <a name="windows"></a>Windows

**更新された記事**

- [Visual Studio のドキュメント | Microsoft Docs](../windows/index.yml) - Windows ハブの更新

### <a name="xaml-tools"></a>XAML ツール

**新しい記事**

- [Visual Studio の XAML デザイナーでデザイン時のデータを使用する](../xaml-tools/xaml-designtime-data.md)
  - XAML デザイン時のドキュメントに拡張セクションを追加しました
  - 新しい XAML デザイン時の記事

## <a name="september-2020"></a>2020 年 9 月
### <a name="code-quality"></a>コード品質

**新しい記事**

- [CA1416:プラットフォームの互換性を検証する](/dotnet/fundamentals/code-analysis/quality-rules/ca1416) - 「CA1416 プラットフォームの互換性を検証する」のドキュメント化
- [CA1834: 1 文字の文字列に対して StringBuilder.Append(char) を使用する](/dotnet/fundamentals/code-analysis/quality-rules/ca1834) - CA1834 のドキュメント

**更新**

- [ソース コード分析の概要](../code-quality/roslyn-analyzers-overview.md) - .NET リファクターのコード分析の更新プログラム
- [コード品質の分析を構成する](../code-quality/use-roslyn-analyzers.md) - .NET リファクターのコード分析の更新プログラム

### <a name="containers"></a>コンテナー

**新しい記事**

- [Bridge to Kubernetes を使用する](../containers/bridge-to-kubernetes.md) - Kubernetes のローカル プロセスが Bridge to Kubernetes にブランド変更
- [Bridge to Kubernetes のしくみ](../containers/overview-bridge-to-kubernetes.md) - Kubernetes のローカル プロセスが Bridge to Kubernetes にブランド変更

### <a name="deployment"></a>デプロイ

**更新された記事**

- [フォルダー、IIS、Azure、または別の場所にアプリを配置する](../deployment/deploying-applications-services-and-components-resources.md) - 配置に関する更新
- [Visual Studio を使用してアプリをフォルダーに配置する](../deployment/quickstart-deploy-to-local-folder.md) - 配置に関する更新

### <a name="ide"></a>IDE

**新しい記事**

- [Visual Studio での新しい Git エクスペリエンス (プレビュー)](../version-control/git-with-visual-studio.md) - 新しい Git エクスペリエンス コンテンツの追加 (プレビュー)
- [C++ EditorConfig の書式規則](./cpp-editorconfig-properties.md) - 新しい記事
- [GitHub Codespaces とは (プレビュー)](./codespaces/codespaces-overview.md) - Codespaces コンテンツの追加 (プレビュー)
- [codespace をカスタマイズする方法 (プレビュー)](./codespaces/customize-codespaces.md) - codespace の (プレビュー) コンテンツの追加
- [サポートされている Visual Studio の機能 (プレビュー)](./codespaces/supported-features-codespaces.md) - codespace の (プレビュー) コンテンツの追加
- [codespace で Visual Studio を使用する方法 (プレビュー)](./codespaces/use-visual-studio-with-codespaces.md) - codespace の (プレビュー) コンテンツの追加

**更新された記事**

- [EditorConfig の .NET コーディング規則の設定](/dotnet/fundamentals/code-analysis/code-style-rule-options) - 更新された EditorConfig
- [言語規則](/dotnet/fundamentals/code-analysis/style-rules/language-rules) - 例がありません

### <a name="install"></a>インストール

**新しい記事**

- [ARM 搭載デバイスの Visual Studio](../install/visual-studio-on-arm-devices.md) - ARM での VS のドキュメントの追加

**更新された記事**

- [Visual Studio をインストールまたは使用するときのネットワーク関連のエラーのトラブルシューティング](../install/troubleshooting-network-related-errors-in-visual-studio.md) - フィードバックされた認証プロキシのクラッシュの回避策を追加

### <a name="profiling"></a>プロファイル

**更新された記事**

- [Visual Studio でのメモリ使用量の測定](../profiling/memory-usage.md) - プロファイリング機能ツアーの更新
- [PerfTips](../profiling/perftips.md) - プロファイリング機能ツアーの更新
- [プロファイリング ツールの概要](../profiling/profiling-feature-tour.md) - プロファイリング機能ツアーの更新
- [デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
  - プロファイリング機能ツアーの更新
  - コンテンツのパフォーマンスの向上

## <a name="august-2020"></a>2020 年 8 月
### <a name="azure"></a>Azure

**新しい記事**

- [Visual Studio 接続済みサービスを使用して Azure Application Insights を追加する](../azure/azure-app-insights-add-connected-service.md) - VS 2019 16.7 の接続済みサービス
- [Visual Studio 接続済みサービスを使用して Azure Cache for Redis を追加する](../azure/azure-cache-for-redis-add-connected-service.md) - VS 2019 16.7 の接続済みサービス
- [Visual Studio 接続済みサービスを使用して Azure Cosmos DB をアプリに追加する](../azure/azure-cosmosdb-add-connected-service.md) - VS 2019 16.7 の接続済みサービス
- [Visual Studio 接続済みサービスを使用して Azure SignalR を追加する](../azure/azure-signalr-add-connected-service.md) - VS 2019 16.7 の接続済みサービス
- [Azure SQL Database への接続を追加する](../azure/azure-sql-database-add-connected-service.md) - VS 2019 16.7 の接続済みサービス

**更新された記事**

- [Visual Studio 接続済みサービスを使用した Azure ストレージの追加](../azure/vs-azure-tools-connected-services-storage.md)
  - VS 2019 16.7 の接続済みサービス
  - Azure Storage 接続済みサービスの記事: UI およびサポートされているプロジェクトの種類の更新

### <a name="code-quality"></a>コード品質

**新しい記事**

- [CA1310: 正確さのために StringComparison を指定する](/dotnet/fundamentals/code-analysis/quality-rules/ca1310) - CA1310 のドキュメントを追加、CA1307 のドキュメントを更新
- [CA1837: Process.GetCurrentProcess().Id の代わりに Environment.ProcessId を使用する](/dotnet/fundamentals/code-analysis/quality-rules/ca1837) - CA1837 のドキュメント
- [CA1838: P/Invoke に対して `StringBuilder` パラメーターを使用しない](/dotnet/fundamentals/code-analysis/quality-rules/ca1838) - CA1838 のドキュメントを追加
- [CA2008: TaskScheduler を渡さずにタスクを作成しない](/dotnet/fundamentals/code-analysis/quality-rules/ca2008) - CA2008 のドキュメントを追加
- [CA2249: String.IndexOf の代わりに String.Contains を使用することを検討する](/dotnet/fundamentals/code-analysis/quality-rules/ca2249) - CA2249 のドキュメント
- [CA2361: DataSet.ReadXml() を含む自動生成クラスが信頼されていないデータで使用されていないことを確認する](/dotnet/fundamentals/code-analysis/quality-rules/ca2361) - DataSet/DataTable の規則の追加
- [CA2362: シリアル化可能な自動生成型の安全でない DataSet または DataTable は、リモート コード実行攻撃に対して脆弱になる可能性がある](/dotnet/fundamentals/code-analysis/quality-rules/ca2362) - DataSet/DataTable の規則の追加
- [IL3000: 単一ファイルとして発行するときにアセンブリ ファイル パスへのアクセスを使用しない](/dotnet/fundamentals/code-analysis/quality-rules/il3000) - IL3000 のドキュメントを追加
- [IL3001: 単一ファイルとして発行するときにアセンブリ ファイル パスにアクセスしない](/dotnet/fundamentals/code-analysis/quality-rules/il3001) - IL3001 のドキュメントを追加

**更新**

- [CA1002: ジェネリック リストを公開しない](/dotnet/fundamentals/code-analysis/quality-rules/ca1002) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1046: 参照型で演算子 equals をオーバーロードしない](/dotnet/fundamentals/code-analysis/quality-rules/ca1046) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1307: 明確化のために StringComparison を指定する](/dotnet/fundamentals/code-analysis/quality-rules/ca1307) - CA1310 のドキュメントを追加、CA1307 のドキュメントを更新
- [CA1700: 列挙型の値に &#39;Reserved&#39; という名前を指定しない](/dotnet/fundamentals/code-analysis/quality-rules/ca1700) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1707: 識別子にアンダースコアを含めることはできない](/dotnet/fundamentals/code-analysis/quality-rules/ca1707) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1822: メンバーを static に設定する](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) - 構成可能な項目の追加 - API サーフェス セクション
- [CA2351:DataSet.ReadXml() の入力が信頼されていることを確認する](/dotnet/fundamentals/code-analysis/quality-rules/ca2351) - DataSet/DataTable の規則の追加
- [サードパーティ製アナライザーのインストール](../code-quality/install-roslyn-analyzers.md) - コード分析のドキュメントの構造とタイトルの変更

### <a name="containers"></a>コンテナー

**更新された記事**

- [Visual Studio を使用して ASP.NET Docker コンテナーをコンテナー レジストリにデプロイする](../containers/hosting-web-apps-in-docker.md) - Visual Studio 16.7 の発行 UI のコンテナー ツールの更新
- [Visual Studio Kubernetes ツールの概要](../containers/bridge-to-kubernetes.md) - Kubernetes チュートリアル: 削除に対する手順の追加

### <a name="deployment"></a>デプロイ

**新しい記事**

- [Visual Studio Installer Projects 拡張機能 と .NET Core 3.1](../deployment/installer-projects-net-core.md) - インストーラー プロジェクトの .NET Core 3.1 の機能に対する新しいヘルプ ページの作成

**更新された記事**

- [フォルダー、IIS、Azure、または別の場所にアプリを配置する](../deployment/deploying-applications-services-and-components-resources.md) - 配置に関する更新
- [Visual Studio での配置](../deployment/index.yml) - 配置に関する更新

### <a name="extensibility"></a>機能拡張

**更新された記事**
- [プロジェクトのサブタイプ](../extensibility/internals/project-subtypes.md) - リスト項目のインデントの修正
- [Visual Studio の色の値の参照](../extensibility/ux-guidelines/color-value-reference-for-visual-studio.md) - 列ヘッダーがない AB#1759333 の修正

### <a name="get-started"></a>作業開始

**更新された記事**

- [手順 5:Azure に ASP.NET Core アプリをデプロイする](../get-started/csharp/tutorial-aspnet-core-ef-step-05.md) - 新しい接続済みサービスの UI に関するビデオ チュートリアルの更新

### <a name="ide"></a>IDE

**新しい記事**

- [Visual Studio の F1 ヘルプ キーを変更する](./not-in-toc/change-f1-help-key.md) - 既定の F1 ヘルプ ページのリファクタリング
- [テキスト エディターの F1 ヘルプ](./not-in-toc/default-f1-text-editor.md) - 既定の F1 ヘルプ ページのリファクタリング
- [`typeof` を `nameof` に変換](./reference/convert-typeof-to-nameof.md) - typeof から nameof への変換のリファクタリング
- [LINQ 式の簡略化](./reference/simplify-linq-expression.md) -LINQ 式簡略化のリファクタリング

**更新された記事**

- [Visual Studio のウィンドウ レイアウトをカスタマイズする](./customizing-window-layouts-in-visual-studio.md) - ウィンドウ レイアウトのカスタマイズに関する記事へのモニカーされた縦型のドキュメント タブの情報の追加
- [Visual Studio または Visual Studio Installer に関する問題を報告する方法](./how-to-report-a-problem-with-visual-studio.md)
  - NMI に詳細情報を追加しました
  - [問題の報告] ページ全体を再作成しました
- [F1 ヘルプ](./not-in-toc/default.md) - 既定の F1 ヘルプ ページのリファクタリング
- [[自動バックアップ] ([オプション] ダイアログ ボックス - [環境])](./reference/autorecover-environment-options-dialog-box.md) - 更新された自動保存ファイルの場所に関する情報の追加
- [[オプション]、[テキスト エディター]、[基本] (Visual Basic)、[詳細]](./reference/options-text-editor-basic-visual-basic.md) - インライン パラメーター名のヒントに関する基本的なドキュメントの追加
- [[オプション]、[テキスト エディター]、[C#]、[詳細]](./reference/options-text-editor-csharp-advanced.md) - インライン パラメーター名のヒントに関する基本的なドキュメントの追加
- [Visual Studio のパフォーマンスのヒントとテクニック](./visual-studio-performance-tips-and-tricks.md) - "マップ モードの無効化" と "右端での折り返しの無効化" の情報の追加
- [Visual Studio 2019 の新機能](./whats-new-visual-studio-2019.md) - 16.7 GA 情報に関する Visual Studio 2019 の新機能の更新

### <a name="rtvs"></a>RTVS

**更新された記事**

- [SQL Server と R の使用](../rtvs/integrating-sql-server-with-r.md) - 列ヘッダーを含むように表を修正

## <a name="july-2020"></a>2020 年 7 月
### <a name="code-quality"></a>コード品質

**新しい記事**

- [CA1417:P/Invoke の文字列パラメーターに `OutAttribute` を使用しない](/dotnet/fundamentals/code-analysis/quality-rules/ca1417) - CA1417 のドキュメントを追加
- [CA1805:不必要に初期化しない。](/dotnet/fundamentals/code-analysis/quality-rules/ca1805) - CA1805 のドキュメントを追加
- [CA1836:使用可能な場合は、Count よりも IsEmpty を優先します](/dotnet/fundamentals/code-analysis/quality-rules/ca1836) - CA1836 の記事を追加 (Count よりも IsEmpty を優先します)
- [CA2016:CancellationToken パラメーターを 1 つのメソッドに転送する](/dotnet/fundamentals/code-analysis/quality-rules/ca2016) - ドキュメント CA2016 - CancellationToken パラメーターを 1 つのメソッドに転送する
- [CA2350:DataTable.ReadXml() の入力が信頼されていることを確認してください](/dotnet/fundamentals/code-analysis/quality-rules/ca2350) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2351:DataSet.ReadXml() の入力が信頼されていることを確認してください](/dotnet/fundamentals/code-analysis/quality-rules/ca2351) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2352:シリアル化可能な型の安全でない DataSet または DataTable は、リモート コード実行攻撃に対して脆弱になる可能性があります](/dotnet/fundamentals/code-analysis/quality-rules/ca2352) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2353:シリアル化可能な型の安全でない DataSet または DataTable](/dotnet/fundamentals/code-analysis/quality-rules/ca2353) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2354:逆シリアル化されたオブジェクト グラフの安全でない DataSet または DataTable は、リモート コード実行攻撃に対して脆弱になる可能性があります](/dotnet/fundamentals/code-analysis/quality-rules/ca2354) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2355:逆シリアル化されたオブジェクト グラフの安全でない DataSet または DataTable](/dotnet/fundamentals/code-analysis/quality-rules/ca2355) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント
- [CA2356:Web の逆シリアル化されたオブジェクト グラフの安全でない DataSet または DataTable 型](/dotnet/fundamentals/code-analysis/quality-rules/ca2356) - DataSet または DataTable の初期逆シリアル化規則に関するドキュメント

### <a name="containers"></a>コンテナー

**新しい記事**

- [Local Process with Kubernetes を構成する](../containers/configure-bridge-to-kubernetes.md) - Local Process with Kubernetes: yaml の構成
- [Local Process with Kubernetes (プレビュー) の使用](../containers/bridge-to-kubernetes.md) - 開発スペースの移行
- [Local Process with Kubernetes のしくみ](../containers/overview-bridge-to-kubernetes.md)
  - Local Process for Kubernetes:ルーティング セクションの追加
  - 開発スペースの移行

### <a name="cross-platform"></a>クロス プラットフォーム

**更新された記事**

- [変更ログ (Visual Studio Tools for Unity、Windows)](/gamedev/unity/change-log-visual-studio-tools-for-unity.md) - Bump VSTU 変更ログ 4.7.1.0
- [変更ログ (Visual Studio Tools for Unity、Mac)](/gamedev/unity/change-log-visual-studio-tools-for-unity-mac.md) - Bump VSTUM 変更ログ 2.7.1.0

### <a name="get-started"></a>はじめに

**新しい記事**

- [チュートリアル: シンプルな C# コンソール アプリを拡張する](../get-started/csharp/tutorial-console-part-2.md) - 拡張路上チュートリアルの最初のバージョンをリリース

### <a name="ide"></a>IDE

**新しい記事**

- [Developer Community のガイドライン](./developer-community-guidelines.md) - DevCom ガイドラインを追加
- [インポートされていない型と拡張メソッドに対する IntelliSense 入力候補](./reference/intellisense-completion-unimported-types-extension-methods.md)

### <a name="install"></a>インストール

**新しい記事**

- [最小限のオフライン レイアウトを使用して Visual Studio を更新する](../install/update-minimal-layout.md) - 最小限のレイアウト機能に関するドキュメント
- [Visual Studio 企業向けガイド](../install/visual-studio-enterprise-guide.md) - 企業向けガイド

### <a name="javascript"></a>JavaScript

**新しい記事**

- [TypeScript コードのコンパイル (Node.js)](../javascript/compile-typescript-code-npm.md) - TypeScript のコンパイルとビルド
- [TypeScript コードのコンパイル (ASP.NET Core)](../javascript/compile-typescript-code-nuget.md) - TypeScript のコンパイルとビルド

### <a name="msbuild"></a>MSBuild

**新しい記事**

- [一般的な MSBuild 項目メタデータ](../msbuild/common-msbuild-item-metadata.md) - MSBuild: Link と LinkBase の省略可能なメタデータに関する表を追加
- [MSBuild でのソリューション フィルター](../msbuild/solution-filters.md) - MSBuild のソリューション フィルター

### <a name="test"></a>テスト

**新しい記事**

- [テスト エクスプローラーを使用した単体テストのデバッグと分析](../test/debug-unit-tests-with-test-explorer.md) - テスト エクスプローラーのパフォーマンス作業

**更新された記事**

- [ *.runsettings* ファイルを使用して単体テストを構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
  - runsettings ファイルを使用した単体テストの構成に関する更新
  - Blame オプションの説明が変更され、例が追加されました。