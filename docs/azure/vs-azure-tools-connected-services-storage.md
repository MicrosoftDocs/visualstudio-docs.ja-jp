---
title: 接続済みサービスを使用して Azure Storage を追加する | Microsoft Docs
description: Visual Studio の接続済みサービスを使用して、Azure Storage サービスの依存関係をアプリに追加します
author: ghogen
manager: jmartens
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 08/13/2020
ms.author: ghogen
ms.openlocfilehash: a2aa5a0453b6a05c261d3cac853ab8265fb4e453
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844347"
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Visual Studio 接続済みサービスを使用した Azure ストレージの追加

Visual Studio では、**接続済みサービス** 機能を使用して、次のいずれかを Azure Storage に接続できます。

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

## <a name="connect-to-azure-storage-using-connected-services"></a>接続済みサービスを使用して Azure Storage に接続する

::: moniker range="vs-2017"

1. Visual Studio でプロジェクトを開きます。

1. **ソリューション エクスプローラー** で **[接続済みサービス]** ノードを右クリックし、コンテキスト メニューの **[接続済みサービスの追加]** を選択します。

    ![Azure の接続済みサービスを追加する](./media/vs-azure-tools-connected-services-storage/add-connected-service.png)

1. **[接続済みサービス]** ページで、**[Azure Storage を使用したクラウド ストレージ]** を選択します。

    ![Azure Storage を追加する](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. **[Azure Storage]** ダイアログで、既存のストレージ アカウントを選択し、**[追加]** をクリックします。

    ストレージ アカウントを作成する必要がある場合は、次の手順に進みます。 それ以外の場合、手順 6. に進みます。

    ![既存のストレージ アカウントをプロジェクトに追加する](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. ストレージ アカウントを作成するには、以下の手順を実行します。

   1. ダイアログの下部にある **[新しいストレージ アカウントを作成します]** を選択します。

   1. **[ストレージ アカウントの作成]** ダイアログに入力し、**[作成]** をクリックします。

       ![新しい Azure ストレージ アカウント](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)

   1. **[Azure Storage]** ダイアログが表示されると、新しいストレージ アカウントが一覧に表示されます。 一覧で新しいストレージ アカウントを選択し、**[追加]** をクリックします。

1. プロジェクトの **[サービス参照]** ノードに、ストレージの接続済みサービスが表示されます。
:::moniker-end

:::moniker range=">=vs-2019"

1. Visual Studio でプロジェクトを開きます。

1. **ソリューション エクスプローラー** で **[接続済みサービス]** ノードを右クリックし、コンテキスト メニューの **[接続済みサービスの追加]** を選択します。

    ![Azure の接続済みサービスを追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. **[接続済みサービス]** タブで、 **[サービスの依存関係]** の [+] アイコンを選択します。

    ![サービスの依存関係を追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. **[依存関係の追加]** ページで、 **[Azure Storage]** を選択します。

    ![Azure Storage を追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/add-azure-storage.png)

    まだサインインしていない場合は、Azure アカウントにサインインします。 Azure アカウントを持っていない場合、[無料試用版](https://azure.microsoft.com/account/free)でサインアップできます。

1. **[Azure Storage の構成]** 画面で、既存のストレージ アカウントを選択し、 **[次へ]** を選択します。

    ストレージ アカウントを作成する必要がある場合は、次の手順に進みます。 それ以外の場合、手順 6. に進みます。

    ![既存のストレージ アカウントをプロジェクトに追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/select-azure-storage-account.png)

1. ストレージ アカウントを作成するには、以下の手順を実行します。

   1. ダイアログの下部にある **[ストレージ アカウントを作成する]** を選択します。

   1. **[Azure Storage: 新規作成]** ダイアログに入力し、 **[作成]** を選択します。

       ![新しい Azure ストレージ アカウント](./media/vs-azure-tools-connected-services-storage/vs-2019/create-storage-account.png)

   1. **[Azure Storage]** ダイアログが表示されると、新しいストレージ アカウントが一覧に表示されます。 一覧で新しいストレージ アカウントを選択し、 **[次へ]** を選択します。

1. 接続文字列名を入力し、接続文字列をローカル シークレット ファイルと [Azure Key Vault](/azure/key-vault) のどちらに保存するかを選択します。

   ![接続文字列を指定する](./media/vs-azure-tools-connected-services-storage/vs-2019/connection-string.png)

1. **[変更の概要]** 画面には、プロセスを完了した場合にプロジェクトに対して行われるすべての変更が表示されます。 変更が問題ない場合は、 **[完了]** を選択します。

   ![変更の概要](./media/vs-azure-tools-connected-services-storage/vs-2019/summary-of-changes.png)

1. プロジェクトの **[サービス参照]** ノードに、ストレージの接続済みサービスが表示されます。
:::moniker-end

## <a name="see-also"></a>関連項目

- [Azure Storage フォーラム](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Azure Storage のドキュメント](/azure/storage/)
- [接続済みサービス (Visual Studio for Mac)](/visualstudio/mac/connected-services)
