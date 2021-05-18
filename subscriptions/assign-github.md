---
title: Visual Studio Subscription with GitHub Enterprise を割り当てる | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: f271d623-dcde-442a-865c-4dca5ad8a9c5
ms.date: 03/03/2021
ms.topic: conceptual
description: Visual Studio Subscription with GitHub Enterprise でのサブスクリプションの管理
ms.openlocfilehash: c174b9beb7a7a0eec6bdb65e684869bc0be7dadb
ms.sourcegitcommit: 8da735b586276c95bf566a867655e3464ab1f989
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2021
ms.locfileid: "109740666"
---
# <a name="manage-visual-studio-subscriptions-with-github-enterprise"></a>GitHub Enterprise を使用して Visual Studio サブスクリプションを管理する
Microsoft と Enterprise Agreement (EA) を契約しているお客様は、Visual Studio Standard サブスクリプションと GitHub Enterprise が一体化した、新しいサブスクリプション オファーを購入できます。 この方法により、Visual Studio サブスクライバーは GitHub Enterprise を簡単かつ経済的に入手することができます。 

組織が Visual Studio Subscription with GitHub Enterprise を購入すると、2 つの部分に分かれてプロビジョニングおよび管理されます。

## <a name="manage-visual-studio-subscriptions"></a>Visual Studio サブスクリプションを管理する
組織が Visual Studio Subscription with GitHub Enterprise を購入すると、サブスクリプションの Visual Studio 部分がすぐにプロビジョニングされ、Visual studio の[サブスクリプション管理](https://manage.visualstudio.com)ポータルで割り当てと管理にこれらのサブスクリプションを使用できます。 Visual Studio Subscription with GitHub Enterprise を割り当てると、サブスクライバーは、<https://my.visualstudio.com/subscriptions> で Visual Studio サブスクリプションにアクセスできることを知らせるメールを受け取ります。

Visual Studio サブスクリプションの管理の詳細については、次のトピックを参照してください。
- [管理ポータルの使用](using-admin-portal.md)
- [サブスクリプションを割り当てる](assign-license.md)
- [サブスクリプションの編集](edit-license.md)
- [サブスクリプションの削除](delete-license.md)
- [超過](handle-overclaimed-license.md)

> [!Important]
> Visual Studio Subscription with GitHub Enterprise を、最初に購入せずに Visual Studio サブスクリプション管理者によって割り当てられた場合、GitHub Enterprise アカウントを作成したいという希望は GitHub に通知されません。  Visual Studio Subscription with GitHub Enterprise は、サブスクリプションが割り当てられる前に、**少なくとも 1 つ購入しておく** 必要があります。

## <a name="moving-to-visual-studio-with-github-enterprise"></a>Visual Studio with GitHub Enterprise に移動する
標準の Visual Studio Enterprise および Visual Studio Professional サブスクリプションが割り当てられた後に組織が GitHub Enterprise バンドルで Visual Studio サブスクリプションを購入すると、既存のサブスクライバーを対応する Visual Studio Enterprise with GitHub Enterprise サブスクリプションか Visual Studio Professional with GitHub Enterprise サブスクリプションに移動する目的で役立つ機能が管理ポータルに追加されます。  たとえば、Visual Studio Professional サブスクリプションのサブスクライバーが Visual Studio Professional with GitHub Enterprise サブスクリプションに移動されます。 左側のバーにある [概要] パネルに次のタイルが表示されます。

   > [!div class="mx-imgBorder"]
   > ![[今すぐ移動] ボタン](_img/assign-github/move-now.png "[今すぐ移動] をクリックし、Visual Studio with GitHub Enterprise サブスクリプションにアップグレードする")

> [!IMPORTANT]
> 上記のように、既存のサブスクライバー データ、履歴、サブスクリプション ID が維持されます。また、アクティブにしているベネフィットがこの移動により中断されることはありません。  


**[今すぐ移動]** ボタンをクリックすると、Enterprise および Professional サブスクリプションの移動に関する推奨事項がポップアップ パネルに表示されます。

   > [!div class="mx-imgBorder"]
   > ![ポップアップ パネル](_img/assign-github/fly-out.png)

このタイルでは、影響を受けるサブスクライバーを確認したり、移動完了後、メール通知が届くことを通知するかどうかを指定したりできます。  このメールでは、ベネフィットが変更されないことと、GitHub でプレゼンス設定を始めることを推奨することがサブスクライバーに伝えられます。  

 **[Move subscribers]\(サブスクライバーの移動\)**   ボタンをクリックすると、推奨されるすべてのサブスクライバーを移動することや、一覧から個々のサブスクライバーを選択することができます。  選択内容を確定した後、サブスクリプションの移動が完了するまで数秒かかります。 該当する場合、Professional と Enterprise で別々に以上の手順を行う必要があります。  

## <a name="what-is-the-visual-studio-with-github-enterprise-setup-process"></a>GitHub Enterprise の設定プロセスを使用した Visual Studio とは
GitHub Enterprise は、Visual Studio サブスクリプションとは別に設定され、管理されます。 Visual Studio Subscription with GitHub Enterprise を購入すると、GitHub Enterprise アカウントの設定プロセスが、[manage.visualstudio.com](https://manage.visualstudio.com) での契約と並行して (ただし、個別に) 開始されます。 この GitHub Enterprise アカウントの確立には、時間がかかることがあります。 

会社が GitHub Enterprise アカウントを設定すると、Visual Studio Subscription with GitHub Enterprise が割り当てられているサブスクライバーは、Visual Studio サブスクリプションがリンクされたことを通知する電子メールを GitHub から受け取ります。 電子メールを受信したサブスクライバーは、GitHub 組織の管理者に連絡して、適切な組織への招待を依頼できます。

GitHub Enterprise 設定の詳細については、[サブスクライバー ドキュメント](access-github.md)を参照してください。   

## <a name="manage-github-enterprise-subscriptions"></a>GitHub Enterprise サブスクリプションを管理する
GitHub Enterprise サブスクリプションが購入されると、GitHub ではお客様との連携がなされて、GitHub にアクセスする組織が作成および構成され、管理者が識別されます。  すると、これらの管理者は、管理者として設定されていることを示す通知を受け取ります。  

このプロセスは非常に複雑であるため、サブスクリプションの購入後、組織と管理者が完全に設定されるまで数日かかることがあります。

GitHub は、クラウド ベースの GitHub.com、またはオンプレミスの GitHub Enterprise Server のいずれかとして使用できます。  2 つのバージョンを管理するプロセスは異なります。  GitHub では、GitHub Enterprise サブスクリプションの管理に役立つ、さまざまなヘルプ トピックや管理者ガイドが提供されています。  選択したトピックへのリンクを次に示します。  

## <a name="support-resources"></a>サポート リソース
- GitHub の割り当ての詳細については、[GitHub ドキュメント](https://docs.github.com/en/github/setting-up-and-managing-your-enterprise-account/managing-licenses-for-the-github-enterprise-and-visual-studio-bundle)を参照してください。
- GitHub のさまざまなトピックに関する質問への回答については、[GitHub ヘルプ](https://help.github.com/en)で検索できます。
- [GitHub Community Forum](https://github.community/) で、他の GitHub ユーザーからサポートを得ることができます。
- Visual Studio サブスクリプションの管理については、[Visual Studio サブスクリプション サポート](https://aka.ms/vsadminhelp)にお問い合わせください。
- Visual Studio IDE、Azure DevOps Services、またはその他の Visual Studio の製品やサービスに関する質問がありますか。  [Visual Studio のサポート](https://visualstudio.microsoft.com/support/)にアクセスしてください。
- GitHub Enterprise の[テクニカル サポート](https://support.microsoft.com/supportforbusiness/productselection?sapId=b77fe80f-5417-80bd-4b2a-275cf0018c24)を利用してください。   

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次のステップ
Visual Studio サブスクリプションの管理に関する詳細情報をご覧ください。
- [個別のサブスクリプションの割り当て](assign-license.md)
- [複数のサブスクリプションを管理する](assign-license-bulk.md)
- [サブスクリプションの編集](edit-license.md)
- [サブスクリプションの削除](delete-license.md)
- [最大使用量の確認](maximum-usage.md)

Visual Studio Subscription with GitHub Enterprise の管理の詳細については、Visual Studio の[サブスクリプション管理ポータル](https://visualstudio.microsoft.com/subscriptions-administration/)をご覧ください。