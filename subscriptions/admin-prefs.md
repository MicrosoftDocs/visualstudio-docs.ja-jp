---
title: 管理ポータルで契約の基本設定を設定する
author: evanwindom
ms.author: lank
manager: lank
ms.date: 08/21/2019
ms.topic: conceptual
description: 管理ポータルで言語、連絡先、サブスクリプション レベルなどの基本設定を設定する方法について説明します。
ms.openlocfilehash: 24e9ddfa92ee63e4d15eea086224e1069d4bcbc8
ms.sourcegitcommit: c90a998716b3dfa614dedc61a1bea515364efbec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000982"
---
# <a name="set-preferences-for-your-agreements-in-the-administration-portal"></a>管理ポータルで契約の基本設定を設定する
スーパー管理者は、各契約に対してグローバルに適用される管理ポータルで特定の基本設定を設定できるようになりました。  この基本設定により、契約の管理者がサブスクライバーを追加するときに設定できるものが決定されます。この基本設定はスーパー管理者だけがグローバルで変更できます。  

## <a name="access-preferences"></a>アクセスの基本設定
基本設定を表示したり、変更したりするには、契約に対してスーパー管理者権限が与えられているサインイン ID を使用し、[管理者ポータル](https://manage.visualstudio.com)にサインインする必要があります。  

基本設定を設定するには:
1. スーパー管理者特権が与えられている ID で管理ポータルにサインインします。
2. **[管理者の管理]** タブをクリックします。
   > [!div class="mx-imgBorder"]
   > ![管理者の基本設定ボタン](_img/admin-prefs/admin-prefs-button.png)

3. **[Agreement Preferences]\(契約の基本設定\)** をクリックします。
右側でパネルが開き、利用できる基本設定が表示されます。 

   > [!div class="mx-imgBorder"]
   > ![管理者の基本設定のポップアップ ダイアログ](_img/admin-prefs/admin-prefs-flyout.png)

## <a name="set-your-preferences"></a>基本設定を設定する
それでは、利用できる基本設定とその効果を 1 つずつ見ていきましょう。 

### <a name="agreement"></a>[契約]
自分がスーパー管理者になっている契約が複数ある場合、ドロップダウンで目的の契約を選択できます。  設定した基本設定はその契約にのみ適用されます。  個々の管理者はサブスクリプションを割り当てるとき、1 件ごとに基本設定の一部をオーバーライドできます。 

サインインに使用した電子メール アドレスに契約が 1 つだけ割り当てられている場合、その契約が表示され、ドロップダウンが無効になります。 

### <a name="contact-email-address"></a>[連絡先の電子メール アドレス]
この基本設定では、サブスクライバー ポータルの[サブスクリプション ページ](https://my.visualstudio.com/subscriptions)にある **[Contact my Admin]\(管理者に問い合わせる\)** ボタンを使用することでサブスクライバーが管理者に連絡する方法が提供されます。  この基本設定を空のままにした場合、サブスクライバー メッセージは契約のすべての管理者とスーパー管理者に転送されます。  グループ電子メール エイリアスまたはセキュリティ グループを使用し、この連絡先電子メールの受信者を調整することをお勧めします。 必要に応じて、個人の電子メール アドレスを入力することもできます。

> [!NOTE]
> ここに記載する電子メール アドレスはサブスクライバーに表示されません。  サブスクライバーがサブスクライバー ポータルで **[Contact my Admin]\(管理者に問い合わせる\)** 要求を送信すると、メッセージはサブスクライバーに公開されることなく、エイリアスに転送されます。 

### <a name="default-external-subscribers-setting"></a>[Default external subscribers setting]\(既定の外部サブスクライバー設定\)
この基本設定では、管理者が組織のテナント/ディレクトリの外からサブスクライバーを追加できるかどうかを決定できます。  オフにした場合、外部のサブスクライバーは許可されません。  有効にしたとき、管理者が外部のサブスクライバーを追加しようとすると、選択を確定するように求められ、サブスクリプションの割り当てが許可されます。 管理者はこの設定をオーバーライドできません。 

### <a name="default-downloads-setting"></a>[Default downloads setting]\(既定のダウンロード設定\)
既定ではオンになっていますが、この設定を有効になっている場合、管理者が新しいサブスクリプションを作成すると、サブスクライバーはダウンロードにアクセスできます。  依然として管理者はサブスクリプション別にダウンロードを無効にできます。  

### <a name="default-subscription-level"></a>[Default subscription level]\(既定のサブスクリプション レベル\)
この設定を使用すると、サブスクリプションがユーザーに割り当てられるとき、契約に含まれるどのサブスクリプション レベルが既定で選択されるかを決定できます。  管理者は設定を契約内のあらゆるサブスクリプション レベルに変更できます。最も多い選択を繰り返す必要がなくなります。 

### <a name="default-communication-preferences"></a>[Default communication preferences]\(既定のコミュニケーション設定\)
既定のコミュニケーション言語とロケールを設定することで、サブスクリプションを割り当てるプロセスを合理化できます。  たとえば、開発チームが管理者チームとは別の国を拠点にしている場合、サブスクライバーの場所に最も適した基本設定を設定できます。 この設定はすべての管理者がサブスクライバーごとに変更できます。 

## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="q--can-i-disable-the-contact-email-address-so-subscribers-cannot-contact-administrators"></a>Q:サブスクライバーが管理者に連絡できないように **[連絡先の電子メール アドレス]** を無効にできますか。
A: いいえ。あなたはセキュリティ グループ、グループ電子メール エイリアス、または個々の電子メール アドレスを利用して連絡する管理者を決定できますが、この機能を無効にすることはできません。

### <a name="q-if-i-answer-a-subscribers-email-will-they-have-my-email-address"></a>Q:サブスクライバーの電子メールに返信すると、サブスクライバーに私の電子メール アドレスが表示されますか。
A: 応答はユーザーが使用している電子メール クライアントから届くため、サブスクライバーが受信する応答には、ユーザーが使用している電子メール アドレスが表示されます。  そのため、グループ エイリアスから返信する場合、グループ エイリアスが表示されます。  自分の電子メール アドレスから返信する場合、それが表示されます。  

### <a name="q-where-can-i-find-out-more-about-the-contact-my-admin-feature-in-the-subscriber-portal"></a>Q: **[Contact my Admin]\(管理者に問い合わせる\)** 機能の詳細はサブスクライバー ポータルのどこにありますか。
A: 管理者に連絡する方法に関する記事が[こちら](contact-my-admin.md)にございます。ご覧ください。 

### <a name="q-if-we-dont-complete-the-contact-email-address-and-a-subscriber-uses-the-contact-my-admin-feature-who-receives-their-request"></a>Q: **[連絡先の電子メール アドレス]** に入力していないとき、サブスクライバーが **[Contact my Admin]\(管理者に問い合わせる\)** 機能を使用すると、誰が要求を受け取りますか。
A: **[Contact my Admin]\(管理者に問い合わせる\)** に特定の電子メール アドレスが設定されていない場合、契約のすべての管理者が要求を受け取ります。 

## <a name="resources"></a>リソース
- [Visual Studio の管理とサブスクリプションのサポート](https://visualstudio.microsoft.com/support/support-overview-vs)

## <a name="next-steps"></a>次の手順
- [サブスクリプションを割り当てる](assign-license.md)方法を学ぶ
- さまざまな[サブスクリプションのメリット](https://visualstudio.microsoft.com/vs/benefits/)について学ぶ

