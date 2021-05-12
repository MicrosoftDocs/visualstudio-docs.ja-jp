---
title: スナップショットのデバッグに関するトラブルシューティング | Microsoft Docs
description: Visual Studio でのスナップショットのデバッグに関するトラブルシューティングと既知の問題について説明します。 実稼働サイトでダウンタイムを引き起こすことなく ICorProfiler を読み込みます。
ms.custom: SEO-VS-2020
ms.date: 04/24/2019
ms.topic: troubleshooting
helpviewer_keywords:
- debugger
ms.assetid: 511a0697-c68a-4988-9e29-8d0166ca044a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aad883ac0c3f703b2d6a4e10d3a0ef2468cd8465
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798441"
---
# <a name="troubleshooting-and-known-issues-for-snapshot-debugging-in-visual-studio"></a>Visual Studio でのスナップショットのデバッグに関するトラブルシューティングと既知の問題

この記事で説明されている手順を実行しても問題が解決しない場合は、[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)で問題を検索するか、Visual Studio で **[ヘルプ]**  >  **[フィードバックの送信]**  >  **[問題の報告]** を選択して新しい問題を報告してください。

## <a name="issue-attach-snapshot-debugger-encounters-an-http-status-code-error"></a>問題:[スナップショット デバッガーのアタッチ] で HTTP 状態コード エラーが発生する

アタッチしようとしたときに **[出力]** ウィンドウに次のエラーが表示される場合は、後述する既知の問題である可能性があります。 提案された解決策を試してください。問題が解決しない場合は、前述のエイリアスに問い合わせてください。

`[TIMESTAMP] Error --- Unable to Start Snapshot Debugger - Attach Snapshot Debugger failed: System.Net.WebException: The remote server returned an error: (###) XXXXXX`

### <a name="401-unauthorized"></a>(401) 許可されていません

このエラーは、Visual Studio から Azure に発行された REST 呼び出しに無効な資格情報が使用されていることを示しています。 

次の手順を実行します。

* Visual Studio 個人アカウントに、アタッチしている Azure サブスクリプションとリソースへのアクセス許可があることを確認します。 これを簡単に確認するには、 **[デバッグ]**  >  **[スナップショット デバッガーのアタッチ]**  >  **[Azure Resource]**  >  **[既存のものを選択]** のダイアログ ボックス、または Cloud Explorer でリソースを使用できるかどうかを確認します。
* このエラーが引き続き発生する場合は、この記事の冒頭で説明したフィードバック チャネルのいずれかを使用します。

App Service で認証/承認 (EasyAuth) を有効にした場合、呼び出し履歴エラーメッセージで LaunchAgentAsync の 401 エラーが発生することがあります。 Azure portal で **[要求が認証されない場合に実行するアクション]** が **[匿名要求を許可する (操作不要)]** に設定されていることを確認し、代わりに D:\Home\sites\wwwroot で以下の内容の authorization.json を指定します。 

```
{
  "routes": [
    {
      "path_prefix": "/",
      "policies": {
        "unauthenticated_action": "RedirectToLoginPage"
      }
    },
    {
      "http_methods": [ "POST" ],
      "path_prefix": "/41C07CED-2E08-4609-9D9F-882468261608/api/agent",
      "policies": {
        "unauthenticated_action": "AllowAnonymous"
      }
    }
  ]
}
```

