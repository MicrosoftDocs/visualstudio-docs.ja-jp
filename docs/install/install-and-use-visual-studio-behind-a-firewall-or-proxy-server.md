---
title: ファイアウォールまたはプロキシ サーバーの内側にインストールして使用する
description: ファイアウォールまたはプロキシ サーバーを使用する場合に、許可リストに追加したり、開いたりすることがあるドメイン URL、ポート、プロトコルを確認します
ms.date: 06/17/2020
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
- list of domains, locations, URLs
ms.assetid: ''
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 44af5c5a00e1ca26eb545b0973090486f6d320ea
ms.sourcegitcommit: 99b66b0f4ced46ead0b2506a103f974f40cc0076
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2021
ms.locfileid: "103295705"
---
# <a name="install-and-use-visual-studio-and-azure-services-behind-a-firewall-or-proxy-server"></a>ファイアウォールまたはプロキシ サーバーの内側に Visual Studio および Azure Services をインストールして使用する

ユーザーまたはユーザーの組織でファイアウォールやプロキシ サーバーなどのセキュリティ対策を取っている場合は、Visual Studio および Azure Services をインストールして使用するときに最適なエクスペリエンスを得るために、"許可リスト" への追加をお勧めするドメイン URL および開くことをお勧めするポートおよびプロトコルがあります。

