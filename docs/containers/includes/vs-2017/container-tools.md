---
title: Visual Studio コンテナー ツールと ASP.NET Core
author: ghogen
description: Visual Studio 2017 ツールと Docker for Windows を使用する方法について説明します
ms.author: ghogen
ms.date: 02/01/2019
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: 92b97cb1091722bdf0caa6e7708e015612c545ad
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2021
ms.locfileid: "112044704"
---
Visual Studio を使用すると、コンテナー化された ASP.NET Core アプリを簡単にビルド、デバッグ、および実行して、Azure Container Registry、Docker Hub、Azure App Service、または独自のコンテナー レジストリに発行することができます。 この記事では、コンテナー レジストリに発行します。

## <a name="prerequisites"></a>必須コンポーネント

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、かつ/または **.NET Core クロスプラットフォーム開発** ワークロードがインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
* Azure Container Registry に発行する場合、Azure サブスクリプション。 [無料試用版にサインアップします](https://azure.microsoft.com/free/dotnet/)。

## <a name="installation-and-setup"></a>インストールとセットアップ

Docker をインストールするには、まず、「[Docker Desktop for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)」 (Docker Desktop for Windows: インストール前に知っておくべきこと) の情報を確認します。 次に、[Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows) をインストールします。

## <a name="add-a-project-to-a-docker-container"></a>Docker コンテナーにプロジェクトを追加する

1. Visual Studio のメニューで、 **[ファイル]、[新規作成]、[プロジェクト]** の順に選択します。
1. **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** セクションで、 **[Visual C#]、[Web]** の順に選択します。
1. **[ASP.NET Core Web アプリケーション]** を選択します。または、.NET Core ではなく .NET Framework を使用する場合は、 **[ASP.NET Web アプリケーション]** を選択します。
1. 新しいアプリケーションに名前を設定 (または、既定の名前をそのまま使用) して、 **[OK]** を選択します。
1. **[Web アプリケーション]** を選択します。
1. **[Docker サポートを有効にする]** チェック ボックスをオンにします。

   ![[Enable Docker Support]\(Docker サポートを有効にする\) チェック ボックス](../../media/container-tools/enable-docker-support.PNG)

   このスクリーンショットには .NET Core が表示されています。.NET Framework を使用している場合は、少し異なります。

1. コンテナーの種類 (Windows または Linux) を選択し、 **[OK]** をクリックします。

## <a name="dockerfile-overview"></a>Dockerfile の概要

*Dockerfile* (Docker の最終イメージを作成するためのレシピ) は、プロジェクトで作成されます。 その中に含まれるコマンドの詳細については、「[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)」 (Dockerfile リファレンス) を参照してください。

```
FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 59518
EXPOSE 44364

FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /src
COPY HelloDockerTools/HelloDockerTools.csproj HelloDockerTools/
RUN dotnet restore HelloDockerTools/HelloDockerTools.csproj
COPY . .
WORKDIR /src/HelloDockerTools
RUN dotnet build HelloDockerTools.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish HelloDockerTools.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloDockerTools.dll"]
```

前の *Dockerfile* は、[microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) イメージに基づいており、プロジェクトをビルドしてコンテナーに追加することで基本イメージを変更するための手順が含まれています。 .NET Framework を使用している場合、基本イメージは異なります。

新しいプロジェクト ダイアログの **[Configure for HTTPS]\(HTTPS 用に構成する\)** チェック ボックスがオンになっている場合、*Dockerfile* は 2 つのポートを公開します。 1 つのポートは HTTP トラフィック用、もう 1 つのポートは HTTPS 用に使用されます。 チェック ボックスがオンになっていない場合は、HTTP トラフィック用に単一のポート (80) が公開されます。

## <a name="debug"></a>デバッグ

ツールバーのデバッグ ドロップダウンから **[Docker]** を選択し、アプリのデバッグを開始します。 証明書の信頼を求めるメッセージが表示される場合があります。続行するには、証明書を信頼することを選びます。

**出力** ウィンドウには、行われているアクションの内容が表示されます。

**[ツール]** メニュー、[NuGet パッケージ マネージャー]、 **[パッケージ マネージャー コンソール]** の順に選択して、 **[パッケージ マネージャー コンソール]** (PMC) を開きます。

アプリの結果の Docker イメージは、*dev* としてタグ付けされます。 イメージは、*microsoft/dotnet* 基本イメージの *2.1-aspnetcore-runtime* タグに基づいています。 **パッケージ マネージャー コンソール** (PMC) ウィンドウで `docker images` コマンドを実行します。 コンピューター上のイメージが表示されます。

```console
REPOSITORY        TAG                     IMAGE ID      CREATED         SIZE
hellodockertools  dev                     d72ce0f1dfe7  30 seconds ago  255MB
microsoft/dotnet  2.1-aspnetcore-runtime  fcc3887985bb  6 days ago      255MB
```

> [!NOTE]
> **[デバッグ]** 構成ではボリュームのマウントを使用して、反復編集とデバッグ操作を提供するため、**dev** イメージにはアプリのバイナリやその他のコンテンツは含まれません。 すべてのコンテンツを含む実稼働イメージを作成するには、 **[リリース]** 構成を使用します。

PMC で `docker ps` コマンドを実行します。 アプリがコンテナーを使用して実行されていることがわかります。

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a>Docker イメージの発行

アプリの開発とデバッグのサイクルが完了すると、アプリの実稼働イメージを作成できます。

1. 構成ドロップダウンを **[リリース]** に変更し、アプリを構築します。
1. **ソリューション エクスプローラー** で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
1. 発行先ダイアログで **[コンテナー レジストリ]** タブを選択します。
1. **[新しい Azure コンテナー レジストリを作成する]** を選択し、 **[発行]** をクリックします。
1. **[新しい Azure コンテナー レジストリを作成する]** で、目的の値を入力します。

    | 設定      | 推奨値  | 説明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS プレフィックス** | グローバルに一意の名前 | コンテナー レジストリを一意に識別する名前。 |
    | **サブスクリプション** | サブスクリプションの選択 | 使用する Azure サブスクリプション。 |
    | **[リソース グループ](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  コンテナー レジストリを作成するリソース グループの名前。 新しいリソース グループを作成する場合は、 **[新規]** を選択します。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 標準 | コンテナー レジストリのサービス層  |
    | **レジストリの場所** | 近くの場所 | [[地域]](https://azure.microsoft.com/regions/) で、自分に近いか、またはコンテナー レジストリを使用する他のサービスに近い場所を選択します。 |

    ![Visual Studio の Azure コンテナー レジストリを作成するダイアログ][0]

1. **[作成]**

## <a name="next-steps"></a>次の手順

これでレジストリからコンテナーを、[Azure Container Instances](/azure/container-instances/container-instances-tutorial-deploy-app) などの Docker イメージを実行できるホストにプルできるようになりました。

[0]:../../media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png