最初の route は、 **[[ID プロバイダー] でのログイン]** と同様にアプリドメインを効果的に保護します。 2 番目の route は、認証の外部で SnapshotDebugger AgentLaunch エンドポイントを公開し、SnapshotDebugger のプレインストールされたサイト拡張機能がアプリサービスに対して有効になっている *場合にのみ*、事前定義済みの SnapshotDebugger 診断エージェント開始アクションを実行します。 authorization. json 構成の詳細については、[URL 承認規則に関する記事](https://azure.github.io/AppService/2016/11/17/URL-Authorization-Rules.html)を参照してください。

### <a name="403-forbidden"></a>(403) 禁止されています

このエラーは、アクセス許可が拒否されたことを示しています。 これは、さまざまな問題が原因で発生する可能性があります。

次の手順を実行します。

* Visual Studio アカウントに、リソースに必要なロールベースのアクセス制御 (RBAC) アクセス許可を持つ有効な Azure サブスクリプションがあることを確認します。 AppService の場合は、アプリをホストする App Service プランの[クエリ](/rest/api/appservice/appserviceplans/get)を実行するアクセス許可があるかどうかを確認します。
* クライアント マシンのタイムスタンプが正しく、最新であることを確認します。 通常、要求のタイムスタンプからのずれが 15 分を超えるタイムスタンプのサーバーでこのエラーが発生します。
* このエラーが引き続き発生する場合は、この記事の冒頭で説明したフィードバック チャネルのいずれかを使用します。

### <a name="404-not-found"></a>(404) 見つかりません

このエラーは、Web サイトがサーバー上に見つからなかったことを示します。

次の手順を実行します。

* アタッチする App Service リソース上に Web サイトが配置され、実行されていることを確認します。
* https://\<resource\>.azurewebsites.net でサイトを使用できることを確認します
* https://\<resource\>.azurewebsites.net にアクセスしたときに、適切に実行されているカスタム Web アプリケーションから状態コード 404 が返されないことを確認します
* このエラーが引き続き発生する場合は、この記事の冒頭で説明したフィードバック チャネルのいずれかを使用します。

### <a name="406-not-acceptable"></a>(406) 受容不可

このエラーは、サーバーでは要求の Accept ヘッダーに設定されている種類に応答できないことを示しています。

次の手順を実行します。

* https://\<resource\>.azurewebsites.net でサイトを使用できることを確認します
* サイトが新しいインスタンスに移行していないことを確認します。 スナップショット デバッガーでは、ARRAffinity の概念を使用して、このエラーが断続的に生成される可能性がある特定のインスタンスに要求をルーティングします。
* このエラーが引き続き発生する場合は、この記事の冒頭で説明したフィードバック チャネルのいずれかを使用します。

### <a name="409-conflict"></a>(409) 競合

このエラーは、要求が現在のサーバーの状態と競合していることを示しています。

これは、ApplicationInsights が有効な AppService に対して、ユーザーがスナップショット デバッガーをアタッチしようとしたときに発生する既知の問題です。 ApplicationInsights では、Visual Studio とは異なる大文字と小文字の指定で AppSettings が設定されるため、この問題が発生します。

::: moniker range=">= vs-2019"
これは Visual Studio 2019 で解決されました。
::: moniker-end

次の手順を実行します。

::: moniker range="vs-2017"

* Azure portal で、SnapshotDebugger (SNAPSHOTDEBUGGER_EXTENSION_VERSION) と InstrumentationEngine (INSTRUMENTATIONENGINE_EXTENSION_VERSION) の AppSettings が大文字であることを確認します。 そうでない場合は、手動で設定を更新し、サイトを強制的に再起動します。
::: moniker-end
* このエラーが引き続き発生する場合は、この記事の冒頭で説明したフィードバック チャネルのいずれかを使用します。

### <a name="500-internal-server-error"></a>(500) 内部サーバー エラー

このエラーは、サイトが完全にダウンしているか、サーバーで要求を処理できないことを示しています。 スナップショット デバッガーは、実行中のアプリケーションでのみ機能します。 [Application Insights スナップショット デバッガー](/azure/azure-monitor/app/snapshot-debugger)には例外に対してスナップショットを作成する機能があり、ニーズに最適なツールとなる場合があります。

### <a name="502-bad-gateway"></a>(502) 無効なゲートウェイ

このエラーはサーバー側のネットワークの問題を示しており、一時的なものである可能性があります。

次の手順を実行します。

* 数分待ってから、スナップショット デバッガーを再アタッチしてみてください。
* このエラーが引き続き発生する場合は、この記事の冒頭で説明したフィードバック チャネルのいずれかを使用します。

## <a name="issue-snappoint-does-not-turn-on"></a>問題:スナップポイントが有効にならない

通常のスナップ アイコンではなく、![スナップポイントの警告アイコン](../debugger/media/snapshot-troubleshooting-snappoint-warning-icon.png "スナップポイント警告アイコン")がスナップポイントに表示される場合、スナップポイントは有効ではありません。

![スナップポイントが有効にならない](../debugger/media/snapshot-troubleshooting-dont-turn-on.png "スナップポイントが有効にならない")

次の手順を実行します。

1. アプリのビルドと配置に使用したものと同じバージョンのソース コードがあることを確認します。 配置の正しいシンボルを読み込んでいることを確認します。 これを行うには、スナップショットのデバッグ中に **[モジュール]** ウィンドウを表示し、デバッグ対象のモジュール用に読み込まれた .pdb ファイルが [シンボル ファイル] 列に表示されることを確認します。 スナップショット デバッガーは、配置用のシンボルを自動的にダウンロードして使用しようとします。

## <a name="issue-symbols-do-not-load-when-i-open-a-snapshot"></a>問題:スナップショットを開いてもシンボルが読み込まれない

次のウィンドウが表示される場合、シンボルは読み込まれていません。

![シンボルが読み込まれない](../debugger/media/snapshot-troubleshooting-symbols-wont-load.png "シンボルが読み込まれない")

次の手順を実行します。

- このページの **[シンボルの設定の変更]** リンクをクリックします。 **[デバッグ] > [シンボル]** 設定で、シンボルのキャッシュ ディレクトリを追加します。 シンボルのパスを設定したら、スナップショットのデバッグを再開します。

   プロジェクトで使用できるシンボル、または .pdb ファイルは、App Service の配置と一致する必要があります。 ほとんどの配置 (Visual Studio、Azure Pipelines または Kudu を含む CI/CD などによる配置) は、シンボル ファイルを App Service に発行します。 シンボルのキャッシュ ディレクトリを設定すると、Visual Studio でそのシンボルを使用できるようになります。

   ![シンボルの設定](../debugger/media/snapshot-troubleshooting-symbol-settings.png "シンボルの設定")

- また、組織がシンボル サーバーを使用している場合、または別のパスにあるシンボルをドロップする場合は、シンボル設定を使用して配置の正しいシンボルを読み込みます。

## <a name="issue-i-cannot-see-the-attach-snapshot-debugger-option-in-the-cloud-explorer"></a>問題:Cloud Explorer に [スナップショット デバッガーのアタッチ] オプションが表示されない

次の手順を実行します。

- スナップショット デバッガー コンポーネントがインストールされていることを確認します。 Visual Studio インストーラーを開き、Azure ワークロードの **スナップショット デバッガー** コンポーネントをオンにします。
::: moniker range="< vs-2019"
- アプリがサポートされていることを確認します。 現在、Azure App Service にデプロイされている ASP.NET (4.6.1 以降) と ASP.NET Core (2.0 以降) のアプリケーションのみがサポートされています。
::: moniker-end
::: moniker range=">= vs-2019"
- アプリがサポートされていることを確認します。
  - Azure App Service - .NET Framework 4.6.1 以降で実行されている ASP.NET アプリケーション。
  - Azure App Service - Windows の .NET Core 2.0 以降で実行されている ASP.NET Core アプリケーション。
  - Azure Virtual Machines (および仮想マシン スケール セット) - .NET Framework 4.6.1 以降で実行されている ASP.NET アプリケーション。
  - Azure Virtual Machines (および仮想マシン スケール セット) - Windows 上の .NET Core 2.0 以降で実行されている ASP.NET Core アプリケーション。
  - Azure Kubernetes Service - Debian 9 上の .NET Core 2.2 以降で実行されている ASP.NET Core アプリケーション。
  - Azure Kubernetes Service - Alpine 3.8 上の .NET Core 2.2 以降で実行されている ASP.NET Core アプリケーション。
  - Azure Kubernetes Service - Ubuntu 18.04 上の .NET Core 2.2 以降で実行されている ASP.NET Core アプリケーション。
::: moniker-end

## <a name="issue-i-only-see-throttled-snapshots-in-the-diagnostic-tools"></a>問題:診断ツールに調整されたスナップショットのみが表示される

![調整されたスナップポイント](../debugger/media/snapshot-troubleshooting-throttled-snapshots.png "調整されたスナップポイント")

次の手順を実行します。

- スナップショットはほとんどメモリを占有しませんが、コミット チャージがかかります。 スナップショット デバッガーで、サーバーに大きなメモリ負荷がかかっていることが検出された場合は、スナップショットが取得されません。 既にキャプチャされたスナップショットを削除するには、スナップショット デバッガー セッションを停止して再試行します。

::: moniker range=">= vs-2019"
## <a name="issue-snapshot-debugging-with-multiple-versions-of-the-visual-studio-gives-me-errors"></a>問題:複数のバージョンの Visual Studio でスナップショットをデバッグするとエラーが発生する

Visual Studio 2019 では、Azure App Service 上に新しいバージョンのスナップショット デバッガー サイト拡張機能が必要です。  このバージョンは、Visual Studio 2017 で使用されている古いバージョンのスナップショット デバッガー サイト拡張機能と互換性がありません。  Visual Studio 2019 のスナップショット デバッガーを、Visual Studio 2017 のスナップショット デバッガーによって以前にデバッグされた Azure App Service にアタッチしようとすると、次のエラーが発生します。

![互換性のないスナップショット デバッガー サイト拡張機能 Visual Studio 2019](../debugger/media/snapshot-troubleshooting-incompatible-vs2019.png "互換性のないスナップショット デバッガー サイト拡張機能 Visual Studio 2019")

逆に、Visual Studio 2019 のスナップショット デバッガーによって以前にデバッグされた Azure App Service に、Visual Studio 2017 を使用してスナップショット デバッガーをアタッチすると、次のエラーが発生します。

![互換性のないスナップショット デバッガー サイト拡張機能 Visual Studio 2017](../debugger/media/snapshot-troubleshooting-incompatible-vs2017.png "互換性のないスナップショット デバッガー サイト拡張機能 Visual Studio 2017")

これを修正するには、Azure portal で次のアプリ設定を削除し、スナップショット デバッガーを再度アタッチします。

- INSTRUMENTATIONENGINE_EXTENSION_VERSION
- SNAPSHOTDEBUGGER_EXTENSION_VERSION
::: moniker-end

## <a name="issue-i-am-having-problems-snapshot-debugging-and-i-need-to-enable-more-logging"></a>問題:スナップショットのデバッグに問題があり、さらに多くのログを有効にする必要がある

### <a name="enable-agent-logs"></a>エージェント ログを有効にする

エージェント ログを有効または無効にするには、Visual Studio を開き、 *[ツール] > [オプション] > [スナップショット デバッガー] > [エージェント ログを有効にする]* に移動します。 *[セッションの開始時に古いエージェント ログを削除する]* も有効な場合、Visual Studio のアタッチが成功するたびに以前のエージェント ログは削除される点に注意してください。

エージェント ログは次の場所にあります。

- App Service:
  - App Service の Kudu サイト (つまり yourappservice.**scm**.azurewebsites.net) にアクセスし、[デバッグ コンソール] に移動します。
  - エージェントのログは、次のディレクトリに格納されます。D:\home\LogFiles\SiteExtensions\DiagnosticsAgentLogs\
- VM/VMSS:
  - VM にサインインすると、エージェントのログは次のように格納されます。C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<Version>\SnapshotDebuggerAgent_*.txt
- AKS
  - /tmp/diag/AgentLogs/* ディレクトリに移動します

### <a name="enable-profilerinstrumentation-logs"></a>プロファイラー/インストルメンテーション ログを有効にする

インストルメンテーション ログは次の場所にあります。

- App Service:
  - エラー ログは D:\Home\LogFiles\eventlog.xml に自動的に送信され、イベントは `<Provider Name="Instrumentation Engine" />` または "運用ブレークポイント" を使用してマークされます。
- VM/VMSS:
  - VM にサインインし、イベント ビューアーを開きます。
  - 次のビューを開きます。 *[Windows ログ] > [アプリケーション]* 。
  - *[Production Breakpoints]\(運用ブレークポイント\)* または *[インストルメンテーション エンジン]* を使用して、 *[イベント ソース]* で *[現在のログをフィルター]* を実行します。
- AKS
  - /tmp/diag/log.txt のインストルメンテーション エンジン ログ (DockerFile で MicrosoftInstrumentationEngine_FileLogPath を設定します)
  - /tmp/diag/shLog.txt の ProductionBreakpoint ログ

## <a name="known-issues"></a>既知の問題

- 同じ App Service に対する複数の Visual Studio クライアントを使用したスナップショットのデバッグは、現在サポートされていません。
- Roslyn IL の最適化は、ASP.NET Core プロジェクトでは完全にはサポートされていません。 一部の ASP.NET Core プロジェクトには、表示されない変数や、条件付きステートメントに使用できない変数があります。
- *$FUNCTION* や *$CALLER* などの特殊な変数は、ASP.NET Core プロジェクトの条件付きステートメントやログポイントで評価できません。
- スナップショットのデバッグは、[ローカル キャッシュ](/azure/app-service/app-service-local-cache)が有効な App Service では機能しません。
- スナップショット デバッグ API アプリは現在サポートされていません。

## <a name="site-extension-upgrade"></a>サイト拡張機能のアップグレード

スナップショットのデバッグと Application Insights は ICorProfiler に依存しています。ICorProfiler はサイト プロセスに読み込まれ、アップグレード中にファイル ロックの問題を引き起こします。 このプロセスで運用サイトにダウンタイムが発生しないようにすることをお勧めします。

- App Service 内に[デプロイ スロット](/azure/app-service/web-sites-staged-publishing)を作成し、サイトをスロットにデプロイします。
- Visual Studio の Cloud Explorer または Azure portal から、スロットを運用とスワップします。
- スロット サイトを停止します。 すべてのインスタンスからサイトの w3wp.exe プロセスを終了するため、この処理には数秒かかります。
- Kudu サイトまたは Azure portal からスロット サイト拡張機能をアップグレードします ( *[App Service] ブレード > [開発ツール] > [拡張機能] > [更新]* )。
- スロット サイトを起動します。 もう一度ウォームアップするために、このサイトにアクセスすることをお勧めします。
- スロットを運用とスワップします。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデバッグ](../debugger/index.yml)
- [スナップショット デバッガーを使用してライブ ASP.NET アプリをデバッグする](../debugger/debug-live-azure-applications.md)
- [スナップショット デバッガーを使用して、Azure Virtual Machines と Azure Virtual Machine Scale Sets 上のライブ ASP.NET アプリをデバッグする](../debugger/debug-live-azure-virtual-machines.md)
- [スナップショット デバッガーを使用してライブ ASP.NET Azure Kubernetes をデバッグする](../debugger/debug-live-azure-kubernetes.md)
- [スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.yml)
