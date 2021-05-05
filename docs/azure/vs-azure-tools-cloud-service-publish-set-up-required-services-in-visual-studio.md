---
title: クラウド サービスの発行またはデプロイの準備
description: クラウド サービスとストレージ アカウント サービスを設定し、Azure アプリケーションを構成する手順を説明します。
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/10/2017
ms.author: ghogen
ms.openlocfilehash: 06157f1476762af5bfe24ce950e29e80ac60e6b1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844425"
---
# <a name="prepare-to-publish-or-deploy-a-cloud-service-from-visual-studio"></a>Visual Studio からのクラウド サービスの発行またはデプロイの準備

クラウド サービス プロジェクトを発行するには、この記事の説明に従って、次のサービスを設定する必要があります。

* Azure 環境でロールを実行する **クラウド サービス**
* Blob service、Queue サービス、および Table service へのアクセスを提供する **ストレージ アカウント**

## <a name="create-a-cloud-service"></a>クラウド サービスを作成する

クラウド サービスは、Azure 環境でロールを実行します。 次のセクションで説明するように、Visual Studio または [Azure Portal](https://portal.azure.com/) で、クラウド サービスを作成できます。

### <a name="create-a-cloud-service-from-visual-studio"></a>Visual Studio からクラウド サービスを作成する

1. 以前に作成したクラウド サービス プロジェクトで、プロジェクトを右クリックして **[発行]** を選択します。
1. 必要に応じて、Microsoft アカウント、または Azure サブスクリプションに関連付けられている組織のアカウントを使用してサインインし、**[次へ]** を選択して **[設定]** ページに進みます。
1. **[クラウド サービスとストレージ アカウントの作成]** ダイアログが表示されます (表示されない場合は、**[クラウド サービス]** 一覧から **[新規作成]** を選択します)。
1. クラウド サービス名 (大文字と小文字を区別しない) を入力します。この名前は URL の一部となり、一意である必要があります。 さらにリージョンまたはアフィニティ グループを選択し、レプリケーション オプションを選択します。

### <a name="create-a-cloud-service-through-the-azure-portal"></a>Azure Portal を使用してクラウド サービスを作成する

1. [Azure portal](https://portal.azure.com/) にサインインします。
1. ページ左側の **[Cloud Services (クラシック)]** を選択します。
1. **[+ 追加]** を選択し、必要な情報 (DNS 名、サブスクリプション、リソース グループ、および場所) を入力します。 後で Visual Studio で行うため、この時点でパッケージをアップロードする必要はありません。
1. **[作成]** を選択してプロセスを完了します。

## <a name="create-a-storage-account"></a>ストレージ アカウントの作成

ストレージ アカウントを使用すると、Blob service、Queue サービス、および Table service にアクセスできます。 ストレージ アカウントは、Visual Studio または [Azure Portal](https://portal.azure.com/) を使用して作成できます。

### <a name="create-a-storage-account-from-visual-studio"></a>Visual Studio からストレージ アカウントを作成する

1. **ソリューション エクスプローラー** を開き、以前に作成したクラウド サービス プロジェクトで、ロール プロジェクト内の **接続済みサービス** ノードを検索し、右クリックして **[接続済みサービスの追加]** を選択します (Visual Studio 2015 では、**ストレージ** ノードを右クリックして **[ストレージ アカウントの作成]** を選択します)。
1. 表示された **[接続済みサービス]** 一覧で、**[Azure Storage を使用したクラウド ストレージ]** を選択します。
1. 表示された Azure Storage ダイアログで、**[+ 新しいストレージ アカウントの作成]** を選択し、表示されたダイアログで、サブスクリプション、アカウント名、価格レベル、リソース グループ、および場所を指定します。
1. 完了したら **[作成]** を選択します。 サブスクリプションで使用できるストレージ アカウントの一覧に、新しいストレージ アカウントが表示されます。
1. このアカウントを選んで、**[追加]** を選択します。

### <a name="create-a-storage-account-through-the-azure-portal"></a>Azure Portal を使用してストレージ アカウントを作成する

1. [Azure portal](https://portal.azure.com/) にサインインします。
1. 左上の **[+ 新規]** を選択します。
1. "Azure Marketplace" の下の **[ストレージ]** を選択し、右側の **[ストレージ アカウント - Blob、File、Table、Queue]** を選択します。
1. 必要な情報 (名前、デプロイ モデルなど) を入力します。
1. **[作成]** を選択してプロセスを完了します。

## <a name="configure-your-app-to-use-the-storage-account"></a>ストレージ アカウントを使用するようにアプリを構成する

ストレージ アカウントを作成した後、Visual Studio からストレージ アカウントに接続すると、プロジェクトのサービス構成 (URL とアクセス キーを含む) が自動的に更新されます。

**[接続済みサービスの追加]** を使用して Visual Studio からクラウド サービスを作成した場合は、`ServiceConfiguration.Cloud.cscfg` と `ServiceConfiguration.Local.cscfg` を開いて接続を確認できます。

Azure Portal でクラウド サービスを作成した場合は、「[Visual Studio からストレージ アカウントを作成する](#create-a-storage-account-from-visual-studio)」と同じ手順を実行します。ただし、新しいアカウントを作成するのではなく、既存のアカウントを選択します。 Visual Studio によって、構成が更新されます。

手動で設定を構成するには、Visual Studio で、クラウド サービス プロジェクトの適切なロールのプロパティ ページを使用 (ロールを右クリックして **[プロパティ]** を選択) します。 詳細については、「[ストレージ アカウントへの接続文字列の構成](vs-azure-tools-multiple-services-project-configurations.md#configuring-a-connection-string-for-a-storage-account)」をご覧ください。

### <a name="about-access-keys"></a>アクセス キーについて

Azure Portal には、各 Azure Storage サービスのリソースにアクセスするために使用できる URL が表示されます。また、アカウントのプライマリ アクセス キーとセカンダリ アクセス キーも表示されます。 これらのキーは、ストレージ サービスに対する要求を認証するために使用します。

セカンダリ アクセス キーは、プライマリ アクセス キーと同じようにストレージ アカウントにアクセスでき、プライマリ アクセス キーが侵害された場合の予備として生成されます。 また、定期的にアクセスのキーを再生成することをお勧めします。 プライマリ キーの再生成時にセカンダリ キーを使用するように接続文字列の設定を変更した後で、セカンダリ キーの再生成時に再生成したプライマリ キーを使用するように接続文字列の設定を変更できます。

## <a name="next-steps"></a>次のステップ

Visural Studio からの Azure へのアプリ発行の詳細については、「 [Azure Tools を使用したクラウド サービスの発行](vs-azure-tools-publishing-a-cloud-service.md)」を参照してください。
