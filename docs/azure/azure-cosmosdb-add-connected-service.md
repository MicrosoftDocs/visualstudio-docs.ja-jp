---
title: 接続済みサービスを使用して Azure Cosmos DB を追加する | Microsoft Docs
description: Visual Studio を使用して接続済みサービスを追加することによって、Azure Cosmos DB のサポートをアプリに追加します
author: AngelosP
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: 070c1e77559e33ac398730b1bafc5a4a86825cda
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841185"
---
# <a name="add-azure-cosmos-db-to-your-app-by-using-visual-studio-connected-services"></a>Visual Studio の接続済みサービスを使用して Azure Cosmos DB をアプリに追加する

Visual Studio では、**接続済みサービス** 機能を使用して、次のいずれかを Azure Cosmos DB に接続できます。

- .NET Framework コンソール アプリ
- ASP.NET MVC (.NET Framework) 
- ASP.NET Core
- .NET Core (コンソール アプリ、WPF、Windows フォーム、クラス ライブラリを含む)
- .NET Core Worker ロール
- Azure Functions
- ユニバーサル Windows プラットフォーム アプリ
- Xamarin
- Cordova

接続済みサービス機能により、必要なすべての参照と接続コードがプロジェクトに追加され、構成ファイルが適切に変更されます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac での接続済みサービス](/visualstudio/mac/connected-services)に関するページを参照してください。
## <a name="prerequisites"></a>必須コンポーネント

- Azure ワークロードがインストールされている Visual Studio
- サポートされているいずれかの種類のプロジェクト

## <a name="connect-to-azure-cosmos-db-using-connected-services"></a>接続済みサービスを使用して Azure Cosmos DB に接続する

1. Visual Studio でプロジェクトを開きます。

1. **ソリューション エクスプローラー** で **[接続済みサービス]** ノードを右クリックし、コンテキスト メニューの **[接続済みサービスの追加]** を選択します。

1. **[接続済みサービス]** タブで、 **[サービスの依存関係]** の [+] アイコンを選択します。

    ![サービスの依存関係を追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. **[依存関係の追加]** ページで、 **[Azure Cosmos DB]** を選択します。

    ![Azure Cosmos DB を追加する](./media/azure-cosmosdb-add-connected-service/azure-cosmosdb.png)

    まだサインインしていない場合は、Azure アカウントにサインインします。 Azure アカウントを持っていない場合、[無料試用版](https://azure.microsoft.com/account/free)でサインアップできます。

1. **[Azure Cosmos DB]** 画面で、既存の Azure Cosmos DB を選択し、 **[次へ]** を選択します。

    データベースを作成する必要がある場合は、次の手順に進みます。 それ以外の場合は、手順 7 に進みます。

    ![既存の Cosmos DB をプロジェクトに追加する](./media/azure-cosmosdb-add-connected-service/created-cosmosdb.png)

1. Azure Cosmos DB を作成するには:

   1. 画面の下部にある **[新しい Azure Cosmos DB の作成]** を選択します。

   1. **[Azure Cosmos DB: 新規作成]** 画面に入力し、 **[作成]** を選択します。

       ![新しい Azure Cosmos DB](./media/azure-cosmosdb-add-connected-service/create-new-cosmosdb.png)

   1. **[Azure Cosmos DB の構成]** ダイアログが表示されると、新しいデータベースが一覧に表示されます。 一覧で新しいデータベースを選択し、 **[次へ]** を選択します。

1. 接続文字列名を入力し、接続文字列をローカル シークレット ファイルと [Azure Key Vault](/azure/key-vault) のどちらに保存するかを選択します。

   ![接続文字列を指定する](./media/azure-cosmosdb-add-connected-service/connection-string.png)

1. **[変更の概要]** 画面には、プロセスを完了した場合にプロジェクトに対して行われるすべての変更が表示されます。 変更が問題ない場合は、 **[完了]** を選択します。

   ![変更の概要](./media/azure-cosmosdb-add-connected-service/summary-of-changes.png)

1. 接続は、 **[接続済みサービス]** タブの **[サービスの依存関係]** セクションに表示されます。

   ![サービスの依存関係](./media/azure-cosmosdb-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>関連項目

- [Azure Cosmos DB 製品ページ](https://azure.microsoft.com/services/cosmos-db/)
- [Azure Cosmos DB のドキュメント](/azure/cosmos-db/)
- [接続済みサービス (Visual Studio for Mac)](/visualstudio/mac/connected-services)
