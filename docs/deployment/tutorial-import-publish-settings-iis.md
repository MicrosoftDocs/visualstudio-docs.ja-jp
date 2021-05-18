---
title: 発行設定をインポートして IIS に発行する
description: 発行プロファイルを作成してインポートし、Visual Studio から IIS にアプリケーションを配置します
ms.date: 05/06/2020
ms.topic: tutorial
helpviewer_keywords:
- deployment, publish settings
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aeaaff68ab0abe85838456e8c8b69e2520295689
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729274"
---
# <a name="publish-an-application-to-iis-by-importing-publish-settings-in-visual-studio"></a>Visual Studio で発行設定をインポートしてアプリケーションを IIS に発行する

**[発行]** ツールを使用して、発行設定をインポートしてからアプリを配置することができます。 この記事では、IIS の発行設定を使用していますが、同様の手順を使用して [Azure App Service](../deployment/tutorial-import-publish-settings-azure.md) の発行設定をインポートすることができます。 場合によっては、Visual Studio のインストールごとに IIS への配置を手動で構成するよりも、発行設定プロファイルを使用する方が早い場合があります。

これらの手順は、Visual Studio で ASP.NET、ASP.NET Core、および .NET Core アプリケーションに適用されます。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * 発行設定ファイルを生成できるように IIS を構成する
> * 発行設定ファイルを作成する
> * 発行設定ファイルを Visual Studio にインポートする
> * IIS にアプリを配置する

発行設定ファイル ( *\*.publishsettings*) は、Visual Studio で作成される発行プロファイル ( *\*.pubxml*) とは異なります。 発行設定ファイルは、IIS または Azure App Service を使用して作成するか、手動で作成して Visual Studio にインポートすることができます。

> [!NOTE]
> Visual Studio 発行プロファイル (\*.pubxml ファイル) を Visual Studio のあるインストールから別のインストールにコピーするだけであれば、マネージド プロジェクトの種類の *\\<projectname\>\Properties\PublishProfiles* フォルダー内に発行プロファイル *\<profilename\>.pubxml* があります。 Web サイトについては、 *\App_Data* フォルダー以下を確認してください。 発行プロファイルは MSBuild XML ファイルです。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range=">=vs-2019"

* Visual Studio 2019 をインストールし、**ASP.NET と Web 開発** ワークロードを用意する必要があります。

    Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
::: moniker-end

::: moniker range="vs-2017"

* Visual Studio 2017 をインストールし、ASP.NET と **Web 開発** のワークロードを用意する必要があります。

    Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
::: moniker-end

* サーバーでは Windows Server 2012、Windows Server 2016、または Windows Server 2019 を実行している必要があります。また、発行設定ファイル ( *\*.publishsettings*) を生成するには [IIS Web Server ロール](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)を正しく設定している必要があります。 ASP.NET 4.5 または ASP.NET Core もサーバーにインストールする必要があります。 ASP.NET 4.5 を設定する方法については、「[IIS 8.0 Using ASP.NET 3.5 and ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」 (ASP.NET 3.5 および ASP.NET 4.5 を使用する IIS 8.0) を参照してください。 ASP.NET Core を設定する方法については、「[IIS を使用した Windows での ASP.NET Core のホスト](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)」を参照してください。 ASP.NET Core については、記事で説明されているように、 **[マネージ コードなし]** を使用しするようにアプリケーション プールを構成してください。

## <a name="create-a-new-aspnet-project-in-visual-studio"></a>Visual Studio で新しい ASP.NET プロジェクトを作成する

1. Visual Studio を実行しているコンピューター上で新しいプロジェクトを作成します。

    適切なテンプレートを選択します。 この例では、 **[ASP.NET Web アプリケーション (.NET Framework)]** または (C# の場合のみ) **[ASP.NET Core Web アプリケーション]** を選択し、 **[OK]** を選択します。

    指定したプロジェクト テンプレートが表示されない場合は、 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクに進みます。 Visual Studio インストーラーが起動します。 **ASP.NET と Web 開発** ワークロードをインストールします。

    選択したプロジェクト テンプレート (ASP.NET または ASP.NET Core) は、Web サーバーにインストールされている ASP.NET のバージョンと対応している必要があります。

1. **[MVC]** .(.NET Framework) または **[Web アプリケーション (モデル ビュー コントローラー)]** (.NET Core の場合)、 **[認証なし]** がオンであることを確認してから **[OK]** を選択します。

1. 「**MyWebApp**」のような名前を入力し、 **[OK]** を選択します。

    Visual Studio によってプロジェクトが作成されます。

1. **[ビルド]**  >  **[ソリューションのビルド]** の順に選択して (または、**Ctrl** + **Shift** + **B** キーを押して)、プロジェクトをビルドします。

## <a name="install-and-configure-web-deploy-on-windows-server"></a>Windows Server に Web 配置をインストールして構成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

## <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Windows Server 上の IIS に発行設定ファイルを作成する

[!INCLUDE [create-publish-settings-iis](../deployment/includes/create-publish-settings-iis.md)]

## <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Visual Studio で発行設定をインポートして配置する

[!INCLUDE [import-publish-settings](../deployment/includes/import-publish-settings-vs.md)]

アプリが正常に配置されたら、自動的に起動されます。 Visual Studio から起動しない場合は、IIS でアプリを起動します。 ASP.NET Core の場合、**DefaultAppPool** の [アプリケーション プール] フィールドが **[マネージド コードなし]** に設定されていることを確認する必要があります。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、発行設定ファイルを作成して Visual Studio にインポートし、IIS に ASP.NET アプリを配置しました。 Visual Studio の他の発行オプションの概要を確認することができます。

> [!div class="nextstepaction"]
> [配置でのはじめに](../deployment/deploying-applications-services-and-components.md)
