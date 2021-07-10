---
title: Visual Studio サブスクリプション管理ポータルで基本設定を設定する
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 0fe9eaa4-f589-429e-a443-13bf86637d5a
ms.date: 05/18/2021
ms.topic: conceptual
description: 管理ポータルで言語、連絡先、サブスクリプション レベルなどの基本設定を設定する方法について説明します。
ms.openlocfilehash: 348febd6b964feec54053cff4a3d50cc02eba3d0
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "109983028"
---
# <a name="set-preferences-for-your-agreements-in-the-admin-portal"></a>管理ポータルで契約の基本設定を設定する
スーパー管理者は、各契約に対してグローバルに適用される特定の基本設定を、管理ポータルで設定できます。  これらの基本設定を行うと、管理者がサブスクライバーを追加するときには、その管理者用のサブスクリプションの詳細が自動的に設定されます。また、これらの基本設定は、スーパー管理者だけがグローバルに変更できます。  

## <a name="access-preferences"></a>アクセスの基本設定
基本設定を表示したり、変更したりするには、契約に対してスーパー管理者権限が与えられているサインイン ID を使用し、[管理者ポータル](https://manage.visualstudio.com)にサインインする必要があります。  

基本設定を設定するには:
1. スーパー管理者特権が与えられている ID で管理ポータルにサインインします。
2. 左側のペインにある設定アイコンをクリックします。
   > [!div class="mx-imgBorder"]
   > ![管理者の基本設定ボタン](_img/admin-preferences/admin-preferences-button.png "[管理者の管理] をクリックし、[Agreement Preferences]\(契約の基本設定\) をクリックして基本設定を表示します")

3. **[Agreement Preferences]\(契約の基本設定\)** をクリックします。
左側でパネルが開き、利用できる基本設定が表示されます。 

   > [!div class="mx-imgBorder"]
   > ![管理者の基本設定のポップアップ ダイアログ](_img/admin-preferences/admin-preferences-flyout-2.png "基本設定を設定し、[保存] をクリックします")

## <a name="set-your-preferences"></a>基本設定を設定する
それでは、利用できる基本設定とその効果を 1 つずつ見ていきましょう。 

### <a name="agreement"></a>[契約]
自分がスーパー管理者になっている契約が複数ある場合、展開された設定パネルの右側にあるドロップダウンで目的の契約を選択できます。  設定した基本設定はその契約にのみ適用されます。  個々の管理者はサブスクリプションを割り当てるとき、1 件ごとに基本設定の一部をオーバーライドできます。 

サインインに使用した電子メール アドレスに契約が 1 つだけ割り当てられている場合は、それが展開された設定パネルの右側に表示され、ドロップダウンは無効になります。 

### <a name="contact-email-address"></a>[連絡先の電子メール アドレス]
この基本設定では、サブスクライバー ポータルの [サブスクリプション ページ](https://my.visualstudio.com/subscriptions)にある **[Contact my Admin]\(管理者に問い合わせる\)** ボタンを使用することで、サブスクライバーが管理者に連絡する方法が提供されます。  この基本設定を空のままにした場合、サブスクライバー メッセージは契約のすべての管理者とスーパー管理者に転送されます。  グループ電子メール エイリアスまたはセキュリティ グループを使用し、この連絡先電子メールの受信者を調整することをお勧めします。 必要に応じて、個人の電子メール アドレスを入力することもできます。

> [!NOTE]
> ここに記載する電子メール アドレスはサブスクライバーに表示されません。  サブスクライバーがサブスクライバー ポータルで **[Contact my Admin]\(管理者に問い合わせる\)** 要求を送信すると、メッセージはサブスクライバーに公開されることなく、別名に転送されます。 

### <a name="default-subscription-level"></a>[Default subscription level]\(既定のサブスクリプション レベル\)
この設定を使用すると、サブスクリプションがユーザーに割り当てられるとき、契約に含まれるどのサブスクリプション レベルが既定で選択されるかを決定できます。  管理者は設定を契約内のあらゆるサブスクリプション レベルに変更できます。最も多い選択を繰り返す必要がなくなります。 

### <a name="default-communication-preferences"></a>[Default communication preferences]\(既定のコミュニケーション設定\)
既定のコミュニケーション言語とロケールを設定することで、サブスクリプションを割り当てるプロセスを合理化できます。  たとえば、開発チームが管理者チームとは別の国を拠点にしている場合、サブスクライバーの場所に最も適した基本設定を設定できます。 この設定はすべての管理者がサブスクライバーごとに変更できます。 

### <a name="default-external-subscribers-setting"></a>[Default external subscribers setting]\(既定の外部サブスクライバー設定\)
この基本設定では、管理者が組織のテナント/ディレクトリの外からサブスクライバーを追加できるかどうかを決定できます。  オフにした場合、外部のサブスクライバーは許可されません。  有効にしたとき、管理者が外部のサブスクライバーを追加しようとすると、選択を確定するように求められ、サブスクリプションの割り当てが許可されます。 管理者はこの設定をオーバーライドできません。 

### <a name="default-downloads-setting"></a>[Default downloads setting]\(既定のダウンロード設定\)
既定ではオンになっていますが、この設定を有効になっている場合、管理者が新しいサブスクリプションを作成すると、サブスクライバーはダウンロードにアクセスできます。  依然として管理者はサブスクリプション別にダウンロードを無効にできます。  ダウンロードへのアクセスを無効にすると、プロダクト キーへのアクセスも無効になります。  

### <a name="overallocation-notification"></a>割り当て超過の通知 
契約の割り当てが割り当て超過になったときに電子メールを受け取ることを選択します。 この電子メール通知は [連絡先メール アドレス](admin-preferences.md#contact-email-address) か、連絡先メール アドレスがない場合、契約に登録されているすべての管理者に送信されます。 ドロップ ダウン メニューを使用し、通知のしきい値を設定します。 

 
## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="q--can-i-disable-the-contact-email-address-so-subscribers-cannot-contact-admins"></a>Q:サブスクライバーが管理者に連絡できないように **[連絡先の電子メール アドレス]** を無効にできますか。
A: いいえ。あなたはセキュリティ グループ、グループ電子メール エイリアス、または個々の電子メール アドレスを利用して連絡する管理者を決定できますが、この機能を無効にすることはできません。

### <a name="q-if-i-answer-a-subscribers-email-will-they-have-my-email-address"></a>Q:サブスクライバーの電子メールに返信すると、サブスクライバーに私の電子メール アドレスが表示されますか。
A: 応答はユーザーが使用している電子メール クライアントから届くため、サブスクライバーが受信する応答には、ユーザーが使用している電子メール アドレスが表示されます。  そのため、グループ エイリアスから返信する場合、グループ エイリアスが表示されます。  自分の電子メール アドレスから返信する場合、それが表示されます。  

### <a name="q-where-can-i-find-out-more-about-the-contact-my-admin-feature-in-the-subscriber-portal"></a>Q: **[Contact my Admin]\(管理者に問い合わせる\)** 機能の詳細はサブスクライバー ポータルのどこにありますか。
A: 管理者に連絡する方法に関する記事が[こちら](contact-my-admin.md)にございます。ご覧ください。 

### <a name="q-if-we-dont-complete-the-contact-email-address-and-a-subscriber-uses-the-contact-my-admin-feature-who-receives-their-request"></a>Q: **[連絡先の電子メール アドレス]** に入力していないとき、サブスクライバーが **[Contact my Admin]\(管理者に問い合わせる\)** 機能を使用すると、誰が要求を受け取りますか。
A: **[Contact my Admin]\(管理者に問い合わせる\)** に特定の電子メール アドレスが設定されていない場合、契約のすべての管理者が要求を受け取ります。 

## <a name="resources"></a>リソース
- [Visual Studio の管理とサブスクリプションのサポート](https://aka.ms/vsadminhelp)

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
- [最大使用量の確認](maximum-usage.md)