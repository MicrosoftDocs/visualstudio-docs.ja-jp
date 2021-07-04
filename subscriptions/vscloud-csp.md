---
title: CSP 向けの Visual Studio クラウド サブスクリプションの購入
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: d2ab13ed-ef79-4ef0-8736-eccd04bc6020
ms.date: 03/18/2021
ms.topic: conceptual
description: クラウド ソリューション プロバイダーが顧客のために Visual Studio クラウド サブスクリプションを購入および管理する方法について説明します。
ms.openlocfilehash: 09c905d113920a0bb55aed8851d3fb62c92a39bf
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2021
ms.locfileid: "112042851"
---
# <a name="buy-and-manage-visual-studio-cloud-subscriptions-for-your-customers"></a>顧客用に Visual Studio クラウド サブスクリプションを購入して管理する
[クラウド ソリューション プロバイダー (CSP)](https://partner.microsoft.com/cloud-solution-provider) プログラムのパートナーは、顧客のために Visual Studio Enterprise クラウド サブスクリプションと Visual Studio Professional クラウド サブスクリプションを購入できます。

[クラウド サブスクリプションのオプションを比較する](https://visualstudio.microsoft.com/vs/pricing)

> [!NOTE]
> Microsoft では、クラウド サブスクリプションの Visual Studio Professional 年間サブスクリプションおよび Visual Studio Enterprise 年間サブスクリプションが提供されなくなりました。 サブスクリプションの更新、増減、キャンセルに関する既存のお客様のエクスペリエンスと機能については変更はありません。 新規のお客様は、[https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/) に移動し、Visual Studio のさまざまな購入オプションを調べることをお勧めします。

## <a name="prerequisites"></a>必須コンポーネント
最初に、パートナー センターで顧客のテナントをセットアップし、そのテナント用の Azure サブスクリプションを作成する必要があります。

[詳細を表示](/azure/devops/organizations/billing/csp/set-up-csp-customer)

## <a name="who-can-buy-visual-studio-subscriptions"></a>Visual Studio サブスクリプションの購入条件
Azure サブスクリプションに対する[所有者または共同作成者アクセス権](https://na01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fvsts%2Forganizations%2Fbilling%2Fadd-backup-billing-managers%3Fview%3Dvsts%2520%2520sa&data=02%7C01%7C%7Cb9e717e8abff47b0cd7e08d618edd860%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636723807145220358&sdata=aIaamEXHhx94KCYVY%2FFibqFzNBEqKPntpql867xAMgU%3D&reserved=0)を持っているユーザーは、だれでも Visual Studio サブスクリプションを購入できます。

## <a name="how-to-buy"></a>購入方法

1. [Microsoft パートナー センター](https://partnercenter.microsoft.com)にログインします。
0. **[Customers]\(顧客\)** を選択し、購入対象の顧客を選びます。
0. **[Service Management]\(サービス管理\)** を選択します。
0. **[Visual Studio Marketplace]** を選択します。
0. 右上隅に顧客の名前が表示されていることを確認します。
0. **[Subscriptions]\(サブスクリプション\)** を選択します。
0. Enterprise for Visual Studio または Professional for Visual Studio を選択します。
0. **[Buy]\(購入\)** を選択します。
0. 購入の請求先の Azure サブスクリプションを選びます。
0. 顧客が必要とするユーザーの数を入力します。
0. 注文を確認して、 **[Confirm]\(確認\)** を選択します。

>[!NOTE]
> CSP として Visual Studio サブスクリプションを購入するたびに、以上の手順に従う必要があります。 現時点では、購入を自動化するための API はありません。

購入を確定した後は、 **[Manage]\(管理\)** を選択して、顧客のエンド ユーザーにサブスクリプションを割り当てることができます。  また、パートナー センターで **[Service management]\(サービス管理\)** を選択して、サブスクリプション管理ポータルにアクセスすることもできます。  それ以降については、以下の手順またはビデオをご覧ください。

## <a name="how-to-manage-visual-studio-cloud-subscriptions-for-your-customer"></a>顧客用に Visual Studio クラウド サブスクリプションを管理する方法

1. [Microsoft パートナー センター](https://partnercenter.microsoft.com)にログインします。
0. **[Customers]\(顧客\)** を選択し、顧客の名前を選びます。
0. **[Service Management]\(サービス管理\)** を選択します。
0. **[Manage Visual Studio Subscriptions]\(Visual Studio サブスクリプションの管理\)** を選択します。

その顧客に複数の Azure サブスクリプションがある場合は、ドロップダウン メニューを使って、購入を行った Azure サブスクリプションを選びます。  **[License Summary]\(ライセンスの概要\)** に、割り当て済みのサブスクリプションの数と、Visual Studio クラウド サブスクリプションのオプションごとに使用可能な数が表示されます。  概要では、サブスクリプションの追加購入や、サブスクリプションの数の削減を行うこともできます。

新しいユーザーにサブスクリプションを割り当てるには、 **[add]\(追加\)** を選択します。  表示されている数が更新され、エンド ユーザーはメール通知を受け取ります。 エンド ユーザーは、提供されたメール アドレスを使って [Visual Studio サブスクライバー ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)にサインインし、Visual Studio サブスクリプションをアクティブ化できます。

Visual Studio サブスクリプションを別のユーザーに割り当て直すには、現在のサブスクライバーを削除した後、新しいサブスクライバーを追加します。

サブスクライバーが自分の Visual Studio サブスクリプションをアクティブ化していない場合は、招待メールを受け取っていないためである可能性があります。  Visual Studio 管理ポータルでは、ユーザーへのアクティブ化招待の再送を Microsoft に要求することもできます。

## <a name="view-visual-studio-pricing-for-csp-partners"></a>CSP パートナー向けの Visual Studio の価格を見る
CSP パートナー向けの Visual Studio の価格を見るには、[パートナー センター](https://partnercenter.microsoft.com)にログインします。  左側のナビゲーションで **[Pricing and offers]\(価格とプラン\)** を選択します。  右上の **[usage-based services]\(使用量ベースのサービス\)** で、今月の価格ファイルを選びます。 Excel スプレッドシートをダウンロードした後、 **[Azure Price List]\(Azure 価格リスト\)** シートを開き、 **[Meter Category]\(メーター カテゴリ\)** 列を **[Visual Studio]** でフィルターします。

このスプレッドシートの見方を次に示します。

| メーター カテゴリ    |   名前                 |  [単位]                                |           内容                          |
|-------------------|------------------------|---------------------------------------|-------------------------------------------------|
| Visual Studio     | エンタープライズ             |  サブスクリプション                         | Visual Studio Enterprise - 月間プラン サブスクリプション   |
| Visual Studio     | 2 次元形式           |  サブスクリプション                         | Visual Studio Professional - 月間プラン サブスクリプション |

月および Visual Studio サブスクリプションの単位で、(特定の顧客が) 購入した 6 番目以降のユニットに 5% の割引がオファーされます。 各サブスクリプション オプションに 2 つの行があるのはそのためです。 1 つの行の [Minimum Value]\(最小値\) は 0 で、これはユニット 1 から 5 が基準価格であることを示します。 もう 1 つの行の [Minimum Value]\(最小値\) は 5 で、ユニット 6 以上に適用される 5% の割引価格を示します。

## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="q-how-are-monthly-cloud-subscription-charges-processed"></a>Q:**月間プラン** のクラウド サブスクリプション料金はどのように処理されますか。
A: 最初の購入時は、現在の月の残りの日数をカバーする日割り計算された数量を請求します。 たとえば、10 個の Visual Studio Professional クラウド サブスクリプション月間プランを 4 月 15 日に購入した場合、30 日の月のうち 15 日、つまり 50% が残っており、ユニットの 50% が日割り計算されるため、5 ユニット分が請求されます。 5 月 1 日およびそれ以降は毎月、ユーザーがキャンセルするまで、10 ユニット分が請求されます。

後で支払い数量を増やした場合も、現在の月の残りの日数について、増加ユニット分が日割りで請求されます。 したがって、1 個の Visual Studio Professional クラウド サブスクリプション月間プランを 5 月 10 日に追加購入した場合は、約 0.677 ユニット (5 月の 31 日間の残り 21 日分) が請求されます。

### <a name="q-how-do-cancellations-work"></a>Q:キャンセルはどのように行われますか。
A: Visual Studio クラウド サブスクリプションをキャンセルすると、自動更新がキャンセルされます。 サブスクリプションは通常の更新日まで継続した後、単に期限切れになります。 期限が切れると、Visual Studio サブスクライバーは、Visual Studio またはサブスクリプションからの他のすべての特典を使用できなくなります。

クラウド サブスクリプション月間プランでは、キャンセルは次の月の最初の日に有効になります。 顧客のクラウド サブスクリプション月間プランの一部だけをキャンセルする場合は、次の月の最初の日にユーザーを削除し、適切なユーザーが引き続きアクティブなサブスクリプションを割り当てられるようにしてください。

クラウド サブスクリプション年間プランの場合は、元の購入または最後の年間更新請求から 12 か月が経過した後の月の最初の日に有効になります。 たとえば、2018 年 1 月 3 日に Visual Studio Enterprise クラウド サブスクリプション年間プランを購入した場合、2019 年 2 月 1 日に次の年に自動的に更新されるまで、サブスクリプションはアクティブです。 2019 年 2 月 1 日から 2020 年 2 月 1 日までの間にキャンセルした場合、サブスクリプションは 2020 年 2 月 1 日に期限切れになります。 クラウド サブスクリプション年間プランのサブスクリプション年の途中でキャンセルした場合の払い戻しはありません。

### <a name="q-what-kind-of-volume-discounts-are-available-for-visual-studio-subscriptions"></a>Q:Visual Studio サブスクリプションに対してはどのようなボリューム ディスカウントを利用できますか。
A: サブスクリプションの *各タイプ内* で 6 番目以降のすべてのサブスクリプションについて、5% の割引を得られます。
- Visual Studio Professional - 月間プラン
- Visual Studio Enterprise - 月間プラン

たとえば、6 個の Visual Studio Professional サブスクリプション月間プランと 5 個の Visual Studio Enterprise サブスクリプション月間プランを購入した場合、5 個の Professional サブスクリプションは通常料金、6 番目の Professional サブスクリプションは 5% のディスカウント料金、5 個の Enterprise サブスクリプションはすべて通常料金のお支払いになります。

また、割引は、特定の月単位の請求期間内の料金に対してのみ適用されます。 したがって、ある月に 5 個の Visual Studio Professional サブスクリプション年間プランを購入し、次の月にさらに 5 個追加購入した場合、10 個のサブスクリプションすべてについて通常料金のお支払いになります。

これらの割引は、[パートナー センター](https://partnercenter.microsoft.com)の価格データに反映されます。

### <a name="q-are-there-renewal-discounts"></a>Q:更新時には割引はありますか。
A: いいえ、Visual Studio サブスクリプションの価格は一定です。 新規サブスクリプションも継続サブスクリプションも同じ価格です。

### <a name="q-are-there-azure-devtest-pricing-options-for-csps"></a>Q:CSP には Azure 開発/テスト価格オプションがありますか。
A: 現時点ではありません。 顧客には [Azure 開発/テスト価格](https://azure.microsoft.com/pricing/dev-test/)の特典がありますが、CSP に対しては特に何もありません。

## <a name="resources"></a>リソース
- Visual Studio サブスクリプションの販売、サブスクリプション、アカウント、課金のサポートについては、Visual Studio [サブスクリプション サポート](https://aka.ms/vssubscriberhelp)をご覧ください。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次の手順
請求に関する一般的な質問の回答については、[クラウドの請求に関してよくあるご質問](vscloud-billing-faq.yml)に関するページを参照してください。