* **[Visual Studio のインストール](#install-visual-studio)** :これらの表には、目的とするすべてのコンポーネントおよびワークロードにアクセスできるようにするために、許可リストに追加すべきドメイン URL を示します。

* **[Visual Studio および Azure Services の使用](#use-visual-studio-and-azure-services)** :この表には、目的とするすべての機能とサービスにアクセスできるようにするために、許可リストに追加すべきドメイン URL と、開くべきポートおよびプロトコルを示します。

> [!NOTE]
> この記事は Windows 上の Visual Studio 向けに書かれていますが、一部の情報はファイアウォールやプロキシ サーバーの背後に [Visual Studio for Mac をインストール](/visualstudio/mac/install-behind-a-firewall-or-proxy-server)する場合にも適用されます。

## <a name="install-visual-studio"></a>Visual Studio のインストール

### <a name="urls-to-add-to-an-allow-list"></a>許可リストに追加する URL

Visual Studio インストーラーによって、さまざまなドメインやダウンロード サーバーからファイルがダウンロードされます。このため、UI または配置スクリプトで信頼されているものとして許可リストに追加することをお勧めするドメイン URL を次に示します。

#### <a name="microsoft-domains"></a>Microsoft ドメイン

| ドメイン | 目的 |
| - | - |
| go.microsoft.com | URL の解像度を設定する |
| aka.ms | URL の解像度を設定する |
| download.visualstudio.microsoft.com | パッケージのダウンロード場所を設定する |
| download.microsoft.com | パッケージのダウンロード場所を設定する |
| download.visualstudio.com | パッケージのダウンロード場所を設定する |
| dl.xamarin.com | パッケージのダウンロード場所を設定する |
| xamarin-downloads.azureedge.net | Android SDK パッケージのダウンロード リストの場所 |
| marketplace.visualstudio.com | Visual Studio 拡張機能のダウンロード場所 |
| \*.gallerycdn.vsassets.io  | Visual Studio 拡張機能のダウンロード場所 |
| visualstudio.microsoft.com | ドキュメントの場所 |
| docs.microsoft.com | ドキュメントの場所 |
| msdn.microsoft.com | ドキュメントの場所 |
| www\.microsoft.com | ドキュメントの場所 |
| \*.windows.net | サインインの場所 |
| \*.microsoftonline.com | サインインの場所 |
| \*.live.com | サインインの場所 |
| | |

#### <a name="non-microsoft-domains"></a>Microsoft 以外のドメイン

| ドメイン | 以下のワークロードをインストールします。 |
| - | - |
| archive.apache.org | JavaScript でのモバイル開発 (Cordova) |
| cocos2d-x.org | C++ によるゲーム開発 (Cocos) |
| download.epicgames.com | C++ によるゲーム開発 (Unreal Engine) |
| download.oracle.com | JavaScript でのモバイル開発 (Java SDK) <br /><br />.NET によるモバイル開発 (Java SDK) |
| download.unity3d.com | Unity でのゲーム開発 (Unity) |
| netstorage.unity3d.com | Unity でのゲーム開発 (Unity) |
| dl.google.com | JavaScript によるモバイル開発 (Android SDK および NDK、エミュレーター) <br /><br />.NET によるモバイル開発 (Android SDK および NDK、エミュレーター) |
| www\.incredibuild.com | C++ によるゲーム開発 (IncrediBuild) |
| incredibuildvs2017i.azureedge.net | C++ によるゲーム開発 (IncrediBuild) |
| www\.python.org | Python 開発 (Python) <br /><br />データ サイエンスと分析のアプリケーション (Python) |
| developerservices2.apple.com | Xamarin.iOS provisioning |
| developer.apple.com | Xamarin.iOS provisioning |
| appstoreconnect.apple.com | Xamarin.iOS provisioning |
| idmsa.apple.com | Xamarin.iOS provisioning |
| akamized.net | Content Delivery Network (Akamai Technologies) |
| | |

## <a name="use-visual-studio-and-azure-services"></a>Visual Studio および Azure Services の使用

### <a name="urls-to-add-to-an-allow-list-and-ports-and-protocols-to-open"></a>許可リストに追加すべき URL と開くべきポートおよびプロトコル

ここでは、ファイアウォールまたはプロキシ サーバーの内側で Visual Studio または Azure サービスを使用するときに必要なものすべてにアクセスできるようにするために、許可リストに追加すべき URL と、開くことをお勧めするポートおよびプロトコルを示します。

| サービスまたはシナリオ | DNS エンドポイント | プロトコル<br/>/ポート | 説明 |
| - | - | -: | - | - |
| URL<br>解決 | go.microsoft.com<br><br>aka.ms | | URL を短くするために使用されます。後で長い URL に解決されます。 |
| スタート ページ | vsstartpage.blob.core.windows.net | 443 | スタート ページに示される開発者向けニュースを表示するために使用されます (Visual Studio 2017 のみ) |
| 対象の<br> 通知 <br>サービス | targetednotifications-tm.trafficmanager.net <br><br>www.research.net | 443<br><br>443 | 通知のグローバル リストを、特定の種類のコンピューター/使用状況シナリオにのみ適用されるリストへとフィルター処理するために使用されます。 |
| 拡張子 <br>更新チェック | marketplace.visualstudio.com<br><br>&#42;.windows.net <br>&#42;.microsoftonline.com <br>&#42;.live.com | 443 | インストールした拡張機能の更新プログラムが利用可能になったときに通知を提供するために使用されます。 <br><br> サインインの場所として使用されます。 |
| AI プロジェクト <br>統合 | az861674.vo.msecnd.net | 443<br> | 登録されている Application Insights アカウントに使用状況データを送信する新しいプロジェクトを構成するために使用されます。 |
| コード レンズ | codelensprodscus1su0.app.<br>codelens.visualstudio.com | 443 | ファイルの最終更新日時、変更のタイムライン、変更が関連付けられている作業項目、作成者など、エディター内に情報を提供するために使用されます。 |
| 実験用 <br>機能の有効化 | visualstudio-devdiv-c2s.msedge.net | 80 | 実験用の新しい機能や機能の変更をアクティブ化するために使用されます。 |
| 識別情報 "バッジ" <br>(ユーザー名とアバター)<br>and <br>ローミング設定 | app.vssps.visualstudio.com <br><br>app.vsspsext.visualstudio.com<br><br>app.vssps.visualstudio.com<br><br> ns-sb2-prod-ch1-002.cloudapp.net <br><br>az700632.vo.msecnd.net<br><br>api.vstsusers.visualstudio.com/profiles/* | 443 | IDE でユーザーの名前とアバターを表示するために使用されます。 <br><br> あるコンピューターから別のコンピューターに設定の変更が確実にローミングするように使用されます。 |
| リモート設定 | az700632.vo.msecnd.net | 443 | Visual Studio で問題を引き起こすことがわかっている拡張機能をオフにするために使用されます。 |
| Windows ツール | developer.microsoft.com <br><br>dev.windows.com  <br><br>appdev.microsoft.com | https/443 | Windows アプリ ストアのシナリオで使用されます。 |
| JSON スキーマ <br>探索 <br><br>JSON スキーマ <br>定義<br><br>JSON スキーマ <br>サポート <br>Azure リソース | json.schemastore.org <br>schemastoreorg.azurewebsites.net<br><br>json-schema.org<br><br>schema.management.azure.com | http/80<br>https/443<br><br>http/80<br><br>https/443 | JSON ドキュメントの編集時にユーザーによって使用される可能性のある JSON スキーマを検出およびダウンロードするために使用されます。 <br><br>Json 用のメタ検証スキーマを取得するために使用されます。<br><br>Azure Resource Manager 展開テンプレート用の現在のスキーマを取得するために使用されます。 |
| NPM パッケージ <br>探索 | Skimdb.npmjs.com <br><br>Registry.npmjs.org <br><br>Api.npms.io | https/443<br><br>http/80 &<br> https/443<br>https/443 | NPM パッケージを検索する場合に必要であり、Web プロジェクトでのクライアント側スクリプト パッケージのインストールに使用されます。 |
| Bower パッケージ<br> アイコン<br><br>Bower パッケージ <br>search | Bower.io <br><br>bowercache.azurewebsites.net <br>go.microsoft.com <br>Registry.bower.io | http/80<br><br>https/443<br>http/80<br>https/443 | 既定の Bower パッケージ アイコンを指定します。  <br><br>Bower パッケージを検索する機能を提供します。 |
| NuGet<br><br>NuGet パッケージ<br> 探索 | api.nuget.org <br>www.nuget.org <br>nuget.org <br>azuresearch-usnc.nuget.org <br>azuresearch-ussc.nuget.org <br>licenses.nuget.org <br>nuget.cdn.azure.cn <br>azuresearch-ea.nuget.org <br>azuresearch-sea.nuget.org <br><br>crl3.digicert.com <br>crl4.digicert.com <br>ocsp.digicert.com <br>cacerts.digicert.com | https/443<br><br>http/80 &<br>https/443<br> | 署名された NuGet パッケージを確認するために使用されます。<br><br>NuGet パッケージおよびバージョンを検索するために必要です。 |
| GitHub リポジトリの情報 | api.github.com | https/443 | Bower パッケージに関する追加情報を取得するために必要です。 |
| Web リンター | Eslint.org<br><br>www.Bing.com <br><br>www.coffeelint.org | http/80 | |
| Cookiecutter<br>エクスプローラー テンプレート<br>探索 <br><br>Cookiecutter <br>エクスプローラー プロジェクトの<br> 作成 | api.github.com <br>raw.githubusercontent.com <br>go.microsoft.com<br><br>pypi.org <br> pypi.python.org | https/443<br> | 推奨されるフィードから、および GitHub リポジトリから、オンライン テンプレートを検出するために使用されます <br><br>Python パッケージ インデックス (PyPI) からの cookiecutter Python パッケージの 1 回限りのオンデマンド インストールを必要とする cookiecutter テンプレートからプロジェクトを作成するために使用されます。 |
| Python パッケージ <br>探索<br><br>Python パッケージ <br>管理<br><br>新規作成 <br>Python <br> プロジェクト <br>テンプレートの使用 | pypi.org<br> <br>pypi.python.org <br>bootstrap.pypa.io<br><br>go.microsoft.com | https/443 | pip パッケージを検索する機能を提供します。<br><br>pip が存在しない場合に、pip を自動的にインストールするために使用されます。 <br><br>次の新しい Python プロジェクト テンプレートを cookiecutter テンプレート URL に解決するために使用されます。<br> - 分類子プロジェクト<br>- クラスタリング プロジェクト <br> - 回帰プロジェクト <br> - PyKinect を使用した PyGame <br> - Pyvot プロジェクト |
| Office Web <br>アドイン <br> file:/// <br>検証 <br>サービス | verificationservice.osi.office.net | https/443 | Office Web アドインのマニフェストを検証するために使用されます。 |
| SharePoint と <br>Office アドイン | sharepoint.com<br> microsoft.com/microsoft-365<br> microsoftonline.com <br> outlook.com | https/443 | SharePoint および Office のアドインを SharePoint Online および Microsoft 365 に発行し、テストするために使用されます |
| ワークフロー マネージャー <br>テスト サービス<br> Host | | http/12292 | SharePoint アドインをワークフローでテストするために自動的に作成されるファイアウォール規則です。 |
| 自動的に収集される <br>信頼性の統計情報 <br>と、 <br>Azure SDK および SQL Tools 用の <br>その他の<br> カスタマー エクスペリエンス向上プログラム <br>(CEIP) <br><br> | vortex.data.microsoft.com<br> <br>dc.services.visualstudio.com | https/443 | ユーザーから Microsoft に信頼性の統計情報 (クラッシュまたは無応答データ) を送信するために使用されます。 Windows エラー報告を有効にした場合、実際のクラッシュまたは無応答ダンプは引き続きアップロードされ、統計情報のみが抑制されます。 <br>Azure Tools SDK 拡張機能の匿名の利用状況パターン、および SQL ツールの利用状況パターンを Visual Studio に対して明らかにします。 |
| Visual Studio <br> カスタマー エクスペリエンス <br>向上プログラム (CEIP) <br><br>PerfWatson.exe | vortex.data.microsoft.com<br>dc.services.visualstudio.com<br>visualstudio-devdiv-c2s.msedge.net<br>az667904.vo.msecnd.net <br>scus-breeziest-in.cloudapp.net<br> | https/443 | 匿名の利用状況のパターンとエラー ログを収集するために使用されます。 <br><br>UI のフリーズ問題を追跡するために使用されます。 |
| Azure リソースの<br>作成と <br>管理 | management.azure.com <br>management.core.windows.net | https/443 | Web アプリケーション、Azure Functions、または WebJobs の発行をサポートする Azure Websites またはその他のリソースを作成するために使用されます。 |
| 更新された Web 発行ツールの <br>確認と拡張機能に関する <br>推奨事項 | marketplace.visualstudio.com | https/443 | 更新された発行ツールの可用性を確認するために使用されます。 無効の場合、Web 発行のための潜在的な推奨拡張機能が表示されない場合があります。 |
| 更新された Azure リソース <br>作成エンドポイント情報 | \*.blob.core.windows.net | https/443 | 特定の Azure Services 用の Azure Resources の作成に使用するエンドポイントを更新するために使用されます。 無効である場合は、最後にダウンロードまたは組み込まれたエンドポイントの場所が代わりに使用されます。 |
| Azure Websites のリモート デバッグ <br>および <br>リモート プロファイル | &#42;.cloudapp.net <br> &#42;.azurewebsites.net | 4022 | リモート デバッガーを Azure Websites にアタッチするために使用されます。 無効である場合、Azure Websites へのリモート デバッガーのアタッチは機能しません。 |
| Active Directory <br>Graph | graph.windows.net | https/443 | 新しい Azure Active Directory アプリケーションをプロビジョニングするために使用されます。 Microsoft 365 MSGraph と接続されたサービス プロバイダーによっても使用されます |
| Azure Functions <br>CLI 更新プログラムの <br>チェック | functionscdn.azureedge.net | https/443 | Azure Functions CLI の更新されたバージョンを確認するために使用されます。 無効である場合、CLI のキャッシュされたコピー (または、Azure Functions のコンポーネントによって実行されるコピー) が代わりに使用されます。 |
| Cordova | npmjs.org<br>gradle.org | http/80 &<br/>https/443 | ビルド時の Gradle のダウンロードには HTTP が使用され、プロジェクトに Cordova プラグインを含めるには HTTPS が使用されます。 |
| Cloud Explorer | 1. &#60;クラスター エンドポイント&#62; <br>Service Fabric <br>2. &#60;管理エンドポイント&#62;<br>汎用的な Cloud Exp <br>3. &#60;graph エンドポイント&#62;<br>汎用的な Cloud Exp<br>4. &#60;ストレージ アカウント エンドポイント&#62;<br>記憶域ノード <br>5. &#60;Azure Portal の URL&#62;<br>汎用的な Cloud Exp <br>6. &#60;キー コンテナー エンドポイント&#62; <br>Azure Resource Manager VM ノード<br>7. &#60;PublicIPAddressOfCluster&#62;<br>Service Fabric のリモート デバッグと ETW トレース | <br>1.https/19080<br>2. https/443<br>3. https/443<br>4. https/443<br>5. https/443<br>6. https/443<br>7.tcp/dynamic | 1.例: test12.eastus.cloudapp.com<br>2.サブスクリプションを取得し、Azure リソースを取得/管理します<br>3.Azure Stack サブスクリプションを取得します。<br>4.Storage リソースを管理します (例: mystorageaccount.blob.core.windows.net)<br>5.[ポータルで開く] コンテキスト メニュー オプション (Azure Portal でリソースを開く)<br>6.VM デバッグ用にキー コンテナーを作成して使用します (例: myvault.vault.azure.net) <br><br>7.クラスターおよび使用可能なポート内のノード数に基づいて、ポートのブロックを動的に割り当てます。 <br><br>最低 10 個のポートでノード数の取得を 3 回試みます。<br><br>ストリーミング トレースの場合、810 からポート ブロックの取得が試みられます。 そのポート ブロックのいずれかが既に使用されている場合は、次のブロックを取得する試みが行われるという具合に進められます (ロード バランサーが空の場合、ほとんどは 810 からのポートが使用されます)。 <br><br>デバッグの場合と同様に、ポート ブロックの 4 つのセットが予約されます。 <br>- connectorPort:30398、 <br>- forwarderPort:31398、 <br>- forwarderPortx86:31399、<br>- fileUploadPort:32398<br> |
| Cloud Services | 1.RDP<br><br>2. core.windows.net <br><br>3.  management.azure.com<br> management.core.windows.net <br><br>4. &#42;.blob.core.windows.net <br>&#42;.queue.core.windows.net<br>&#42;.table.core.windows.net <br><br>5. portal.azure.com <br><br>6. &#60;ユーザーのクラウド サービス&#62;.cloudapp.net <br> &#60;ユーザーの VM&#62;.&#60;リージョン&#62;.azure.com | 1. rdp/3389 <br><br> 2. https/443 <br><br> 3. https/443 <br><br> 4. https/443 <br><br> 5. https/443 <br><br>6. tcp <br>a) 30398 <br>b) 30400 <br>c) 31398 <br>d) 31400 <br>e) 32398 <br>f) 32400 | 1.リモート デスクトップと Cloud Services VM <br><br> 2.プライベート診断構成のストレージ アカウント コンポーネント <br><br> 3.Azure ポータル <br><br> 4.サーバー エクスプローラー - Azure Storage  &#42; は顧客によって名前が付けられるストレージ アカウントです  <br><br> 5.ポータルを開くリンク&#47;サブスクリプション証明書のダウンロード&#47; 設定ファイルの発行 <br><br>6. a) クラウド サービスおよび VM のリモート デバッグ用のコネクタ ローカル ポート<br> 6. b) クラウド サービスおよび VM のリモート デバッグ用のコネクタ パブリック ポート <br> 6. c) クラウド サービスおよび VM のリモート デバッグ用のフォワーダー ローカル ポート <br> 6. d) クラウド サービスおよび VM のリモート デバッグ用のフォワーダー パブリック ポート  <br> 6. e) クラウド サービスおよび VM のリモート デバッグ用のファイル アップローダー ローカル ポート <br> 6. f) クラウド サービスおよび VM のリモート デバッグ用のファイル アップローダー パブリック ポート |
| Service Fabric | 1. <br>docs.Microsoft.com<br>aka.ms <br>go.microsoft.com <br><br>2. <br>vssftools.blob.core.windows.net <br>Vault.azure.com <br>Portal.azure.com <br><br> 3. &#42; vault.azure.net<br><br> 4. <br>app.vsaex.visualstudio.com<br>&#42; .vsspsext.visualstudio.com<br>clouds.vsrm.visualstudio.com <br>clouds.visualstudio.com<br>app.vssps.visualstudio.com <br>&#42; .visualstudio.com | https/443 | 1.ドキュメント <br><br> 2.クラスター機能の作成 <br><br>3.&#42; は Azure Key Vault 名です (例:- test11220180112110108.vault.azure.net)  <br><br>  4.&#42; は動的です (例: vsspsextprodch1su1.vsspsext.visualstudio.com) |
| スナップショット <br>デバッガー | 1. go.microsoft.com <br>2. management.azure.com <br> 3. &#42;.azurewebsites.net <br> 4. &#42;.scm.azurewebsites.net<br>5. api.nuget.org/v3/index.json <br>6.リモート サービス/サーバーの IP アドレス/FQDN | 1. https/443 <br>2. https/443  <br>3. http/80 <br>4. https/443 <br>5. https/443 <br>6.Concord/<br> 4022 (Visual Studio バージョン依存) | 1..json ファイルに対してクエリを実行して、アプリ サービス SKU サイズを取得します <br>2.さまざまな Azure RM 呼び出し <br>3.サイト ウォーム アップ呼び出し  <br>4.顧客の対象 App Service Kudu エンドポイント <br>5.nuget.org で発行されたサイト拡張機能バージョンに対してクエリを実行します <br>6.[リモート デバッグ](../debugger/remote-debugging.md) |
| Azure Stream Analytics <br><br>HDInsight | Management.azure.com | https/443 | ASA ジョブの表示、送信、実行、管理で使用されます <br><br> HDI クラスターを参照し、HDI ジョブを送信、診断、およびデバッグするために使用されます |
| Azure Data Lake | &#42;.azuredatalakestore.net <br>&#42;.azuredatalakeanalytics.net | https/443 | ジョブのコンパイル、送信、表示、診断、およびデバッグのために使用されます。ADLS ファイルを参照するために使用されます。ファイルをアップロードおよびダウンロードするために使用されます。 |
| パッケージ サービス | [アカウント].visualstudio.com <br/> [アカウント].\*.visualstudio.com <br/> \*.blob.core.windows.net <br/> registry.npmjs.org </br> nodejs.org <br/> dist.nuget.org <br/> nuget.org | https/443 | 特定のビルド タスク (NuGet Tool インストーラー、Node Tool インストーラーなど) にのみ、またはフィードで公共のアップストリームを使用する場合にのみ、\*.npmjs.org、\*.nuget.org、\*.nodejs.org が必要です。 パッケージ サービスの中心的機能には、他の 3 つのドメインが必要です。 |
| Azure DevOps Services | \*.vsassets.io <br/> static2.sharepointonline.com <br/> dev.azure.com | | Azure DevOps Services と接続するために使用 |
| Azure Service Bus | \*.servicebus.windows.net | ampq/5671 および 5672、 </br> sbmp/9350-9354、 </br> http/80、 </br> https/443 | キュー、トピック、およびサブスクリプションの作成に使用されます。 </br> Service Bus キューおよびトピックとの間でメッセージを送受信するためにも使用されます。 |
| Azure Cosmos DB | \*.documents.azure.com | https/443 | コア ドキュメント データベース API を呼び出すために使用されます。 |
| 開発者コミュニティ | sendvsfeedback2.azurewebsites.net/api | https/443 | Developer Community フィードバック ツール API を呼び出すために使用されます (個人の懸案事項、検索、投票、コメント、送信、アップロード、再開) |
| Intellicode | \*.intellicode.vsengsaas.visualstudio.com | https/443 | Intellicode API を呼び出すために使用されます |
| Live Share | \*.liveshare.vsengsaas.visualstudio.com| https/443 | Live Share API を呼び出すために使用されます |
| GitHub Codespaces | \*.online.visualstudio.com | https/443 | GitHub Codespaces API を呼び出すために使用されます |
| JavaScript の自動型取得 | registry.npmjs.org | https/443 | TypeScript 型定義をインストールして一般的な JavaScript ライブラリ用の IntelliSense を提供するために使用されます |
| Visual Studio サブスクリプションのライセンス サービス | app.vssps.visualstudio.com/apis/<br/>Licensing/ClientRights | https/443 | オンライン アクティブ化用のライセンス |
| デバッガー | 1. <br>vsdebugger.blob.core.windows.net <br>vsdebugger.azureedge.net <br><br>2. <br>download.visualstudio.com/\*/<br/>onecore.msvsmon.\*.zip<br><br> 3. referencesource.microsoft.com/symbols <br><br> 4. <br>symbols.nuget.org/download/symbols<br><br> 5. visualstudio.com<br><br>6. msdl.microsoft.com/download/symbols | https/443 | 1. <br>Unix/macOS での .NET Core デバッグ用のデバッガー ビットを SSH 経由でダウンロードするために使用されます <br><br>2. <br>リモート Windows Docker コンテナー デバッグ用のデバッガー ビットをダウンロードするために使用されます<br><br> 3. .NET Framework ソースのステッピングを有効にするために使用されます <br><br> 4. <br>(ユーザーがオプトインする場合) nuget.org シンボル サーバーに発行されたシンボルをダウンロードするために使用されます。<br><br> 5. (ユーザーがオプトインする場合) MS シンボルとバイナリをダウンロードするために使用されます。ダンプでマネージド コードをデバッグするために必要になることもあります |
| GitHub Codespaces| \*.online.visualstudio.com | https/443 | GitHub Codespaces API を呼び出すために使用されます |
| Xamarin Android アプリの発行 | \*.googleapis.com <br/> play.google.com <br/>accounts.google.com | https/443 | Google Play ストア サービスとやりとりして、Visual Studio から Xamarin Android アプリケーションを直接発行またはアップロードするために使用されます。 |
| Visual Studio の検索サービス | data-ai.microsoft.com/search | https/443 | `Ctrl+Q` 検索ボックスに AI 対応の Visual Studio Search Service を提供するために使用されます |
| Azure Container Registry | *.azurecr.io | https/443 | CICD パイプラインの構成のために、Azure でホストされているコンテナー レジストリにアクセスします |
| | | | |

## <a name="troubleshoot-network-related-errors"></a>ネットワーク関連のエラーをトラブルシューティングする

場合によって、ファイアウォールまたはプロキシ サーバーの内側で Visual Studio をインストールし使用するときにネットワークまたはプロキシに関連するエラーが発生する場合があります。 このようなエラー メッセージの解決策の詳細については、「[Troubleshooting network-related errors when you install or use Visual Studio](troubleshooting-network-related-errors-in-visual-studio.md)」 (Visual Studio をインストールまたは使用するときのネットワーク関連のエラーのトラブルシューティング) ページを参照してください。

## <a name="get-support"></a>サポートを受ける

インストール関連の問題については、[**インストール チャット**](https://visualstudio.microsoft.com/vs/support/#talktous) (英語のみ) のサポート オプションを提供しています。

他のいくつかのサポート オプションを次に示します。

* Visual Studio インストーラーおよび Visual Studio IDE の両方に表示される [[問題の報告]](../ide/how-to-report-a-problem-with-visual-studio.md) ツールから、製品の問題を Microsoft に報告してください。
* [Visual Studio 開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)で機能の提案、製品の問題の追跡、回答の検索を行うことができます。
* [Gitter コミュニティの Visual Studio に関するスレッド](https://gitter.im/Microsoft/VisualStudio)で、ご自分の [GitHub ](https://github.com/) アカウントを使って Microsoft や他の Visual Studio 開発者と情報を交換することもできます。

## <a name="see-also"></a>関連項目

* [Live Share の接続要件](/visualstudio/liveshare/reference/connectivity/)
* [Visual Studio のネットワーク インストールを作成する](create-a-network-installation-of-visual-studio.md)
* [Visual Studio のネットワーク関連エラーのトラブルシューティング](troubleshooting-network-related-errors-in-visual-studio.md)
* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
* [ファイアウォールまたはプロキシ サーバーの内側にインストールする (Visual Studio for Mac)](/visualstudio/mac/install-behind-a-firewall-or-proxy-server)
