---
title: 高度な機能
description: 経験豊富な開発者や、既に Visual Studio に習熟している開発者向けにより適している可能性がある高度な機能について説明します。
ms.custom: vs-acquisition
ms.date: 06/01/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6cc6604816921b054b0c909177c8e641493920a8
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386197"
---
# <a name="features-of-visual-studio"></a>Visual Studio の機能

Visual Studio の基礎については、「[Visual Studio IDE の概要](../get-started/visual-studio-ide.md)」の記事で説明しています。 この記事では、経験を積んだ開発者または Visual Studio を使い慣れている開発者により適している機能について説明します。

## <a name="modular-installation"></a>モジュール式インストール

Visual Studio のモジュール式インストーラーを使用すると、"*ワークロード*" を選択してインストールすることができます。 ワークロードは、任意のプログラミング言語またはプラットフォームで必要とされる機能のグループです。 この方法により、Visual Studio のインストールのフットプリントが小さくなり、インストールと更新に要する時間が短縮されました。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

お使いのシステムに Visual Studio をセットアップする方法について詳しくは、「[Visual Studio のインストール](../install/install-visual-studio.md)」を参照してください。

## <a name="create-cloud-enabled-apps-for-azure"></a>Azure 用のクラウド対応アプリの作成

Visual Studio には、Microsoft Azure を使用するクラウド ファーストのアプリケーションを簡単に作成できるツールのスイートが用意されています。 これにより、IDE から直接 Microsoft Azure でアプリケーションとサービスを簡単に構成、ビルド、デバッグ、パッケージ化、およびデプロイできます。 Azure Tools およびプロジェクト テンプレートを入手するには、Visual Studio をインストールするときに **Azure 開発** ワークロードを選択します。

![[Azure の開発] ワークロード](../data-tools/media/azure-development-workload.png)

::: moniker range="vs-2017"

**Azure 開発** ワークロードのインストール後は、 **[新しいプロジェクト]** ダイアログ ボックスで、以下に示す C# 用 **[クラウド]** テンプレートを使用することができます。

![Visual Studio 用のクラウド プロジェクト テンプレート](media/cloud-project-templates.png)

::: moniker-end

Visual Studio の [Cloud Explorer](/azure/vs-azure-tools-resources-managing-with-cloud-explorer) では、Visual Studio 内の Azure ベースのクラウド リソースを表示および管理できます。 これらのリソースには仮想マシン、テーブル、SQL データベースなどが含まれる場合があります。 **Cloud Explorer** には、ユーザーがログインしている Azure サブスクリプションで管理されているすべてのアカウントに含まれる Azure リソースが表示されます。 特定の操作で Azure Portal が必要な場合は、**Cloud Explorer** によって提供されるリンクから Azure Portal 内の目的の場所に移動できます。

![Visual Studio の Cloud Explorer](media/cloud-explorer.png)

次のような **接続済みサービス** を使用して、アプリに Azure のサービスを活用することができます。

- ユーザーが [Azure Active Directory](/azure/active-directory/active-directory-whatis) からのアカウントを使用して Web アプリに接続するための [Active Directory 接続済みサービス](/azure/active-directory/develop/vs-active-directory-add-connected-service)
- BLOB ストレージ、キュー、およびテーブル用の [Azure Storage 接続済みサービス](/azure/vs-azure-tools-connected-services-storage)
- Web アプリのシークレットを管理する [Key Vault 接続済みサービス](/azure/key-vault/vs-key-vault-add-connected-service)

使用できる **接続済みサービス** はプロジェクトの種類によって異なります。 サービスを追加するには、**ソリューション エクスプローラー** 内のプロジェクトを右クリックし、 **[追加]**  >  **[接続済みサービス]** の順に選択します。

![Visual Studio の接続済みサービス](media/connected-services.png)

