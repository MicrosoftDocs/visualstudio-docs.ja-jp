---
title: Azure SQL Database に接続を追加する | Microsoft Docs
description: Visual Studio 接続済みサービスを使用してアプリに Azure SQL Database 接続を追加する
author: AngelosP
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: 26a01bfe2a34422f9596710f832a1c4af699fd3b
ms.sourcegitcommit: 3fe04d5b931ae459a802a1b965f84186757cbc08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2021
ms.locfileid: "111588489"
---
# <a name="add-a-connection-to-azure-sql-database"></a>Azure SQL Database に接続を追加する

Visual Studio では、**接続済みサービス** 機能を使用して、次のサービスを Azure SQL データベースに接続できます。

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
- サポートされている種類のうち 1 つのプロジェクト

## <a name="connect-to-azure-sql-database-using-connected-services"></a>接続済みサービスを使用して Azure SQL Database に接続する

1. Visual Studio でプロジェクトを開きます。

1. **ソリューション エクスプローラー** で **[接続済みサービス]** ノードを右クリックし、コンテキスト メニューの **[接続済みサービスの追加]** を選択します。

1. **[接続済みサービス]** タブで、 **[サービスの依存関係]** の [+] アイコンを選択します。

    ![サービスの依存関係を追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. **[依存関係の追加]** ページで、 **[Azure SQL Database]** を選択します。

    ![Azure SQL Database サービスを追加する](./media/azure-sql-database-add-connected-service/azure-sql-database.png)

    まだサインインしていない場合は、Azure アカウントにサインインします。 Azure アカウントを持っていない場合、[無料試用版](https://azure.microsoft.com/account/free)でサインアップできます。

1. **[Azure SQL Database の構成]** 画面で、既存の Azure SQL Database を選択し、 **[次へ]** を選択します。

    新しいコンポーネントを作成する必要がある場合は、次の手順に進みます。 それ以外の場合は、手順 7 に進みます。

    ![既存の Azure SQL Database コンポーネントに接続する](./media/azure-sql-database-add-connected-service/created-azure-sql-database.png)

1. Azure SQL Database を作成する方法は次のとおりです。

   1. 画面の下部にある **[SQL Database の作成]** を選択します。

   1. **[Azure SQL Database: 新規作成]** 画面で、 **[作成]** を選択します。

       ![新規の Azure SQL Database](./media/azure-sql-database-add-connected-service/create-new-azure-sql-database.png)

   1. **[Azure SQL Database の構成]** 画面が表示されたら、新しいデータベースが一覧に表示されます。 一覧の中から新しいデータベースを選択し、 **[次へ]** を選択します。

1. 接続文字列名を入力するか、既定値を選択して、接続文字列をローカル シークレット ファイルに保存するか、[Azure Key Vault](/azure/key-vault) に格納するかを選択します。

   ![接続文字列を指定する](./media/azure-sql-database-add-connected-service/connection-string.png)

1. **[変更の概要]** 画面には、プロセスを完了した場合にプロジェクトに対して行われるすべての変更が表示されます。 変更が問題ない場合は、 **[完了]** を選択します。

   ![変更の概要](./media/azure-sql-database-add-connected-service/summary-of-changes.png)

   ファイアウォール規則の設定を求めるダイアログが表示されたら、 **[はい]** を選択します。

   ![ファイアウォール規則](./media/azure-sql-database-add-connected-service/firewall-rules.png)

1. 接続は、 **[接続済みサービス]** タブの **[サービスの依存関係]** セクションに表示されます。

   ![サービスの依存関係](./media/azure-sql-database-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>関連項目

- [Azure SQL Database 製品ページ](https://azure.microsoft.com/services/sql-database/)
- [Azure SQL Database のドキュメント](/azure/azure-sql/database/)
- [接続済みサービス (Visual Studio for Mac)](/visualstudio/mac/connected-services)
