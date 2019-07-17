---
title: クラウド サブスクリプションの管理者を設定する | Microsoft Docs
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 03/28/2018
ms.topic: conceptual
description: クラウド サブスクリプションの管理者を設定する
ms.openlocfilehash: 85371dd77b99fc5013843bb815082cc0f84cff33
ms.sourcegitcommit: f369ff7e84b0216f01570a486c7be80ca6d0e61a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68250691"
---
# <a name="set-up-administrators-for-visual-studio-cloud-subscriptions"></a>Visual Studio クラウド サブスクリプションの管理者を設定する

Visual Studio Cloud サブスクリプションは管理者によって管理されます。 各管理者は、サブスクリプションの割り当て、割り当ての編集、サブスクリプションの追加または削除、その他のサブスクリプション管理タスクを実行できます。

## <a name="the-azure-subscription-owner-is-the-first-administrator"></a>Azure サブスクリプションの所有者が最初の管理者です。

Visual Studio クラウド サブスクリプションを購入すると、その購入に使用された Azure サブスクリプションの所有者となり、そのサブスクリプションの管理者に自動的に設定されます。

クラウド サブスクリプションを購入するには、[Visual Studio Marketplace](https://marketplace.visualstudio.com/subscriptions) を使用するか、クラウド ソリューション プロバイダーにお問い合わせください。 Visual Studio Marketplace を使用して購入した場合、購入エクスペリエンスの終了時にユーザーの管理を実行できます。 このオプションを選択すると、Visual Studio サブスクリプション管理ポータル ([https://manage.visualstudio.com](https://manage.visualstudio.com)) が表示されます。

サブスクリプションを購入したら、いつでも[管理ポータル](https://manage.visualstudio.com)にアクセスできます。 ポータルにサインインし、左上にある適切な Azure サブスクリプションを選択してください。

クラウド サブスクリプションの購入に使用された Azure サブスクリプションの所有者は、追加の管理者を割り当てることもできます。

## <a name="add-administrators"></a>管理者を追加する

管理者を追加するには:

1. Azure Portal ([portal.azure.com](https://portal.azure.com)) にアクセスします。
2. Visual Studio クラウド サブスクリプションの購入に使用したアカウントでサインインします。
3. 左側のナビゲーション ウィンドウで、 **[コストの管理と請求]** まで下にスクロールします。
4. **[個人用サブスクリプション]** リストで、購入に使用した Azure サブスクリプションを選択します。
5. 左側のナビゲーション ウィンドウのリストの一番上の近くにある **[アクセス制御]** をクリックします。
6. ページの上部にある **[追加]** タブをクリックします。
7. 右側のフライアウト ウィンドウで、管理者にする加入者の名前をクリックします。
8. ウィンドウの一番にある **[ロール]** ドロップダウンをクリックし、下にスクロールして **[ユーザー アクセス管理者]** を選択します。
9. **[保存]** をクリックします。

指定したサブスクライバーがページの中央に表示され、それらのロールは "ユーザー アクセス管理者" と表示されます。

新しい管理者は、[管理ポータル](https://manage.visualstudio.com)にすぐにサインインし、ページの左上のリストからクラウド サブスクリプションの購入に使用したものと同じ Azure サブスクリプションを選択し、それらのサブスクリプションの管理を開始できます。

> [!NOTE]
> 管理者として設定しなかったユーザーが、クラウド サブスクリプションを編集するアクセス権を持っている場合は、基になる Azure サブスクリプションで、サブスクリプションの管理を許可するロールを割り当てられている可能性があります。 そのようなロールとしては、所有者、共同作成者、サービス管理者、共同管理者があります。詳細については、[課金管理者の追加](/azure/devops/organizations/billing/add-backup-billing-managers?view=vsts)に関するページを参照してください。

Visual Studio クラウド サブスクリプションについては、クラウド サブスクリプションの購入に関するページの[概要](vscloud-overview.md)を参照してください。 Visual Studio クラウド サブスクリプションを購入するには、Visual Studio Marketplace ([https://marketplace.visualstudio.com/subscriptions](https://marketplace.visualstudio.com/subscription)) にアクセスしてください。
