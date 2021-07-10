---
title: クラウド エクスプローラーを使用した Azure リソースの管理 | Microsoft Docs
description: クラウド エクスプローラーを使用し、Visual Studio 内で Azure リソースを参照および管理する方法について説明します。
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/25/2017
ms.author: ghogen
ms.openlocfilehash: 775045247cda106d31cf1517e727b9dda5142c4f
ms.sourcegitcommit: 690bfc20744e4b543ee81030a60c8fc6d0d6610f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "113038617"
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Visual Studio Cloud Explorer で Azure アカウントに関連付けられているリソースを管理する

::: moniker range=">=vs-2022"
> [!Important]
> Cloud Explorer は、Visual Studio 2022 では廃止されています。 代わりに、次の代替手段を使用します。
> - Microsoft から提供されている無料のスタンドアロン アプリの [Microsoft Azure Storage Explorer](/azure/vs-azure-tools-storage-manage-with-storage-explorer) を使用します。 Windows、macOS、Linux 上で Azure Storage のデータを視覚的に操作することができます。
> - [Kudu コンソール](https://github.com/projectkudu/kudu/wiki/Kudu-console)は、App Service サーバーとそのファイル システムに直接アクセスするための昇格されたコマンド ライン アクセスを提供します。 これは、重要なデバッグ ツールであると同時に、これでパッケージのインストールなどの CLI 操作を実行できます。
>
> 必要に応じて、Azure Portal を使用するか、サーバー エクスプローラーで以前のバージョンの Visual Studio の Azure ノードを引き続き使用します。
>
> Visual Studio 2022 の詳細については、[リリース ノート](/visualstudio/releases/2022/release-notes-preview/)を参照してください。

::: moniker-end

::: moniker range="<=vs-2019"

Cloud Explorer を使用すると、Azure リソースやリソース グループを表示し、そのプロパティを調べることができます。また、開発者は Visual Studio 内から重要な診断操作を実行できます。

[Azure Portal](https://portal.azure.com) と同様に、Cloud Explorer は Azure Resource Manager スタックを基盤としています。 そのため、Cloud Explorer はリソース (Azure リソース グループなど) と Azure サービス (Logic Apps や API Apps など) を認識し、[ロールベースのアクセス制御](/azure/role-based-access-control/role-assignments-portal) (RBAC) をサポートします。

## <a name="prerequisites"></a>必須コンポーネント

* **Azure ワークロード** を選択した Visual Studio 2017 以降 ([Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads)を参照)。 [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/download/details.aspx?id=51657) を含む Visual Studio の以前のバージョンを使用することもできます。
* Microsoft Azure アカウント - アカウントがない場合は、[無料試用版にサインアップ](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)するか、[Visual Studio サブスクライバー特典を有効](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)にします。

> [!NOTE]
> Cloud Explorer を表示するには、**Ctrl**+**Q** を押し、検索ボックスを有効にし、次いで「**Cloud Explorer**」と入力します。

## <a name="add-an-azure-account-to-cloud-explorer"></a>Cloud Explorer に Azure アカウントを追加する

Azure アカウントに関連付けられているリソースを表示するには、まず、**Cloud Explorer** にアカウントを追加する必要があります。

1. **Cloud Explorer** で **[アカウント管理]** ボタンを選択します。

   ![Cloud Explorer の [Azure アカウントの設定] アイコン](./media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. **[アカウントの管理]** を選択します。

   ![Cloud Explorer のアカウントの追加リンク](./media/vs-azure-tools-resources-managing-with-cloud-explorer/manage-accounts-link.png)

1. 参照するリソースが関連付けられている Azure アカウントにログインします。

1. Azure アカウントにログインすると、そのアカウントに関連付けられているサブスクリプションが表示されます。 参照するアカウント サブスクリプションのチェック ボックスをオンにし、**[適用]** をクリックします。

   ![Cloud Explorer: 表示する Azure サブスクリプションを選択する](./media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. 参照するリソースを含むサブスクリプションを選択すると、**Cloud Explorer** にそれらのサブスクリプションとリソースが表示されます。

   ![Cloud Explorer に一覧表示された Azure アカウントのリソース](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Cloud Explorer から Azure アカウントを削除する

1. **Cloud Explorer** で **[アカウント管理]** を選択します。

   ![[Azure アカウントの設定]](./media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. 削除するアカウントの横にある **[アカウントの管理]** をクリックします。

   ![Remove account](./media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

1. **[削除]** を選択してアカウントを削除します。

    ![Cloud Explorer の [アカウントの管理] ダイアログ ボックス](./media/vs-azure-tools-resources-managing-with-cloud-explorer/accountmanage.PNG)

## <a name="view-resource-types-or-resource-groups"></a>リソースの種類またはリソース グループを表示する

Azure リソースを表示するには、**[リソースの種類]** ビューまたは **[リソース グループ]** ビューを選択します。

1. **Cloud Explorer** で、リソース ビュー ドロップダウンをクリックします。

   ![Cloud Explorer のドロップダウン リストで目的のリソース ビューを選択する](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. コンテキスト メニューで目的のビューを選択します。

   * **[リソースの種類]** ビュー - [Azure Portal](https://portal.azure.com) で使用される一般的なビュー。Web アプリ、ストレージ アカウント、仮想マシンなどの Azure リソースが種類ごとに表示されます。
   * **[リソース グループ]** ビュー - Azure リソースが、関連付けられている Azure リソース グループで分類されます。 リソース グループとは Azure リソースの集まりで、通常は特定のアプリケーションで使用されます。 Azure リソース グループについて詳しくは、「[Azure リソース マネージャーの概要](/azure/azure-resource-manager/resource-group-overview)」をご覧ください。

   次の図では、2 つのリソース ビューを比較しています。

   ![Cloud Explorer のリソース ビューの比較](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Cloud Explorer でリソースを表示し、リソースに移動する

Cloud Explorer で Azure リソースに移動してその情報を表示するには、項目の種類または関連付けられているリソース グループを展開し、リソースを選択します。 リソースを選択すると、Cloud Explorer の下部にある 2 つのタブ (**[アクション]** と **[プロパティ]**) に情報が表示されます。

* **[アクション]** タブ - 選択したリソースに対して Cloud Explorer で実行できるアクションが表示されます。 リソースを右クリックしてコンテキスト メニューを表示することで、これらのオプションを表示することもできます。

* **[プロパティ]** タブ - リソースのプロパティ (種類、ロケール、関連付けられているリソース グループなど) が表示されます。

次の図は、App Service の各タブに表示される内容の比較の例を示しています。

  ![Cloud Explorer のスクリーンショット](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

すべてのリソースには、 **[ポータルで開く]** というアクションがあります。 このアクションを選択すると、選択したリソースが [Azure ポータル](https://portal.azure.com)で表示されます。 **[ポータルで開く]** 機能は、深く入れ子になったリソースに移動する場合に便利です。

その他のアクションやプロパティ値も、Azure リソースに基づいて表示される場合があります。 たとえば、Web Apps と Logic Apps には、**[ポータルで開く]** に加えて、**[ブラウザーで開く]** と **[デバッガーのアタッチ]** というアクションもあります。 エディターを開くアクションは、ストレージ アカウントの BLOB、キュー、またはテーブルを選択すると表示されます。 Azure アプリには **URL** と **状態** プロパティがあるのに対し、ストレージ リソースにはキーと接続文字列のプロパティがあります。

## <a name="find-resources-in-cloud-explorer"></a>Cloud Explorer でリソースを検索する

Azure アカウント サブスクリプションで特定の名前のリソースを検索するには、**Cloud Explorer** の **[検索]** ボックスに名前を入力します。

  ![Finding resources in Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

**検索** ボックスに文字を入力すると、その文字に一致するリソースだけがリソース ツリーに表示されます。

::: moniker-end
