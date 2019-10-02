---
title: ASP.NET Docker コンテナーを ACR レジストリにデプロイする
description: Visual Studio コンテナー ツールを使用し、ASP.NET Core Web アプリをコンテナー レジストリにデプロイする方法を説明します
author: ghogen
manager: jillfra
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.devlang: dotnet
ms.topic: conceptual
ms.technology: vs-azure
ms.date: 03/14/2019
ms.author: ghogen
ms.openlocfilehash: b3b012bfe3b9fc359a8c9688c52aa5bfc27fd2c7
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "71126143"
---
# <a name="deploy-an-aspnet-container-to-a-container-registry-using-visual-studio"></a>Visual Studio を使用して ASP.NET Docker コンテナーをコンテナー レジストリにデプロイする

## <a name="overview"></a>概要

Docker は軽量のコンテナー エンジンで、アプリケーションとサービスをホストするために使用できる仮想マシンにいくつかの点で似ています。
このチュートリアルでは、Visual Studio を使用して、コンテナー化されたアプリケーションを [Azure Container Registry](https://azure.microsoft.com/services/container-registry) に発行する方法について説明します。

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/dotnet/?utm_source=acr-publish-doc&utm_medium=docs&utm_campaign=docs) を作成してください。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを完了するには、次のものが必要です。

::: moniker range="vs-2017"
* "ASP.NET および Web 開発" ワークロードと共に、最新バージョンの [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) をインストールする
::: moniker-end
::: moniker range=">=vs-2019"
* "ASP.NET および Web 開発" ワークロードと共に、最新バージョンの [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) をインストールする
::: moniker-end
* [Docker for Windows](https://docs.docker.com/docker-for-windows/install/) をインストールする

## <a name="create-an-aspnet-core-web-app"></a>ASP.NET Core Web アプリを作成する
次の手順では、このチュートリアルで使用する基本的な ASP.NET Core アプリの作成について説明します。

::: moniker range="vs-2017"
[!INCLUDE [create-aspnet5-app](../azure/includes/create-aspnet5-app.md)]
::: moniker-end
::: moniker range=">=vs-2019"
[!INCLUDE [create-aspnet5-app](../azure/includes/vs-2019/create-aspnet5-app-2019.md)]
::: moniker-end

## <a name="publish-your-container-to-azure-container-registry"></a>Azure Container Registry へのコンテナーの発行
1. **ソリューション エクスプローラー**で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
2. 発行先ダイアログで **[コンテナー レジストリ]** タブを選択します。
3. **[New Azure Container Registry]\(新しい Azure コンテナー レジストリ)** を選択し、 **[発行]** をクリックします。
4. **[新しい Azure コンテナー レジストリを作成する]** で、目的の値を入力します。

    | 設定      | 推奨値  | 説明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS プレフィックス** | グローバルに一意の名前 | コンテナー レジストリを一意に識別する名前。 |
    | **サブスクリプション** | サブスクリプションの選択 | 使用する Azure サブスクリプション。 |
    | **[リソース グループ](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  コンテナー レジストリを作成するリソース グループの名前。 新しいリソース グループを作成する場合は、 **[新規]** を選択します。|
    | **[SKU](https://docs.microsoft.com/azure/container-registry/container-registry-skus)** | 標準 | コンテナー レジストリのサービス層  |
    | **レジストリの場所** | 近くの場所 | [[地域]](https://azure.microsoft.com/regions/) で、自分に近いか、またはコンテナー レジストリを使用する他のサービスに近い場所を選択します。 |

    ![Visual Studio の Azure コンテナー レジストリを作成するダイアログ](media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png)

5. **[作成]**

これでレジストリからコンテナーを、[Azure Container Instances](/azure/container-instances/container-instances-tutorial-deploy-app) などの Docker イメージを実行できるホストにプルできるようになりました。