詳細については、[Visual Studio および Azure を使用したクラウドへの移行](https://visualstudio.microsoft.com/vs/azure-tools/)に関するページを参照してください。

## <a name="create-apps-for-the-web"></a>Web 用のアプリの作成

現在世界を動かしているのは Web であり、Visual Studio は Web 用のアプリの作成をサポートします。 Web アプリは ASP.NET、Node.js、Python、JavaScript、TypeScript を使用して作成できます。 Visual Studio は、Angular、jQuery、Express などの Web フレームワークを理解します。 ASP.NET Core と .NET Core は、Windows、Mac、Linux の各オペレーティング システムで実行できます。 [ASP.NET Core](https://dotnet.microsoft.com/learn/aspnet/what-is-aspnet-core) は、MVC、WebAPI、および SignalR へのメジャー アップデートであり、Windows、Mac、および Linux で実行されます。  ASP.NET Core は、最新のクラウド ベースの Web アプリとサービスをビルドするための効率的で構成可能な .NET スタックを提供するために、まったく新たに設計されました。

詳細については、「[最新の Web ツール](https://visualstudio.microsoft.com/vs/modern-web-tooling/)」をご覧ください。

## <a name="build-cross-platform-apps-and-games"></a>クロス プラットフォーム アプリとゲームをビルドする

Visual Studio を使用して、macOS、Linux、Windows 用のアプリおよびゲームをビルドし、Android、iOS、およびその他の[モバイル デバイス](https://visualstudio.microsoft.com/vs/mobile-app-development/)用のアプリおよびゲームもビルドします。

- Windows、macOS、および Linux で実行される [.NET Core](/dotnet/core/) アプリをビルドします。

- [Xamarin](https://developer.xamarin.com/guides/cross-platform/windows/visual-studio/) を使用して、iOS、Android、および Windows 向けにモバイル アプリをビルドします。

- [Visual Studio Tools for Unity](/gamedev/unity/get-started/visual-studio-tools-for-unity.md) を使用して、C# で 2D および 3D ゲームをビルドします。

- iOS、Android、および Windows デバイス用のネイティブ C++ アプリをビルドします。 [C++ for Cross-Platform Development](/cpp/cross-platform/visual-cpp-for-cross-platform-mobile-development) を使用することによって、iOS、Android、および Windows 用にビルドされたライブラリ内で共通コードを共有します。

## <a name="connect-to-databases"></a>データベースへの接続

**サーバー エクスプローラー** は、ローカル、リモートで、また Azure、Salesforce.com、Microsoft 365、および Web サイトで SQL Server インスタンスとアセットを参照および管理するのに役立ちます。 **サーバー エクスプローラー** を開くには、メイン メニューで **[表示]**  >  **[サーバー エクスプローラー]** の順に選択します。 サーバー エクスプローラーの使用方法の詳細については、「[新しい接続を追加する](../data-tools/add-new-connections.md)」をご覧ください。

[SQL Server Data Tools (SSDT)](/sql/ssdt/download-sql-server-data-tools-ssdt) は、SQL Server、Azure SQL Database、Azure SQL Data Warehouse 用の強力な開発環境です。 データベースを構築、デバッグ、管理、およびリファクターできます。 データベース プロジェクトを操作したり、オンプレミスまたはオフプレミスで接続されたデータベース インスタンスを直接操作したりすることができます。

Visual Studio の **SQL Server オブジェクト エクスプローラー** では、SQL Server Management Studio と同様のデータベース オブジェクトのビューを提供します。 SQL Server オブジェクト エクスプローラーを使用すると、データベースの簡易的な管理作業および設計作業を行うことができます。 作業の例としては、SQL Server オブジェクト エクスプローラーから直接表示するコンテキスト メニューを使用したクエリの実行、テーブル データの編集、スキーマの比較などが挙げられます。

![[SQL Server オブジェクト エクスプローラー]](../ide/media/vs2015_sqlobjectexplorer.png)

## <a name="debug-test-and-improve-your-code"></a>デバッグとテストによるコードの改善

コードを記述する際には、バグの存在やパフォーマンスを確認するために実際に実行してテストする必要があります。 Visual Studio の最新のデバッグ システムを使うと、ローカル プロジェクト、リモート デバイス、または[デバイス エミュレーター](../cross-platform/visual-studio-emulator-for-android.md)で実行されるコードをデバッグできます。 一度に 1 つのステートメントずつ、コードを実行して必要に応じて変数を検査できます。 指定した条件が True の場合にのみヒットするブレークポイントを設定することができます。 デバッグ オプションはコード エディター自体で管理できるため、コードを離れる必要はありません。 Visual Studio でのデバッグの詳細については、[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)に関するページをご覧ください。

アプリのパフォーマンスを改善する方法の詳細については、Visual Studio の[プロファイリング](../profiling/profiling-feature-tour.md)に関するページを参照してください。

[テスト](../test/improve-code-quality.md)として、Visual Studio には単体テスト、Live Unit Testing、IntelliTest、負荷およびパフォーマンス テストなどが用意されています。 Visual Studio はまた、デザイン、セキュリティ、およびその他の種類の不具合を検出する[コード分析](../code-quality/code-analysis-for-managed-code-overview.md)機能も備えています。

## <a name="deploy-your-finished-application"></a>完成したアプリケーションを配置する

アプリケーションをユーザーまたは顧客に展開する準備ができたら、Visual Studio に用意されているツールを使用してそれを行うことができます。 展開オプションには、Microsoft Store への展開、SharePoint サイトへの展開、InstallShield または Windows インストーラー テクノロジを使用した展開などがあります。 これはすべて、IDE を使用してアクセスできます。 詳細については、「[アプリケーション、サービス、およびコンポーネントの配置](../deployment/deploying-applications-services-and-components.md)」をご覧ください。

## <a name="manage-your-source-code-and-collaborate-with-others"></a>ソース コードの管理および他のユーザーとの共同作業

GitHub などの任意のプロバイダーがホストしている Git リポジトリにあるソース コードを管理できます。 また、[Azure DevOps Services](/azure/devops/index) を使用して、プロジェクト全体でコードをバグおよび作業項目と共に管理することもできます。 Visual Studio でチーム エクスプローラーを使用して Git リポジトリを管理する方法の詳細については、「[Get started with Git and Azure Repos](/azure/devops/repos/git/gitquickstart?tabs=visual-studio)」(Git および Azure Repos の使用を開始する) を参照してください。 Visual Studio には、その他の組み込みのソース管理機能もあります。 それらの機能の詳細については、[Visual Studio の新しい Git 機能](https://devblogs.microsoft.com/devops/new-git-features-in-visual-studio-2017/)に関するブログを参照してください。

Azure DevOps Services はクラウド ベースのサービスであり、ソフトウェアのプランニング、ホスティング、自動化、およびデプロイを行うことができるほか、チームでのコラボレーションが可能になります。 Azure DevOps Services では、Git リポジトリ (分散型バージョン管理) と Team Foundation バージョン管理 (集中型バージョン管理) の両方がサポートされています。 また、バージョン管理システムに格納されたコードを継続的にビルドおよびリリース (CI/CD) できるようにパイプラインがサポートされています。 Azure DevOps Services では、スクラム、CMMI、アジャイル開発方法もサポートしています。

Team Foundation Server (TFS) は、Visual Studio のアプリケーション ライフサイクル管理のハブです。 これにより、開発プロセスに関わるすべてのユーザーが 1 つのソリューションを使用して参加できるようになります。 TFS は、異種混合のチームやプロジェクトを管理するのにも役立ちます。

Azure DevOps 組織または Team Foundation Server がネットワーク上にある場合、Visual Studio の **[チーム エクスプローラー]** ウィンドウから接続することができます。 このウィンドウからソース管理にコードをチェックインしたりソース管理からコードをチェックアウトできます。また、作業項目を管理したり、ビルドを開始したり、チームのルームやワークスペースにアクセスできます。 **チーム エクスプローラー** は、検索ボックスから開くか、メイン メニューの **[ビュー]**  >  **[チーム エクスプローラー]** または **[チーム]**  >  **[接続の管理]** を選択して開くことができます。

次の図は、Azure DevOps Services でホストされているソリューションの **[チーム エクスプローラー]** ウィンドウを示しています。

![Visual Studio Team Explorer](../ide/media/vs2017_teamexplorer_devops.png)

チームの開発者がバージョン管理にチェックインしたコードをビルドするように、ビルド プロセスを自動化することもできます。 たとえば、1 つまたは複数のプロジェクトを夜間にビルドすることも、コードのチェックインごとにビルドすることもできます。 詳細については、「[Azure Pipelines](/azure/devops/pipelines/index?view=vsts&preserve-view=true)」を参照してください。

## <a name="extend-visual-studio"></a>Visual Studio を拡張する

Visual Studio に必要な機能がない場合は、機能を追加できます。 ワークフローとスタイルに基づいて IDE をカスタマイズしたり、Visual Studio にまだ統合されていない外部ツールのサポートを追加したり、既存の機能を変更して生産性の向上を図ることができます。 Visual Studio 機能拡張ツール (VS SDK) の最新バージョンを検索するには、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

.NET Compiler Platform ("Roslyn") を使って、独自のコード アナライザーとコード ジェネレーターを記述することができます。 必要なものはすべて [Roslyn](https://github.com/dotnet/Roslyn)に揃っています。

Microsoft 開発者や開発コミュニティが作成した Visual Studio の[既存の拡張機能](https://marketplace.visualstudio.com/vs) を検索してください。

Visual Studio の拡張について詳しくは、「[Visual Studio IDE を機能拡張する](https://visualstudio.microsoft.com/vs/extend/)」をご覧ください。

## <a name="see-also"></a>参照

- [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
- [Visual Studio 2017 の新機能](../ide/whats-new-visual-studio-2017.md)
- [Visual Studio 2019 の新機能](../ide/whats-new-visual-studio-2019.md)
