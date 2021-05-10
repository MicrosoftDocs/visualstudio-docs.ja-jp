---
title: 接続済みサービスを使用して Azure App Configuration を追加する | Microsoft Docs
description: Visual Studio 接続済みサービスを使用してアプリに Azure 構成サービスの依存関係を追加する
author: ghogen
manager: ''
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 12/11/2020
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 250b89c983da039717982b31873a470172bde0f5
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683283"
---
# <a name="adding-azure-app-configuration-by-using-visual-studio-connected-services"></a>Visual Studio 接続済みサービスを使用して Azure App Configuration を追加する

このチュートリアルでは、Azure App Configuration を使用して Web プロジェクト用の構成と機能フラグを管理するために必要なもののすべてを、Visual Studio で簡単に追加する方法を学習します。 Visual Studio の接続済みサービスの機能を使用することで、Azure 内の App Configuration リソースに接続するために必要なすべてのコード、NuGet パッケージ、構成設定の追加を Visual Studio に自動的に実行させることができます。 この機能を使用するには、Visual Studio 2019 バージョン 16.9 以降を使用している必要があります。

ASP.NET Core、.NET Core コンソール、.NET Framework プロジェクトの App Configuration 接続済みサービス機能を使用できます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac での接続済みサービス](/visualstudio/mac/connected-services)に関するページを参照してください。

## <a name="prerequisites"></a>必須コンポーネント

- Azure のワークロードがインストールされた Visual Studio。
- サポートされている種類のうち 1 つのプロジェクト

## <a name="connect-to-azure-app-configuration-using-connected-services"></a>接続済みサービスを使用して Azure App Configuration に接続する

1. Visual Studio でプロジェクトを開きます。

1. **ソリューション エクスプローラー** で **[接続済みサービス]** ノードを右クリックし、コンテキスト メニューの **[接続済みサービスの追加]** を選択します。

    ![Azure の接続済みサービスを追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. **[接続済みサービス]** タブで、**サービスの依存関係** の [+] アイコンを選択します。

    ![サービスの依存関係を追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. **[依存関係の追加]** ページで、 **[Azure App Configuration]** を選択します。

    ![App Configuration を追加する](./media/vs-azure-tools-connected-services-app-configuration/add-azure-app-configuration.png)

    まだサインインしていない場合は、Azure アカウントにサインインします。 Azure アカウントを持っていない場合、[無料試用版](https://azure.microsoft.com/free/dotnet)でサインアップできます。

1. **[Azure App Configuration の構成]** 画面で、サブスクリプションと既存の構成ストアを選択します。 その後、 **[次へ]** を選択します。

    App Configuration ストアを作成する必要がある場合は、次の手順に進んでください。 それ以外の場合、手順 6. に進みます。

    ![既存の構成アカウントをプロジェクトに追加する](./media/vs-azure-tools-connected-services-app-configuration/select-config-store.png)

1. Azure App Configuration ストアを作成する方法は次のとおりです。

   1. **App Configuration ストア** のヘッダーの右側にある [+] アイコンを選択します。 

   1. **[Azure App Configuration: 新規作成]** ダイアログ ボックスに入力し、 **[作成]** を選択します。 [リソース名] フィールドは一意である必要があることに注意してください。 

       ![新規の Azure アプリ構成ストア](./media/vs-azure-tools-connected-services-app-configuration/create-new-config-store.png)

   1. **[Azure App Configuration]** ダイアログが表示されると、新しい構成ストアが一覧に表示されます。 この新しいストアを選択し、 **[次へ]** を選択します。

1. 接続文字列名を入力して、接続文字列をローカル シークレット ファイルに保存するか、[Azure Key Vault](/azure/key-vault) に格納するかを選択します。

   ![接続文字列を指定する](./media/vs-azure-tools-connected-services-app-configuration/connection-string-app-config.png)

1. **[変更の概要]** 画面には、プロセスを完了した場合にプロジェクトに対して行われるすべての変更が表示されます。 変更が問題ない場合は、 **[完了]** を選択します。

   ![変更の概要](./media/vs-azure-tools-connected-services-app-configuration/summary-of-changes-app-config.png)

1. **依存関係の構成プロセス** が完了すると、Azure App Configuration がプロジェクトの **[サービスの依存関係]** ノードの下に表示されるようになります。

## <a name="next-steps"></a>次のステップ

[Azure App Configuration のドキュメント](/azure/azure-app-configuration/overview)で Azure アプリの構成について学習します。

## <a name="see-also"></a>関連項目

- [動的な構成を App Configuration に接続された ASP.NET Core アプリで使用するためのチュートリアル](/azure/azure-app-configuration/enable-dynamic-configuration-aspnet-core)
- [接続済みサービス (Visual Studio for Mac)](/visualstudio/mac/connected-services)