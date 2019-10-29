---
title: ASP.NET Core および React.js での Visual Studio コンテナー ツール
author: ghogen
description: Visual Studio コンテナー ツールと Docker for Windows を使用する方法について説明します
ms.author: ghogen
ms.date: 10/16/2019
ms.technology: vs-azure
ms.topic: quickstart
ms.openlocfilehash: 8083d2d6446c872791501f76cb0167a92a9ef660
ms.sourcegitcommit: 6244689e742e551e7b6933959bd42df56928ece3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72516448"
---
# <a name="quickstart-use-docker-with-a-react-single-page-app-in-visual-studio"></a>クイック スタート: Visual Studio で React シングルページ アプリを含む Docker を使用する

Visual Studio を使用すると、コンテナー化された ASP.NET Core アプリ (React.js シングルページ アプリなどのクライアント側 JavaScript を使用したものを含む) のビルド、デバッグ、実行を簡単に行い、それを Azure Container Registry (ACR)、Docker Hub、Azure App Service、または独自のコンテナー レジストリに発行することができます。 この記事では、ACR に発行します。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、かつ/または **.NET Core クロスプラットフォーム開発**ワークロードがインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
* Azure Container Registry に発行する場合、Azure サブスクリプション。 [無料試用版にサインアップします](https://azure.microsoft.com/offers/ms-azr-0044p/)。
* [Node.js](https://nodejs.org/en/download/)
* Windows コンテナー (Windows 10 バージョン 1903 以降) の場合、この記事で参照されている Docker イメージを使用するため。
::: moniker-end
::: moniker range=">=vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、および/または **.NET Core クロスプラットフォーム開発**ワークロードがインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
* .NET Core 2.2 を使って開発するための [.NET Core 2.2 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/2.2)
* Azure Container Registry に発行する場合、Azure サブスクリプション。 [無料試用版にサインアップします](https://azure.microsoft.com/offers/ms-azr-0044p/)。
* [Node.js](https://nodejs.org/en/download/)
* Windows コンテナー (Windows 10 バージョン 1903 以降) の場合、この記事で参照されている Docker イメージを使用するため。
::: moniker-end

## <a name="installation-and-setup"></a>インストールとセットアップ

Docker をインストールするには、まず、「[Docker Desktop for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)」 (Docker Desktop for Windows: インストール前に知っておくべきこと) の情報を確認します。 次に、[Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows) をインストールします。

## <a name="create-a-project-and-add-docker-support"></a>プロジェクトを作成して Docker サポートを追加する

::: moniker range="vs-2017"
1. **[ASP.NET Core Web アプリケーション]** テンプレートを使って新しいプロジェクトを作成します。
1. **[React.js]** を選択します。 **[Docker サポートを有効にする]** が選択できませんが、心配はいりません。プロジェクトを作成した後にそのサポートを追加できます。

   ![新しい React.js プロジェクトのスクリーンショット](media/container-tools-react/vs2017/new-react-project.png)

1. プロジェクト ノードを右クリックし、 **[追加]** > **[Docker サポート]** を選択して、プロジェクトに Dockerfile を追加します。

   ![Docker サポートの追加](media/container-tools-react/vs2017/add-docker-support.png)

1. コンテナーの種類を選択し、 **[OK]** をクリックします。
::: moniker-end
::: moniker range=">=vs-2019"
1. **[ASP.NET Core Web アプリケーション]** テンプレートを使って新しいプロジェクトを作成します。
1. **[React.js]** を選択して、 **[作成]** をクリックします。 **[Docker サポートを有効にする]** が選択できませんが、心配はいりません。後でそのサポートを追加できます。

   ![新しい React.js プロジェクトのスクリーンショット](media/container-tools-react/vs2019/new-react-project.png)

1. プロジェクト ノードを右クリックし、 **[追加]** > **[Docker サポート]** を選択して、プロジェクトに Dockerfile を追加します。

   ![Docker サポートの追加](media/container-tools-react/vs2017/add-docker-support.png)

1. コンテナーの種類を選択します。
::: moniker-end

次のステップは、Linux コンテナーと Windows コンテナーのどちらを使用しているかによって異なります。

## <a name="modify-the-dockerfile-linux-containers"></a>Dockerfile (Linux コンテナー) を変更する

*Dockerfile* (Docker の最終イメージを作成するためのレシピ) は、プロジェクトで作成されます。 その中に含まれるコマンドの詳細については、「[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)」 (Dockerfile リファレンス) を参照してください。

プロジェクトの *Dockerfile* を開き、コンテナーに Node.js 10.x をインストールするための次の行を追加します。 最初のセクションに必ずこれらの行を追加してください。これにより、後続の手順で使われる基本イメージに、Node パッケージ マネージャー *npm.exe* のインストールが追加されます。

```
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs
```

現在、*Dockerfile* の内容は次のようになっているはずです。

```
FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80 
EXPOSE 443
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs

FROM microsoft/dotnet:2.2-sdk-stretch AS build
WORKDIR /src
COPY ["WebApplication37/WebApplication37.csproj", "WebApplication37/"]
RUN dotnet restore "WebApplication37/WebApplication37.csproj"
COPY . .
WORKDIR "/src/WebApplication37"
RUN dotnet build "WebApplication37.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplication37.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication37.dll"]
```

前の *Dockerfile* は、[microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) イメージに基づいており、プロジェクトをビルドしてコンテナーに追加することで基本イメージを変更するための手順が含まれています。

新しいプロジェクト ダイアログの **[Configure for HTTPS]\(HTTPS 用に構成する\)** チェック ボックスがオンになっている場合、*Dockerfile* は 2 つのポートを公開します。 1 つのポートは HTTP トラフィック用、もう 1 つのポートは HTTPS 用に使用されます。 チェック ボックスがオンになっていない場合は、HTTP トラフィック用に単一のポート (80) が公開されます。

## <a name="modify-the-dockerfile-windows-containers"></a>Dockerfile (Windows コンテナー) を変更する

プロジェクト ノードをダブルクリックしてプロジェクト ファイルを開き、次のプロパティを `<PropertyGroup>` 要素の子として追加して、プロジェクト ファイル (*.csproj) を更新します。

   ```xml
    <DockerfileFastModeStage>base</DockerfileFastModeStage>
   ```

次の行を追加して、Dockerfile を更新します。 これにより、ノードと npm がコンテナーにコピーされます。

   1. Dockerfile の最初の行に ``# escape=` `` を追加します
   1. `FROM … base` の前に、次の行を追加します

      ```
      FROM mcr.microsoft.com/powershell:nanoserver-1903 AS downloadnodejs
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v10.16.3/node-v10.16.3-win-x64.zip"; `
      Expand-Archive nodejs.zip -DestinationPath C:\; `
      Rename-Item "C:\node-v10.16.3-win-x64" c:\nodejs
      ```

   1. `FROM … build` の前と後に、次の行を追加します

      ```
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      ```

   1. 完成した Dockerfile は次のようになります。

      ```
      # escape=`
      #Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
      #For more information, please see https://aka.ms/containercompat
      FROM mcr.microsoft.com/powershell:nanoserver-1903 AS downloadnodejs
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v10.16.3/node-v10.16.3-win-x64.zip"; `
      RUN Expand-Archive nodejs.zip -DestinationPath C:\; `
      RUN Rename-Item "C:\node-v10.16.3-win-x64" c:\nodejs

      FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-nanoserver-1903 AS base
      WORKDIR /app
      EXPOSE 80
      EXPOSE 443
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\

      FROM mcr.microsoft.com/dotnet/core/sdk:2.2-nanoserver-1903 AS build
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      WORKDIR /src
      COPY ["WebApplication7/WebApplication37.csproj", "WebApplication37/"]
      RUN dotnet restore "WebApplication7/WebApplication7.csproj"
      COPY . .
      WORKDIR "/src/WebApplication37"
      RUN dotnet build "WebApplication37.csproj" -c Release -o /app/build

      FROM build AS publish
      RUN dotnet publish "WebApplication37.csproj" -c Release -o /app/publish

      FROM base AS final
      WORKDIR /app
      COPY --from=publish /app/publish .
      ENTRYPOINT ["dotnet", "WebApplication37.dll"]
      ```

1. `**/bin` を削除して、.dockerignore ファイルを更新します。

## <a name="debug"></a>デバッグ

ツールバーのデバッグ ドロップダウンから **[Docker]** を選択し、アプリのデバッグを開始します。 証明書の信頼を求めるメッセージが表示される場合があります。続行するには、証明書を信頼することを選びます。  初めてビルドするときは、Docker によって基本イメージがダウンロードされるため、少し時間がかかることがあります。

**[出力]** ウィンドウの **[コンテナー ツール]** オプションに、実行されているアクションの内容が表示されます。 *npm.exe* に関連付けられたインストール手順が表示されるはずです。

ブラウザーにアプリのホーム ページが表示されます。

::: moniker range="vs-2017"
   ![実行中のアプリのスクリーンショット](media/container-tools-react/vs2017/running-app.png)
::: moniker-end
::: moniker range=">=vs-2019"
   ![実行中のアプリのスクリーンショット](media/container-tools-react/vs2019/running-app.png)
::: moniker-end

*Counter* ページに移動して、 **[Increment]\(インクリメント\)** ボタンをクリックしてカウンターのクライアント側コードをテストしてみてください。

**[ツール]** メニュー、[NuGet パッケージ マネージャー]、 **[パッケージ マネージャー コンソール]** の順に選択して、 **[パッケージ マネージャー コンソール]** (PMC) を開きます。

アプリの結果の Docker イメージは、*dev* としてタグ付けされます。 このイメージは、*microsoft/dotnet* 基本イメージの *2.2-aspnetcore-runtime* タグに基づいています。 **パッケージ マネージャー コンソール** (PMC) ウィンドウで `docker images` コマンドを実行します。 コンピューター上のイメージが表示されます。

```console
REPOSITORY        TAG                     IMAGE ID      CREATED         SIZE
webapplication37  dev                     d72ce0f1dfe7  30 seconds ago  255MB
microsoft/dotnet  2.2-aspnetcore-runtime  fcc3887985bb  6 days ago      255MB
```

> [!NOTE]
> **[デバッグ]** 構成ではボリュームのマウントを使用して、反復編集とデバッグ操作を提供するため、**dev** イメージにはアプリのバイナリやその他のコンテンツは含まれません。 すべてのコンテンツを含む実稼働イメージを作成するには、 **[リリース]** 構成を使用します。

PMC で `docker ps` コマンドを実行します。 アプリがコンテナーを使用して実行されていることがわかります。

```console
CONTAINER ID        IMAGE                  COMMAND               CREATED             STATUS              PORTS                                           NAMES
cf5d2ef5f19a        webapplication37:dev   "tail -f /dev/null"   2 minutes ago       Up 2 minutes        0.0.0.0:52036->80/tcp, 0.0.0.0:44342->443/tcp   priceless_cartwright
```

## <a name="publish-docker-images"></a>Docker イメージの発行

アプリの開発とデバッグのサイクルが完了すると、アプリの実稼働イメージを作成できます。

1. 構成ドロップダウンを **[リリース]** に変更し、アプリを構築します。
1. **ソリューション エクスプローラー**で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
1. 発行先ダイアログで **[コンテナー レジストリ]** タブを選択します。
1. **[新しい Azure コンテナー レジストリを作成する]** を選択し、 **[発行]** をクリックします。
1. **[新しい Azure コンテナー レジストリを作成する]** で、目的の値を入力します。

    | 設定      | 推奨値  | 説明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS プレフィックス** | グローバルに一意の名前 | コンテナー レジストリを一意に識別する名前。 |
    | **サブスクリプション** | サブスクリプションの選択 | 使用する Azure サブスクリプション。 |
    | **[リソース グループ](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  コンテナー レジストリを作成するリソース グループの名前。 新しいリソース グループを作成する場合は、 **[新規]** を選択します。|
    | **[SKU](https://docs.microsoft.com/azure/container-registry/container-registry-skus)** | 標準 | コンテナー レジストリのサービス層  |
    | **レジストリの場所** | 近くの場所 | [[地域]](https://azure.microsoft.com/regions/) で、自分に近いか、またはコンテナー レジストリを使用する他のサービスに近い場所を選択します。 |

    ![Visual Studio の Azure コンテナー レジストリを作成するダイアログ][0]

1. **[作成]** をクリックします。

   ![発行の成功を示すスクリーンショット](media/container-tools/publish-succeeded.png)

## <a name="next-steps"></a>次の手順

これでレジストリからコンテナーを、[Azure Container Instances](/azure/container-instances/container-instances-tutorial-deploy-app) などの Docker イメージを実行できるホストにプルできるようになりました。

## <a name="additional-resources"></a>その他の技術情報

* [Visual Studio によるコンテナー開発](/visualstudio/containers)
* [Docker を使用した Visual Studio 開発のトラブルシューティング](troubleshooting-docker-errors.md)
* [Visual Studio コンテナー ツールの GitHub リポジトリ](https://github.com/Microsoft/DockerTools)

::: moniker range="vs-2017"
[0]:media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png
::: moniker-end
::: moniker range=">=vs-2019"
[0]:media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog-2019.png
::: moniker-end