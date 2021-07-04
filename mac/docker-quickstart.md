---
title: Docker の概要
description: Visual Studio for Mac でプロジェクトに Docker を追加する方法について説明します
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/09/2020
ms.topic: how-to
ms.openlocfilehash: 4ddb15c8bc5bf90663c5431d2379af61b43e73a6
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2021
ms.locfileid: "112043095"
---
# <a name="get-started-with-docker-in-visual-studio-for-mac"></a>Visual Studio for Mac での Docker の概要

Visual Studio for Mac では、コンテナー化された ASP.NET Core アプリを簡単にビルド、デバッグ、実行し、それを Azure に発行することができます。

## <a name="prerequisites"></a>必須コンポーネント

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
* [Visual Studio for Mac 2019](https://visualstudio.microsoft.com/vs/mac)

## <a name="installation-and-setup"></a>インストールとセットアップ

Docker のインストールについては、「[Install Docker Desktop for Mac (Docker Desktop for Mac をインストールする)](https://docs.docker.com/docker-for-mac/install/)」の情報を確認し、それに従ってください。

## <a name="creating-an-aspnet-core-web-application-and-adding-docker-support"></a>ASP.NET Core Web アプリケーションを作成し、Docker のサポートを追加する

1. **[ファイル] > [新しいソリューション]** に移動して、新しいソリューションを作成します。
1. **[.NET Core] > [アプリ]** で、 **[Web アプリケーション]** テンプレートを選択します。![新しい ASP.NET アプリケーションを作成する](media/docker-quickstart-1.png)
1. ターゲット フレームワークを選択します。 この例では、.NET Core 2.2 を使います。![ターゲット フレームワークを設定する](media/docker-quickstart-2.png)
1. 名前 (この例では _DockerDemo_) など、プロジェクトの詳細を入力します。 作成されるプロジェクトには、ASP.NET Core の Web サイトをビルドして実行するために必要なすべての基本が含まれています。
1. [ソリューション] ウィンドウで DockerDemo プロジェクトを右クリックし、 **[追加]、[Add Docker Support]\(Docker サポートの追加\)** の順に選択します。![Docker サポートの追加](media/docker-quickstart-3.png)

Visual Studio for Mac で、**docker-compose** という名前の新しいプロジェクトがソリューションに自動的に追加され、既存のプロジェクトに **Dockerfile** が追加されます。

![生成された Docker サポート ファイル](media/docker-quickstart-4.png)

## <a name="dockerfile-overview"></a>Dockerfile の概要

Dockerfile は、Docker の最終イメージを作成するためのレシピです。 その中に含まれるコマンドの詳細については、「[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)」 (Dockerfile リファレンス) を参照してください。

```
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY DockerDemo/DockerDemo.csproj DockerDemo/
RUN dotnet restore "DockerDemo/DockerDemo.csproj"
COPY . .
WORKDIR "/src/DockerDemo"
RUN dotnet build "DockerDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerDemo.dll"]
```

前の *Dockerfile* は、[microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) イメージに基づいており、プロジェクトをビルドしてコンテナーに追加することで基本イメージを変更するための手順が含まれています。

> [!NOTE]
> Visual Studio for Mac によって作成される既定の Dockerfile では、HTTP トラフィック用にポート 80 が公開されます。 HTTPS のトラフィックを有効にするには、`Expose 443` を Dockerfile に追加します。

## <a name="debugging"></a>デバッグ

`docker-compose` プロジェクトをスタートアップ プロジェクトとして選択し、デバッグを始めます ( **[実行] > [デバッグの開始]** )。 コンテナー内の ASP.NET プロジェクトがビルド、配置、起動されます。

> [!TIP]
> Docker Desktop をインストールした後の初回実行時には、デバッグしようとすると、次のエラーが表示される可能性があります。`Cannot start service dockerdemo: Mounts denied`
>
> Docker Desktop で [File Sharing]\(ファイル共有\) タブに `/usr/local/share/dotnet/sdk/NuGetFallbackFolder` を追加します。
>
> ![ファイル共有に NuGetFallbackFolder フォルダーを追加する](media/docker-quickstart-5.png)

ビルドが完了すると、アプリケーションが Safari で起動されます。

![Safari で実行されている既定の Docker プロジェクト](media/docker-quickstart-6.png)

コンテナーがポートでリッスンしていることに注意してください。たとえば `http://localhost:32768` などで、ポートはこれと異なる場合があります。

実行中のコンテナーの一覧を表示するには、ターミナルで `docker ps` コマンドを使います。

下のスクリーンショットで、ポートのリレーに注意してください ( **[PORTS]** の下)。 これは、コンテナーは上の Safari で見たポートでリッスンしており、ポート 80 (Dockerfile で定義されているもの) で内部 Web サーバーに要求を中継していることを示します。 アプリケーションの観点からは、ポート 80 でリッスンしています。

![Docker コンテナー リスト](media/docker-quickstart-7.png)
