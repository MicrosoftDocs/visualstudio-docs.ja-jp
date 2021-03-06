---
title: Azure App Service に ASP.NET Core コンテナーをデプロイする
description: Visual Studio コンテナー ツールを使用し、Docker コンテナーの ASP.NET Core Web アプリを Azure App Service にデプロイする方法について説明します
ms.custom: SEO-VS-2020
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.devlang: dotnet
ms.topic: how-to
ms.date: 02/21/2021
ms.author: ghogen
ms.openlocfilehash: f9a4f26227d2cd3bd065fab88ba294f7341ea4ed
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101684313"
---
# <a name="deploy-an-aspnet-core-container-to-azure-app-service-using-visual-studio"></a>Visual Studio を使用した Azure App Service への ASP.NET Core コンテナーのデプロイ

このチュートリアルでは、Visual Studio を使用し、コンテナー化された ASP.NET Core Web アプリケーションを [Azure App Service](/azure/app-service) に発行する方法について説明します。 Azure App Service は、Azure でホストされている単一コンテナー Web アプリに最適なサービスです。

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/dotnet/?utm_source=acr-publish-doc&utm_medium=docs&utm_campaign=docs) を作成してください。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次のものが必要です。

::: moniker range="vs-2017"
- "ASP.NET および Web 開発" ワークロードと共に、最新バージョンの [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) をインストールする
::: moniker-end
::: moniker range=">=vs-2019"
- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) と *ASP.NET と Web 開発* ワークロード。
::: moniker-end
- [Docker Desktop](https://docs.docker.com/docker-for-windows/install/) のインストール

## <a name="create-an-aspnet-core-web-app"></a>ASP.NET Core Web アプリを作成する

次の手順では、このチュートリアルで使用する基本的な ASP.NET Core アプリの作成について説明します。

::: moniker range="vs-2017"
1. Visual Studio のメニューで、 **[ファイル]、[新規作成]、[プロジェクト]** の順に選択します。
2. **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** セクションで、 **[Visual C#]、[Web]** の順に選択します。
3. **[ASP.NET Core Web アプリケーション]** を選択します。
4. 新しいアプリケーションに名前を設定 (または、既定の名前をそのまま使用) して、 **[OK]** を選択します。
5. **[Web アプリケーション]** を選択します。
6. **[Docker サポートを有効にする]** チェック ボックスをオンにします。
7. コンテナーの種類に **[Linux]** を選択し、 **[OK]** をクリックします。 Windows コンテナーはコンテナーとして Azure App Service にデプロイできません。
::: moniker-end
::: moniker range=">= vs-2019"
1. Visual Studio の [スタート] ウィンドウから **[新しいプロジェクトの作成]** を選択します。
1. **[ASP.NET Core Web アプリ]** を選択し、 **[次へ]** を選択します。
1. 新しいアプリケーションに名前を設定 (または、既定の名前をそのまま使用) し、 **[次へ]** を選択します。
1. 対象にする .NET バージョンを選択します。 よくわからない場合は、長期サポート (LTS) バージョンを選択してください。
1. **[HTTPS 用の構成]** チェックボックスを使用し、SSL サポートを使用するかどうかを選択します。
1. **[Docker サポートを有効にする]** チェック ボックスをオンにします。
1. コンテナーの種類を選択し、 **[作成]** をクリックします。
::: moniker-end

## <a name="deploy-the-container-to-azure"></a>コンテナーを Azure にデプロイする

::: moniker range="vs-2017"

1. **ソリューション エクスプローラー** で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
1. 発行先ダイアログで、 **[App Service Linux]** または **[App Service]** を選択します。 これは、Web サーバーをホストするオペレーティング システムです。
1. App Service にのみ発行するか、App Service と Azure Container Registry (ACR) の両方に発行できます。 Azure Container Registry (ACR) でコンテナーを発行するには、 **[Create new App Service for containers]\(コンテナー用に新しい App Service を作成する\)** を選択し、 **[発行]** をクリックします。

   ![発行ダイアログのスクリーンショット](media/deploy-app-service/publish-app-service-linux-1.png)

   Azure Container Registry を使用せずに Azure App Service にのみ発行するには、 **[新規作成]** を選択し、 **[発行]** をクリックします。

1. Azure サブスクリプションに関連付けられているアカウントでサインインしていることを確認し、一意の名前、サブスクリプション、リソース グループ、ホスティング プラン、コンテナー レジストリ (該当する場合) を選択するか、既定値をそのまま選択します。

   ![発行設定のスクリーンショット](media/deploy-app-service/publish-app-service-linux-2.png)

1. **[作成]** を選択します。 選択したリソース グループとコンテナー レジストリでコンテナーが Azure にデプロイされます。 このプロセスには時間が少しばかりかかります。 完了すると、 **[発行]** タブにサイトの URL など、発行したものに関する情報が表示されます。

   ![発行タブのスクリーンショット](media/deploy-app-service/publish-succeeded.PNG)

1. サイト リンクをクリックし、Azure でアプリが想定どおりに動作することを確認します。

   ![Web アプリケーションのスクリーンショット](media/deploy-app-service/web-application-running.png)

1. リソース グループやコンテナー レジストリなど、選択したすべての詳細が含まれる発行プロファイルが保存されます。

1. 同じ発行プロファイルでもう一度デプロイするには、 **[発行]** ボタンか **[Web 発行アクティビティ]** ウィンドウの **[発行]** ボタンを使用するか、**ソリューション エクスプローラー** でプロジェクトを右クリックし、コンテキストメニューで **[発行]** 項目を選択します。
:::moniker-end
:::moniker range=">=vs-2019"
1. **ソリューション エクスプローラー** で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
1. **[発行]** ダイアログで、**Azure** をターゲットとして選択します。

   ![発行ウィザードのスクリーンショット](media/deploy-app-service/publish-choices.png)

1. **[特定のターゲット]** タブで、コンテナーの種類に応じて、**App Service (Windows)** や **App Service (Linux)** など、適切なデプロイ ターゲットを選択します。

   ![発行ウィザードの [特定のターゲット] タブのスクリーンショット](media/deploy-app-service/publish-app-service-windows.png)

1. 使用するサブスクリプションで適切な Azure アカウントにサインインしていない場合は、 **[発行]** ウィンドウの左上にあるボタンを使用してサインインします。

1. 既存のアプリ サービスを使用するか、 **[Create new Azure App Service]\(新しい Azure App Service を作成する\)** リンクをクリックして新規に作成することができ ます。 ツリービュー内で既存のアプリ サービスを探すには、そのリソース グループを展開するか、 **[表示]** 設定を **[リソースの種類]** に変更して種類で並べ替えます。

   ![アプリ サービスの選択を示すスクリーンショット](media/deploy-app-service/publish-app-service-windows2.png)

1. 新規に作成した場合は、リソース グループとアプリ サービスが Azure 内に生成されます。 名前は、一意であれば、必要に応じて変更できます。

   ![アプリ サービスの作成を示すスクリーンショット](media/deploy-app-service/publish-app-service-windows3.png)

1. 既定のホスティング プランをそのまま使用することも、ホスティング プランを今すぐ、または後で Azure portal 内で変更することもできます。 既定値は、サポートされているリージョンのいずれかにある `S1` (小) です。 ホスティング プランを作成するには、 **[ホスティング プラン]** ドロップダウンの横にある **[新規]** を選択します。 **[ホスティング プラン]** ウィンドウが表示されます。

   ![ホスティング プランのオプションを示すスクリーンショット](media/deploy-app-service/hosting-plan.png)

   これらのオプションの詳細は、「[Azure App Service プランの概要](/azure/app-service/overview-hosting-plans)」で確認できます。

1. これらのリソースの選択または作成が完了したら、 **[完了]** を選択します。 選択したリソース グループとアプリ サービス内でコンテナーが Azure にデプロイされます。 このプロセスには時間が少しばかりかかります。 完了すると、 **[発行]** タブにサイトの URL など、発行したものに関する情報が表示されます。

   ![発行タブのスクリーンショット](media/deploy-app-service/publish-succeeded-windows.png)

1. サイト リンクをクリックし、Azure でアプリが想定どおりに動作することを確認します。

   ![Web アプリケーションのスクリーンショット](media/deploy-app-service/web-application-running2.png)

1. リソース グループやアプリ サービスなど、選択したすべての詳細が含まれる発行プロファイルが保存されます。

1. 同じ発行プロファイルでもう一度デプロイするには、 **[発行]** ボタンか **[Web 発行アクティビティ]** ウィンドウの **[発行]** ボタンを使用するか、**ソリューション エクスプローラー** でプロジェクトを右クリックし、コンテキストメニューで **[発行]** 項目を選択します。
:::moniker-end

## <a name="view-container-settings"></a>コンテナー設定を表示する

[Azure portal](https://portal.azure.com) では、デプロイした App Service を開くことができます。

デプロイした App Service の設定を表示するには、 **[コンテナーの設定]** メニューを開きます (Visual Studio 2019 バージョン 16.4 以降を使用している場合)。

![Azure portal の [コンテナーの設定] メニューのスクリーンショット](media/deploy-app-service/container-settings-menu.png)

そこから、コンテナーの情報を表示したり、ログを表示またはダウンロードしたり、継続的デプロイを設定したりできます。 [Azure App Service 継続的デプロイ CI/CD](/azure/app-service/containers/app-service-linux-ci-cd) に関するページを参照してください。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルに関連付けられている Azure リソースをすべて削除するには、[Azure portal](https://portal.azure.com) を使用してリソース グループを削除します。 発行した Web アプリケーションに関連付けられているリソース グループを見つけるには、 **[表示]** 、 **[その他のウィンドウ]** 、 **[Web 発行アクティビティ]** の順に選択し、歯車アイコンを選択します。 **[発行]** タブが開きます。これにはリソース グループが含まれています。

Azure portal で **[リソース グループ]** をクリックし、リソース グループを選択してその詳細ページを開きます。 リソース グループが間違っていないことを確認し、 **[リソース グループの削除]** を選択し、名前を入力し、 **[削除]** を選択します。

## <a name="next-steps"></a>次の手順

[Azure App Service](/azure/app-service/overview) の詳細を確認します。

## <a name="see-also"></a>関連項目

[Azure Container Registry へのデプロイ](hosting-web-apps-in-docker.md)