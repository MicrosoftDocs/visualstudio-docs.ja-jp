---
title: ASP.NET Core および React.js での Visual Studio コンテナー ツール
titleSuffix: ''
ms.custom: SEO-VS-2020
author: ghogen
description: Visual Studio コンテナー ツールと Docker を使用してコンテナー化された React による SPA アプリを作成する方法について説明します
ms.author: ghogen
ms.date: 02/21/2021
ms.technology: vs-azure
ms.topic: quickstart
ms.openlocfilehash: 177a44f8af73226d4352c4a48c23c65eadc3e608
ms.sourcegitcommit: 674d3fafa7c9e0cb0d1338027ef419a49c028c36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2021
ms.locfileid: "112602033"
---
# <a name="quickstart-use-docker-with-a-react-single-page-app-in-visual-studio"></a>クイック スタート: Visual Studio で React シングルページ アプリを含む Docker を使用する

Visual Studio を使用すると、コンテナー化された ASP.NET Core アプリ (React.js シングルページ アプリなどのクライアント側 JavaScript を使用したものを含む) のビルド、デバッグ、実行を簡単に行い、それを Azure Container Registry (ACR)、Docker Hub、Azure App Service、または独自のコンテナー レジストリに発行することができます。 この記事では、ACR に発行します。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、かつ/または **.NET Core クロスプラットフォーム開発** ワークロードがインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
* Azure Container Registry に発行する場合、Azure サブスクリプション。 [無料試用版にサインアップします](https://azure.microsoft.com/offers/ms-azr-0044p/)。
* [Node.js](https://nodejs.org/en/download/)
* Windows コンテナー (Windows 10 バージョン 1809 以降) の場合、この記事で参照されている Docker イメージを使用するため。
::: moniker-end
::: moniker range=">=vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、および/または **.NET Core クロスプラットフォーム開発** ワークロードがインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
* .NET Core 3.1 を使って開発するための [.NET Core 3.1 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/3.1)。
* Azure Container Registry に発行する場合、Azure サブスクリプション。 [無料試用版にサインアップします](https://azure.microsoft.com/offers/ms-azr-0044p/)。
* [Node.js](https://nodejs.org/en/download/)
* Windows コンテナー (Windows 10 バージョン 1809 以降) の場合、この記事で参照されている Docker イメージを使用するため。
::: moniker-end

## <a name="installation-and-setup"></a>インストールとセットアップ

Docker をインストールするには、まず、「[Docker Desktop for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)」 (Docker Desktop for Windows: インストール前に知っておくべきこと) の情報を確認します。 次に、[Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows) をインストールします。

## <a name="create-a-project-and-add-docker-support"></a>プロジェクトを作成して Docker サポートを追加する

::: moniker range="vs-2017"
1. **[ASP.NET Core Web アプリケーション]** テンプレートを使って新しいプロジェクトを作成します。
1. **[React.js]** を選択します。 **[Docker サポートを有効にする]** が選択できませんが、心配はいりません。プロジェクトを作成した後にそのサポートを追加できます。

   ![新しい React.js プロジェクトのスクリーンショット](media/container-tools-react/vs-2017/new-react-project.png)

1. プロジェクト ノードを右クリックし、 **[追加]** > **[Docker サポート]** を選択して、プロジェクトに Dockerfile を追加します。

   ![Docker サポートを追加する](media/container-tools-react/vs-2017/add-docker-support.png)

1. コンテナーの種類を選択し、 **[OK]** をクリックします。
::: moniker-end

::: moniker range=">=vs-2019"

1. **[ASP.NET Core with React.js]\(React.js 付きの ASP.NET Core\)** テンプレートを使用して新しいプロジェクトを作成します。

   ![新しい React.js プロジェクトの作成を示すスクリーンショット](media/container-tools-react/vs-2019/create-reactjs-project.png)

1. **[追加情報]** 画面では **[Docker サポートを有効にする]** が選択できませんが、心配はいりません。後でそのサポートを追加できます。

   ![新しい React.js プロジェクトの作成を示すスクリーンショット - [追加情報] 画面](media/container-tools-react/vs-2019/new-react-project-additional-information.png)

1. プロジェクト ノードを右クリックし、 **[追加]** > **[Docker サポート]** を選択して、プロジェクトに Dockerfile を追加します。

   ![Docker サポートを追加する](media/container-tools-react/vs-2017/add-docker-support.png)

1. コンテナーの種類を選択します。
::: moniker-end

次のステップは、Linux コンテナーと Windows コンテナーのどちらを使用しているかによって異なります。

## <a name="modify-the-dockerfile-linux-containers"></a>Dockerfile (Linux コンテナー) を変更する

*Dockerfile* (Docker の最終イメージを作成するためのレシピ) は、プロジェクトで作成されます。 その中に含まれるコマンドの詳細については、「[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)」 (Dockerfile リファレンス) を参照してください。

プロジェクトの *Dockerfile* を開き、コンテナーに Node.js 10.x をインストールするための次の行を追加します。 最初のセクションに必ずこれらの行を追加してください。これにより、基本イメージに、および `build` セクションで、Node パッケージ マネージャー *npm.exe* のインストールが追加されます。

```Dockerfile
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs
```

現在、*Dockerfile* の内容は次のようになっているはずです。

```Dockerfile
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs
WORKDIR /src
COPY ["WebApplication-ReactSPA/WebApplication-ReactSPA.csproj", "WebApplication-ReactSPA/"]
RUN dotnet restore "WebApplication-ReactSPA/WebApplication-ReactSPA.csproj"
COPY . .
WORKDIR "/src/WebApplication-ReactSPA"
RUN dotnet build "WebApplication-ReactSPA.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication-ReactSPA.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication-ReactSPA.dll"]
```

前の *Dockerfile* は、[mcr.microsoft.com/dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) イメージに基づいており、プロジェクトをビルドしてコンテナーに追加することで基本イメージを変更するための手順が含まれています。

新しいプロジェクト ダイアログの **[Configure for HTTPS]\(HTTPS 用に構成する\)** チェック ボックスがオンになっている場合、*Dockerfile* は 2 つのポートを公開します。 1 つのポートは HTTP トラフィック用、もう 1 つのポートは HTTPS 用に使用されます。 チェック ボックスがオンになっていない場合は、HTTP トラフィック用に単一のポート (80) が公開されます。

## <a name="modify-the-dockerfile-windows-containers"></a>Dockerfile (Windows コンテナー) を変更する

プロジェクト ノードをダブルクリックしてプロジェクト ファイルを開き、次のプロパティを `<PropertyGroup>` 要素の子として追加して、プロジェクト ファイル (*.csproj) を更新します。

   ```xml
    <DockerfileFastModeStage>base</DockerfileFastModeStage>
   ```

次の行を追加して、Dockerfile を更新します。 これにより、ノードと npm がコンテナーにコピーされます。

   1. Dockerfile の最初の行に ``# escape=` `` を追加します
   1. `FROM … base` の前に、次の行を追加します

      ```Dockerfile
      FROM mcr.microsoft.com/powershell AS downloadnodejs
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v10.16.3/node-v10.16.3-win-x64.zip"; `
      Expand-Archive nodejs.zip -DestinationPath C:\; `
      Rename-Item "C:\node-v10.16.3-win-x64" c:\nodejs
      ```

   2. `FROM … build` の前と後に、次の行を追加します

      ```Dockerfile
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      ```

   3. 完成した Dockerfile は次のようになります。

      ```Dockerfile
      # escape=`
      #Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
      #For more information, please see https://aka.ms/containercompat
      FROM mcr.microsoft.com/powershell AS downloadnodejs
      RUN mkdir -p C:\nodejsfolder
      WORKDIR C:\nodejsfolder
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v10.16.3/node-v10.16.3-win-x64.zip"; `
      Expand-Archive nodejs.zip -DestinationPath C:\; `
      Rename-Item "C:\node-v10.16.3-win-x64" c:\nodejs

      FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
      WORKDIR /app
      EXPOSE 80
      EXPOSE 443
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\

      FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      WORKDIR /src
      COPY ["WebApplicationReact1/WebApplicationReact1.csproj", "WebApplicationReact1/"]
      RUN dotnet restore "WebApplicationReact1/WebApplicationReact1.csproj"
      COPY . .
      WORKDIR "/src/WebApplicationReact1"
      RUN dotnet build "WebApplicationReact1.csproj" -c Release -o /app/build

      FROM build AS publish
      RUN dotnet publish "WebApplicationReact1.csproj" -c Release -o /app/publish

      FROM base AS final
      WORKDIR /app
      COPY --from=publish /app/publish .
      ENTRYPOINT ["dotnet", "WebApplicationReact1.dll"]
      ```

   4. `**/bin` を削除して、.dockerignore ファイルを更新します。

## <a name="debug"></a>デバッグ

ツールバーのデバッグ ドロップダウンから **[Docker]** を選択し、アプリのデバッグを開始します。 証明書の信頼を求めるメッセージが表示される場合があります。続行するには、証明書を信頼することを選びます。  初めてビルドするときは、Docker によって基本イメージがダウンロードされるため、少し時間がかかることがあります。

**[出力]** ウィンドウの **[コンテナー ツール]** オプションに、実行されているアクションの内容が表示されます。 *npm.exe* に関連付けられたインストール手順が表示されるはずです。

ブラウザーにアプリのホーム ページが表示されます。

::: moniker range="vs-2017"
   ![実行中のアプリのスクリーンショット](media/container-tools-react/vs-2017/running-app.png)
::: moniker-end
::: moniker range=">=vs-2019"
   ![実行中のアプリのスクリーンショット](media/container-tools-react/vs-2019/running-app.png)
::: moniker-end

*Counter* ページに移動して、 **[Increment]\(インクリメント\)** ボタンをクリックしてカウンターのクライアント側コードをテストしてみてください。

**[ツール]** メニュー、[NuGet パッケージ マネージャー]、 **[パッケージ マネージャー コンソール]** の順に選択して、 **[パッケージ マネージャー コンソール]** (PMC) を開きます。

アプリの結果の Docker イメージは、*dev* としてタグ付けされます。 このイメージは、*dotnet/core/aspnet* 基本イメージの *3.1* タグに基づいています。 **パッケージ マネージャー コンソール** (PMC) ウィンドウで `docker images` コマンドを実行します。 コンピューター上のイメージが表示されます。

```console
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
webapplicationreact1                   dev                 09be6ec2405d        2 hours ago         352MB
mcr.microsoft.com/dotnet/core/aspnet   3.1                 e3559b2d50bb        10 days ago         207MB
```

> [!NOTE]
> **[デバッグ]** 構成ではボリュームのマウントを使用して、反復編集とデバッグ操作を提供するため、**dev** イメージにはアプリのバイナリやその他のコンテンツは含まれません。 すべてのコンテンツを含む実稼働イメージを作成するには、 **[リリース]** 構成を使用します。

PMC で `docker ps` コマンドを実行します。 アプリがコンテナーを使用して実行されていることがわかります。

```console
CONTAINER ID        IMAGE                      COMMAND               CREATED             STATUS              PORTS                                           NAMES
56d1b1008c89        webapplicationreact1:dev   "tail -f /dev/null"   2 hours ago         Up 2 hours          0.0.0.0:32771->80/tcp, 0.0.0.0:32770->443/tcp   WebApplication-React1
```

## <a name="publish-docker-images"></a>Docker イメージの発行

アプリの開発とデバッグのサイクルが完了すると、アプリの実稼働イメージを作成できます。

:::moniker range="vs-2017"

1. 構成ドロップダウンを **[リリース]** に変更し、アプリを構築します。
1. **ソリューション エクスプローラー** で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
1. [発行先] ダイアログで **[コンテナー レジストリ]** を選択します。
1. **[新しい Azure コンテナー レジストリを作成する]** を選択し、 **[発行]** をクリックします。
1. **[新しい Azure コンテナー レジストリを作成する]** で、目的の値を入力します。

    | 設定      | 推奨値  | 説明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS プレフィックス** | グローバルに一意の名前 | コンテナー レジストリを一意に識別する名前。 |
    | **サブスクリプション** | サブスクリプションの選択 | 使用する Azure サブスクリプション。 |
    | **[リソース グループ](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  コンテナー レジストリを作成するリソース グループの名前。 新しいリソース グループを作成する場合は、 **[新規]** を選択します。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 標準 | コンテナー レジストリのサービス層  |
    | **レジストリの場所** | 近くの場所 | [[地域]](https://azure.microsoft.com/regions/) で、自分に近いか、またはコンテナー レジストリを使用する他のサービスに近い場所を選択します。 |

    ![Visual Studio の Azure コンテナー レジストリを作成するダイアログ](media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png)

1. **［作成］** を選択します

   ![発行の成功を示すスクリーンショット](media/container-tools/publish-succeeded.png)
:::moniker-end

:::moniker range=">=vs-2019"

1. 構成ドロップダウンを **[リリース]** に変更し、アプリを構築します。
1. **ソリューション エクスプローラー** で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
1. [発行先] ダイアログで **[Docker コンテナー レジストリ]** を選択します。

   ![[Docker コンテナー レジストリ] を選択する](media/container-tools-react/vs-2019/publish-dialog1.png)

1. 次に、 **[Azure Container Registry]** を選択します。

   ![[Azure Container Registry] を選択する](media/container-tools-react/vs-2019/publish-dialog-acr.png)

1. **[新しい Azure コンテナー レジストリを作成する]** を選択します。
1. **[新しい Azure コンテナー レジストリを作成する]** 画面で、目的の値を入力します。

    | 設定      | 推奨値  | 説明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS プレフィックス** | グローバルに一意の名前 | コンテナー レジストリを一意に識別する名前。 |
    | **サブスクリプション** | サブスクリプションの選択 | 使用する Azure サブスクリプション。 |
    | **[リソース グループ](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  コンテナー レジストリを作成するリソース グループの名前。 新しいリソース グループを作成する場合は、 **[新規]** を選択します。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 標準 | コンテナー レジストリのサービス層  |
    | **レジストリの場所** | 近くの場所 | [[地域]](https://azure.microsoft.com/regions/) で、自分に近いか、またはコンテナー レジストリを使用する他のサービスに近い場所を選択します。 |

    ![Visual Studio の Azure コンテナー レジストリを作成するダイアログ](media/container-tools-react/vs-2019/azure-container-registry-details.png)

1. **[作成]** 、 **[完了]** の順に選択します。

   ![新しい ACR を選択または作成する](media/container-tools-react/vs-2019/publish-dialog2.png)

   発行プロセスが終了すると、発行設定を確認し、必要に応じて編集できます。また、 **[発行]** ボタンを使用して、再度イメージを発行することもできます。

   ![発行の成功を示すスクリーンショット](media/container-tools-react/vs-2019/publish-finished.png)

   **[発行]** ダイアログを使用してもう一度開始するには、このページの **[削除]** リンクを使用して発行プロファイルを削除し、 **[発行]** をもう一度クリックします。
:::moniker-end

## <a name="next-steps"></a>次の手順

これでレジストリからコンテナーを、[Azure Container Instances](/azure/container-instances/container-instances-tutorial-deploy-app) などの Docker イメージを実行できるホストにプルできるようになりました。

## <a name="additional-resources"></a>その他の技術情報

* [Visual Studio によるコンテナー開発](./index.yml)
* [Docker を使用した Visual Studio 開発のトラブルシューティング](troubleshooting-docker-errors.md)
* [Visual Studio コンテナー ツールの GitHub リポジトリ](https://github.com/Microsoft/DockerTools)

