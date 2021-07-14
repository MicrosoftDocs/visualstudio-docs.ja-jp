---
title: フォルダー、IIS、Azure、または別の場所に Visual Studio アプリを配置する
titleSuffix: ''
description: 発行ツールを使用したアプリの発行オプションに関する詳細情報
ms.custom:
- SEO-VS-2020
- contperf-fy21q1
ms.date: 08/21/2020
ms.topic: troubleshooting
f1_keywords:
- vs.publish
dev_langs:
- FSharp
- VB
- CSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 099bd2c6cc47895c913b3f852835d2fd09d0f9c3
ms.sourcegitcommit: 4e09130bcd55bb9cb8ad157507c23b67aa209fad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2021
ms.locfileid: "113549486"
---
# <a name="deploy-your-app-to-a-folder-iis-azure-or-another-destination"></a>フォルダー、IIS、Azure、または別の場所にアプリを配置する

アプリケーション、サービス、またはコンポーネントを配置すると、他のコンピューターのデバイス、サーバー、またはクラウドに対してインストールするために、それらを配布することになります。 必要な配置の種類に合わせて、Visual Studio で適切な手法を選択します。

配置タスクのサポートが必要な場合:

- どの配置オプションを選択すればよいかわかりませんか? 「[どの発行オプションを使用すべきでしょうか?](#what-publishing-options-are-right-for-me)」を参照してください。
- Azure App Service または IIS の配置に関するイシューのサポートについては、「[Azure App Service および IIS での ASP.NET Core のトラブルシューティング](/aspnet/core/test/troubleshoot-azure-iis)」を参照してください。
- .NET 配置設定の構成について詳しくは、「[.NET 配置設定を構成する](#configure-net-deployment-settings)」を参照してください。
- 既に発行プロファイルを作成していて、新しいターゲットに配置する場合は、構成されているプロファイルの **[発行]** ウィンドウで **[新規]** を選択します。

   ![新しい発行プロファイルを作成する](../deployment/media/create-a-new-publish-profile.png)

   次に、[発行] ウィンドウで配置オプションを選択します。 発行オプションの詳細については、次のセクションを参照してください。

## <a name="what-publishing-options-are-right-for-me"></a>状況に適した発行オプション

Visual Studio 内から、次のターゲットにアプリケーションを直接発行できます。

::: moniker range=">=vs-2019"
- [Azure](#azure)
- [Docker コンテナー レジストリ](#docker-container-registry)
- [フォルダー](#folder)
- [FTP/FTPS サーバー](#ftpftps-server)
- [Web サーバー (IIS)](#web-server-iis)
- [プロファイルのインポート](#import-profile)
::: moniker-end
::: moniker range="vs-2017"
- [App Service](#azure-app-service)
- [App Service Linux](#azure-app-service)
- [IIS (IIS、FTP などを選択します)](#web-server-iis)
- [FTP/FTPS (IIS、FTP などを選択します)](#ftpftps-server)
- [フォルダー](#folder)
- [プロファイルのインポート](#import-profile)
::: moniker-end

上記のオプションは、次の図に示すように、新しい発行プロファイルを作成するときに表示されます。

::: moniker range=">=vs-2019"
![発行オプションを選択する](../deployment/media/quickstart-publish-dialog.png)
::: moniker-end
::: moniker range="vs-2017"
![発行オプションを選択する](../deployment/media/quickstart-publish-dialog-vs-2017.png)
::: moniker-end

アプリケーションの配置に関する一般的なオプションの概要については、[配置の概要](../deployment/deploying-applications-services-and-components.md)に関する記事を参照してください

## <a name="azure"></a>Azure 

Azure を選択する場合は、次のいずれかを選択できます。

- Windows、Linux 上で実行している、または Docker イメージとして実行している [Azure App Service](#azure-app-service)
- [Azure Container Registry](#azure-container-registry) にデプロイした Docker イメージ
- [Azure 仮想マシン](#azure-virtual-machine)

![Azure サービスを選択する](../deployment/media/quickstart-choose-azure-service.png)

### <a name="azure-app-service"></a>Azure App Service

開発者は [Azure App Service](/azure/app-service/app-service-web-overview) を使用して、スケーラブルな Web アプリケーションとサービスをすばやく作成でき、インフラストラクチャを保守する必要はありません。 App Service は Azure のクラウドでホストされる仮想マシン上で実行されますが、これらの仮想マシンはユーザーが管理します。 App Service の各アプリには、\*.azurewebsites.net という一意の URL が割り当てられます。Free 以外のすべての価格レベルでは、カスタム ドメイン名をサイトに割り当てることもできます。

App Service の[価格レベルまたはプラン](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)を選ぶことで、App Service に備わるコンピューティング能力を決定します。 また、価格レベルを変更することなく、複数の Web アプリ (および他の種類のアプリ) で同じ App Service を共有することもできます。 たとえば、開発、ステージング、運用の Web アプリを同じ App Service でホストすることができます。

#### <a name="when-to-choose-azure-app-service"></a>Azure App Service を選ぶ状況

- インターネット経由でアクセスできる Web アプリケーションをデプロイしたい。
- 再デプロイする必要なしに、需要に応じて Web アプリケーションを自動的に拡張したい。
- サーバーのインフラストラクチャを管理したくない (すべてのソフトウェアの更新を含む)。
- Web アプリケーションをホストするサーバーで、コンピューター レベルのカスタマイズを行う必要がない。

> 自社のデータセンターまたは他のオンプレミス コンピューターで Azure App Service を使いたい場合は、[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) を使って行うことができます。

App Service への発行について詳しくは、次を参照してください。
- [クイックスタート - Azure App Service に発行する](quickstart-deploy-to-azure.md)
- [クイックスタート - Linux に ASP.NET Core を発行する](quickstart-deploy-to-linux.md)
- [Azure App Service に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)
- 「[Azure App Service および IIS での ASP.NET Core のトラブルシューティング](/aspnet/core/test/troubleshoot-azure-iis)」。

### <a name="azure-container-registry"></a>Azure Container Registry

[Azure Container Registry](/azure/container-registry/) では、あらゆる種類のコンテナー デプロイに対して、プライベート レジストリで Docker コンテナー イメージや成果物をビルド、保存、管理できます。

#### <a name="when-to-choose-azure-container-registry"></a>Azure Container Registry を選択する状況

- 既存の Docker コンテナー開発とデプロイ パイプラインがある場合。
- Azure で Docker コンテナー イメージをビルドする場合。

詳細情報:

- [ASP.NET コンテナーをコンテナー レジストリにデプロイする](../containers/hosting-web-apps-in-docker.md)

### <a name="azure-virtual-machine"></a>Azure Virtual Machine

[Azure Virtual Machines (VM)](https://azure.microsoft.com/documentation/services/virtual-machines/) を使用すると、任意の数のコンピューティング リソースをクラウドに作成して管理できます。 VM 上のすべてのソフトウェアと更新プログラムについての責任を負うことにより、ユーザーはお使いのアプリケーションで必要なだけいくらでもカスタマイズできます。 また、ユーザーはリモート デスクトップを介して仮想マシンに直接アクセスでき、各マシンは必要な限り割り当てられた IP アドレスを保持します。

仮想マシンでホストされているアプリケーションのスケーリングには、需要に応じた追加 VM のスピンアップと、必要なソフトウェアのデプロイが含まれます。 このような制御レベルの追加により、グローバル リージョンごとに拡張方法を変えることができます。 たとえば、異なるリージョンの従業員がアプリケーションを利用している場合、リージョンの従業員の数に従って VM を拡張でき、コストを削減できる可能性があります。

詳しくは、Visual Studio の [カスタム] オプションを使って配置ターゲットとして使用できる Azure App Service、Azure Virtual Machines、およびその他の Azure サービスの間の[詳細な違い](/azure/architecture/guide/technology-choices/compute-decision-tree)を参照してください。

#### <a name="when-to-choose-azure-virtual-machines"></a>Azure Virtual Machines を選択する状況

- インターネット経由でアクセス可能な Web アプリケーションをデプロイし、割り当てられた IP アドレスの有効期間全体を通して完全に制御したい。
- 専用データベース システムなどの追加ソフトウェア、特定のネットワーク構成、ディスク パーティションなど、サーバーでコンピューター レベルのカスタマイズが必要である。
- Web アプリケーションのスケーリングをきめ細かく制御したい。
- その他の理由で、アプリケーションをホストするサーバーに直接アクセスする必要がある。

> 自社のデータセンターまたは他のオンプレミス コンピューターで Azure Virtual Machines を使いたい場合は、[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) を使って行うことができます。

## <a name="docker-container-registry"></a>Docker コンテナー レジストリ

アプリケーションで Docker を使用している場合は、コンテナー化されたアプリケーションを Docker コンテナー レジストリに発行できます。

### <a name="when-to-choose-docker-container-registry"></a>Docker コンテナー レジストリを選択するタイミング

- コンテナー化されたアプリケーションを配置する場合

詳細については、「

- [ASP.NET コンテナーをコンテナー レジストリにデプロイする](../containers/hosting-web-apps-in-docker.md)
- [Docker Hub に配置する](../containers/deploy-docker-hub.md)

## <a name="folder"></a>フォルダー

ファイル システムへの配置とは、ユーザーが所有するコンピューターの特定のフォルダーにアプリケーションのファイルをコピーすることを意味します。 フォルダーへの配置は、テスト目的で、またはコンピューターでサーバーも実行している場合に限られた数のユーザーが使用するアプリケーションを配置する場合に、最もよく使われます。 ターゲット フォルダーがネットワークで共有されている場合、ファイル システムにデプロイすると、他のユーザーも Web アプリケーション ファイルを使用して特定のサーバーにデプロイできます。
::: moniker range=">=vs-2019"
Visual Studio 2019 16.8 以降、フォルダー ターゲットには、ClickOnce を使用して .Net Windows アプリケーションを発行する機能が含まれています。

ClickOnce を使用して .NET Core 3.1、またはそれ以降の Windows アプリケーションを発行する場合は、[ClickOnce を使用して .NET Windows アプリケーションを配置する](quickstart-deploy-using-clickonce-folder.md)方法に関するページを参照してください。
::: moniker-end
アプリケーションの構成方法およびアプリケーションが接続されているネットワークに応じて、サーバーを実行しているすべてのローカル コンピューターで、インターネットまたはイントラネットを通してアプリケーションを利用できます (コンピューターがインターネットに直接接続されている場合、外部のセキュリティ脅威からの保護に特に注意が必要です)。ユーザーは、これらのコンピューターを管理するので、ソフトウェアとハードウェアの構成を完全に制御できます。

何らかの理由で (コンピューターのアクセスなど) ユーザーが Azure App Service や Azure Virtual Machines などのクラウド サービスを使用できない場合、ユーザーは自社のデータセンターで [Azure Stack](https://azure.microsoft.com/overview/azure-stack/) を使用できます。 Azure Stack を使うと、ユーザーは Azure App Service および Azure Virtual Machines によってコンピューティング リソースを管理および使用しながら、すべてのものをオンプレミスに保持できます。

### <a name="when-to-choose-file-system-deployment"></a>ファイル システムのデプロイを選ぶ状況

- ファイル共有にアプリケーションをデプロイし、他のユーザーがそれを別のサーバーにデプロイすることだけが必要である。
::: moniker range=">=vs-2019"
- ClickOnce を使用して .NET Windows アプリケーションを配置したい
::: moniker-end
- ローカル テスト デプロイのみが必要である。
- 別のデプロイ ターゲットに送る前にアプリケーション ファイルを調べて場合によっては個別に変更したい。

詳細については、[ローカル フォルダーへの配置のクイックスタート](quickstart-deploy-to-local-folder.md)に関するページを参照してください
::: moniker range=">=vs-2019"
ClickOnce を使用した .NET Windows アプリケーションの配置の詳細については、[ClickOnce を使用して .NET Windows アプリケーションを配置する](quickstart-deploy-using-clickonce-folder.md)方法に関するページを参照してください。
::: moniker-end

設定を選択するための追加のヘルプを参照するには、次を参照してください。

- [フレームワーク依存と自己完結型の展開](/dotnet/core/deploying/)
- [ターゲット ランタイム識別子 (ポータブル RID など)](/dotnet/core/rid-catalog)
- [デバッグ構成とリリース構成](../ide/understanding-build-configurations.md)

## <a name="ftpftps-server"></a>FTP または FTPS サーバー

FTP または FTPS サーバーを使用すると、Azure 以外のサーバーにアプリケーションをデプロイできます。 アクセスできるファイル システムや他のサーバー (インターネットまたはイントラネット) にデプロイできます。他のクラウド サービスも含まれます。 Web デプロイ (ファイルまたは .ZIP) および FTP で使用できます。

FTP または FTPS サーバーを選択すると、Visual Studio からプロファイル名の指定を求められます。その後、ターゲット サーバーまたは場所、サイト名、資格情報などの追加の **接続** 情報が収集されます。 **[設定]** タブで次のビヘイビアーをコントロールできます。

- デプロイする構成。
- 宛先から既存のファイルを削除するかどうか。
- 発行中にプリコンパイルするかどうか。
- App_Data フォルダーのファイルをデプロイから除外するかどうか。

Visual Studio では任意の数の FTP または FTPS デプロイ プロファイルを作成し、異なる設定でプロファイルを管理できます。

### <a name="when-to-choose-ftpftps-server-deployment"></a>FTP または FTPS サーバー デプロイを選択する状況

- URL でアクセスできる Azure 以外のプロバイダーでクラウド サービスを使っている。
- Visual Studio で使っている資格情報または Azure アカウントに直接結び付けられている資格情報とは異なる資格情報を使ってデプロイしたい。
- デプロイするたびに、ターゲットからファイルを削除したい。

## <a name="web-server-iis"></a>Web サーバー (IIS)

IIS Web サーバーを使用すると、Azure 以外の Web サーバーにアプリケーションをデプロイできます。 アクセス可能な IIS サーバー (インターネットまたはイントラネット) にデプロイできます。これには他のクラウド サービスのものも含まれます。 Web 配置または Web 配置パッケージと連携できます。

IIS Web サーバーを選択すると、Visual Studio からプロファイル名の指定を求められます。その後、ターゲット サーバーまたは場所、サイト名、資格情報などの追加の **接続** 情報が収集されます。 **[設定]** タブで次のビヘイビアーをコントロールできます。

- デプロイする構成。
- 宛先から既存のファイルを削除するかどうか。
- 発行中にプリコンパイルするかどうか。
- App_Data フォルダーのファイルをデプロイから除外するかどうか。

Visual Studio では任意の数の IIS Web サーバー デプロイ プロファイルを作成し、異なる設定でプロファイルを管理できます。

### <a name="when-to-choose-web-server-iis-deployment"></a>Web サーバー (IIS) デプロイを選択する状況

- URL を通してアクセスできるサイトまたはサービスを発行するために IIS を使用する。
- Visual Studio で使っている資格情報または Azure アカウントに直接結び付けられている資格情報とは異なる資格情報を使ってデプロイしたい。
- デプロイするたびに、ターゲットからファイルを削除したい。

詳細については、[クイック スタート - Web サイトへのデプロイ](quickstart-deploy-to-a-web-site.md)に関するページを参照してください。

IIS での ASP.NET Core のトラブルシューティングについて詳しくは、「[Azure App Service および IIS での ASP.NET Core のトラブルシューティング](/aspnet/core/test/troubleshoot-azure-iis)」を参照してください。

## <a name="import-profile"></a>インポート プロファイル

IIS または Azure App Service に発行するときに、プロファイルをインポートできます。 "*発行設定ファイル*" ( *\*.publishsettings*) を使用してデプロイを構成できます。 発行設定ファイルは、IIS または Azure App Service を使用して作成するか、手動で作成して Visual Studio にインポートすることができます。

発行設定ファイルを使用すると、各デプロイ プロファイルを手動で構成するよりも、デプロイ構成が簡素化され、チーム環境で作業しやすくなります。

### <a name="when-to-choose-import-profile"></a>プロファイルのインポートを選択する状況

- IIS に発行し、デプロイ構成を簡略化したい。
- IIS または Azure App Service に発行し、再利用や同じサービスに発行するチーム メンバーのために配置構成を高速化したい。

詳細については、「

- [発行設定のインポートと IIS へのデプロイ](tutorial-import-publish-settings-iis.md)
- [発行設定のインポートと Azure へのデプロイ](tutorial-import-publish-settings-azure.md)

## <a name="configure-net-deployment-settings"></a>.NET 配置設定を構成する

設定を選択するための追加のヘルプを参照するには、次を参照してください。

- [フレームワーク依存と自己完結型の展開](/dotnet/core/deploying/)
- [ターゲット ランタイム識別子 (ポータブル RID など)](/dotnet/core/rid-catalog)
- [デバッグ構成とリリース構成](../ide/understanding-build-configurations.md)

## <a name="next-steps"></a>次の手順

チュートリアル:

- [発行ツールを使用して .NET Core アプリケーションを展開する](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Visual C++ での配置](/cpp/windows/deployment-in-visual-cpp)
- [UWP アプリを配置する](/windows/uwp/packaging/packaging-uwp-apps?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Web 配置を使用して Azure に Node.js アプリを発行する](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Azure App Service に Python アプリを発行する](../python/publishing-python-web-applications-to-azure-from-visual-studio.md?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
