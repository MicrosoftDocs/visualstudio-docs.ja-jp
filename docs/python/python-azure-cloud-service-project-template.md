---
title: Python 用 Azure クラウド サービス プロジェクト テンプレート
description: Visual Studio には、役割の展開、依存関係、トラブルシューティングなど、Python で記述された Azure クラウド サービス用のテンプレートが用意されています。
ms.date: 11/12/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
monikerRange: vs-2017
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 2de0f255da54d5bd8abf865f6534041d88bbbca3
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254837"
---
# <a name="azure-cloud-service-projects-for-python"></a>Python 用 Azure クラウド サービス プロジェクト

Visual Studio は、Python を使用して Azure Cloud Services の作成に使用できるテンプレートを提供しています。

[クラウド サービス](/azure/cloud-services/)は、任意の数の *worker ロール* と *Web ロール* から構成され、それぞれが概念的に独立したタスクを実行しますが、規模拡張の必要に応じて仮想マシン間で個別にレプリケートできます。 Web ロールでは、フロントエンド Web アプリケーションのホスティングが提供されます。 Python が接続されている場合、WSGI をサポートする任意の Web フレームワークを使用して、このようなアプリケーションを作成できます ([Web プロジェクト テンプレート](python-web-application-project-templates.md)でサポート)。 worker ロールは、ユーザーと直接対話しない長時間実行されるプロセスを意図しています。 通常は、[`pip install azure`](https://pypi.org/project/azure) でインストールされる "azure" パッケージ内のパッケージを利用します。

この記事では、Visual Studio 2017 以降のプロジェクト テンプレートとその他のサポートについて詳しく説明します (以前のバージョンとよく似ていますが、いくつかの違いがあります)。 Python からの Azure の操作について詳しくは、[Azure Python デベロッパー センター](/azure/python/)をご覧ください。

## <a name="create-a-project"></a>プロジェクトを作成する

1. クラウド サービス テンプレートを使用するために必要な [Azure .NET SDK for Visual Studio](https://visualstudio.microsoft.com/vs/azure-tools/) をインストールします。
1. Visual Studio で、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** を選択し、"Azure Python" を検索して **[Azure クラウド サービス]** を一覧から選びます。

    ![Python 用 Azure クラウド プロジェクト テンプレート](media/template-azure-cloud-project.png)

1. 含める 1 つ以上のロールを選びます。 クラウド プロジェクトは、異なる言語で記述されたロールを結合できるため、アプリケーションの各部分を最も適した言語で簡単に記述できます。 このダイアログの完了後に新しいロールをプロジェクトに追加するには、**ソリューション エクスプローラー** で **[ロール]** を右クリックし、 **[追加]** の下で項目の 1 つを選びます。

    ![Azure クラウド プロジェクト テンプレートでのロールの追加](media/template-azure-cloud-service-project-wizard.png)

1. 個々のロール プロジェクトが作成されるときに、Django、Bottle、Flask フレームワークなどの追加の Python パッケージの 1 つを使用するロールを選んだ場合は、これらをインストールするように求めるプロンプトが表示されることがあります。

1. プロジェクトに新しいロールを追加すると、構成手順がいくつか表示されます。 構成の変更は通常必要ありませんが、プロジェクトの将来のカスタマイズに役立つ場合があります。 同時に複数のロールを追加する場合は、最後のロールについての説明のみ開いたままになります。 ただし、他のロールの手順とトラブルシューティングのヒントは、ロールのルートか *bin* フォルダーにある、それぞれの *readme.mht* ファイルで参照できます。

1. プロジェクトの *bin* フォルダーには 1 つまたは 2 つの PowerShell スクリプトも含まれていて、これは Python のインストール、プロジェクトの [*requirements.txt*](#dependencies) ファイル、必要があれば IIS の設定など、リモート仮想マシンを構成するために使用されます。 デプロイでの必要に応じてこれらのファイルを編集できますが、一般的なオプションのほとんどは他の方法で管理できます (下の「[ロールのデプロイを構成する](#configure-role-deployment)」を参照)。 これらのファイルが使用可能でない場合はレガシ構成スクリプトが代わりに使用されるため、これらのファイルの削除はお勧めしません。

    ![worker ロールのサポート ファイル](media/template-azure-cloud-service-worker-role-support-files.png)

    これらの構成スクリプトを新しいプロジェクトに追加するには、プロジェクトを右クリックし、 **[追加]**  >  **[新しい項目]** を選び、 **[Web ロール サポート ファイル]** または **[worker ロール サポート ファイル]** のいずれかを選びます。

## <a name="configure-role-deployment"></a>ロールのデプロイの構成

ロール プロジェクトの *bin* フォルダー内の PowerShell スクリプトは、そのロールのデプロイを制御し、編集して構成をカスタマイズできます。

- *ConfigureCloudService.ps1* は、通常は依存関係をインストールして構成し、Python のバージョンを設定するために Web ロールと worker ロールに使用されます。
- *LaunchWorker.ps1* は worker ロールのためにのみ使用され、起動の動作の変更、コマンドライン引数の追加、環境変数の追加に使用されます。

どちらのファイルにも、カスタマイズの手順が含まれます。 メインのクラウド サービス プロジェクトの *ServiceDefinition.csdef* ファイルに別のタスクを追加し、`PYTHON` 変数をインストールされている *python.exe* (または同等のもの) のパスに設定することで、独自のバージョンの Python をインストールすることもできます。 `PYTHON` が設定されている場合、Python は NuGet からインストールされません。

追加の構成は、次のように実行できます。

1. プロジェクトのルート ディレクトリ内の *requirements.txt* ファイルを更新することで、`pip` を使用してパッケージをインストールします。 *ConfigureCloudService.ps1* スクリプトでは、デプロイ時にこのファイルがインストールされます。
1. *web.config* ファイル (Web ロール) または *ServiceDefinition.csdef* ファイル (worker ロール) の `Runtime` セクションを変更することで、環境変数を設定します。
1. *ServiceDefinitions.csdef* ファイルの `Runtime/EntryPoint` セクションでコマンド ラインを変更して、worker ロールに使用するスクリプトと引数を指定します。
1. *web.config* ファイルを通じて、Web ロールのメイン ハンドラー スクリプトを設定します。

## <a name="test-role-deployment"></a>ロールのデプロイのテスト

ロールの書き込み中に、クラウド サービス エミュレーターを使用してクラウド プロジェクトをローカルでテストできます。 エミュレーターは Azure SDK Tools に含まれるもので、クラウド サービスが Azure に発行されるときに使用される環境の制限付きバージョンです。

エミュレーターを起動するには、最初に右クリックして **[スタートアップ プロジェクトに設定]** を選択して、クラウド プロジェクトがソリューションのスタートアップ プロジェクトであることを確認します。 次に、 **[デバッグ]**  >  **[デバッグの開始]** (**F5**)、または **[デバッグ]**  >  **[デバッグなしで開始]** (**Ctrl**+**F5**) の順に選択します。

エミュレーターでの制限により、Python コードをデバッグすることはできません。 したがって、ロールを個別に実行し、発行する前に統合テストにエミュレーターを使用してロールをデバッグすることをお勧めします。

## <a name="deploy-a-role"></a>ロールのデプロイ

**発行** ウィザードを開くには、**ソリューション エクスプローラー** でロール プロジェクトを選び、メイン メニューから **[ビルド]** > **[発行]** の順に選択するか、プロジェクトを右クリックして **[発行]** を選択します。

発行プロセスには 2 つのフェーズが含まれます。 まず、Visual Studio で、クラウド サービスのすべてのロールを含む 1 つのパッケージを作成します。 このパッケージは Azure にデプロイされるもので、ロールごとに 1 台以上の仮想マシンを初期化し、ソースをデプロイします。

各仮想マシンがアクティブになると、これは *ConfigureCloudService.ps1* スクリプトを実行して、すべての依存関係をインストールします。 既定では、このスクリプトは Python の最新バージョンを [NuGet](https://www.nuget.org/packages?q=Tags%3A%22python%22+Authors%3A%22Python+Software+Foundation%22) からインストールし、*requirements.txt* ファイルで指定されたパッケージをインストールします。

最後に、worker ロールは Python スクリプトの実行を開始する *LaunchWorker.ps1* を実行します。Web ロールは IIS を初期化し、Web 要求の処理を開始します。

## <a name="dependencies"></a>依存関係

Cloud Services では、*ConfigureCloudService.ps1* スクリプトは `pip` を使用して Python の依存関係のセットをインストールします。 依存関係は、*requirements.txt* という名前のファイルで指定する必要があります (*ConfigureCloudService.ps1* を修正することでカスタマイズ可能)。 ファイルは初期化の一部として `pip install -r requirements.txt` で実行されます。

クラウド サービス インスタンスには C コンパイラが含まれていないため、C の拡張子を持つすべてのライブラリはコンパイル済みのバイナリを提供する必要があります。

*requirements.txt* 内のパッケージに加えて、pip とその依存関係が自動的にダウンロードされ、課金対象となる帯域幅の使用としてカウントされる可能性があります。 *requirements.txt* ファイルの管理について詳しくは、「[必要なパッケージの管理](managing-required-packages-with-requirements-txt.md)」をご覧ください。

## <a name="troubleshooting"></a>トラブルシューティング

デプロイ後に Web または worker ロールが正常に動作しない場合は、以下を確認します。

- 少なくとも以下を含む *bin\\* フォルダーが Python プロジェクトに含まれること。

  - *ConfigureCloudService.ps1*
  - *LaunchWorker.ps1* (worker ロール用)
  - *ps.cmd*

- すべての依存関係 (またはホイール ファイルのコレクション) の一覧を含む *requirements.txt* ファイルが Python プロジェクトに含まれること。
- クラウド サービスでリモート デスクトップを有効にし、ログ ファイルを調査します。
- *ConfigureCloudService.ps1* と *LaunchWorker.ps1* のログは、リモート コンピューター上の *C:\Resources\Directory\%RoleId%.DiagnosticStore\LogFiles* フォルダーに格納されます。
- Web ロールが *web.config* で構成されているパス (`WSGI_LOG` appSetting のパス) に追加のログを書き込めること。 ほとんどの標準的な IIS または FastCGI ロギングも動作すること。
- 現在、*LaunchWorker.ps1.log* ファイルは、Python の worker ロールによって表示される出力またはエラーを表示する唯一の方法です。
