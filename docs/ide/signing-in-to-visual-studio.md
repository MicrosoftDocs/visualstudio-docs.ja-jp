---
title: サインイン
description: Visual Studio にサインインする方法について説明します。
ms.custom: contperf-fy21q1
ms.date: 09/11/2020
ms.topic: how-to
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1335ab3d8f679f00fb7f52420d378baa1f2bd905
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222995"
---
# <a name="sign-in-to-visual-studio-on-windows"></a>Windows 上の Visual Studio にサインインする

必須ではありませんが、サインインすることには多くの利点があります。 サインインすると、自分の Visual Studio でのエクスペリエンスをカスタマイズ、最適化、強化できます。 

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[Visual Studio for Mac にサインインする](/visualstudio/mac/signing-in)」を参照してください。

::: moniker range="vs-2017"

> [!WARNING]
> 条件付きアクセス用に構成されたリソースを操作するには、Visual Studio 2019 Update 16.6 以降にアップグレードします。 詳細については、「[多要素認証が必要なアカウントで Visual Studio を使用する方法](work-with-multi-factor-authentication.md)」を参照してください。
> Visual Studio 2017 で条件付きアクセス用に構成されたリソースにアクセスすると、認証エクスペリエンスが低下し、同じ Visual Studio セッション内で再認証を何度も要求される可能性があります。 
> 
::: moniker-end

## <a name="benefits"></a>メリット

期待できる内容とサイン後に行うことができる内容の完全なリストを以下に示します。

|特長|説明|
|---|---|
|Visual Studio の評価期間を延長する|Visual Studio Professional または Visual Studio Enterprise の評価期間を 30 日間に制限せず、**さらに 90 日延長** して使用できます。 <br/>「[試用版を延長する、またはライセンスを更新する](../ide/how-to-unlock-visual-studio.md)」を参照してください。|
|Visual Studio をロック解除する (Visual Studio サブスクリプションまたは Azure DevOps 組織)|Visual Studio サブスクリプションまたは Azure DevOps 組織に関連付けられているアカウントを使用している場合は、Visual Studio をロック解除します。<br/>「[試用版を延長する、またはライセンスを更新する](../ide/how-to-unlock-visual-studio.md)」を参照してください。|
|お使いの Visual Studio の設定を同期する|ユーザーがカスタマイズした設定 (キー バインド、ウィンドウのレイアウト、配色テーマなど) が、どのデバイス上の Visual Studio にサインインしてもすぐに適用されます。 <br/>[Visual Studio での設定の同期](../ide/synchronized-settings-in-visual-studio.md)に関する記事をご覧ください。|
|サービスに自動的に接続する|同じアカウントの場合、IDE で、Azure や Azure DevOps Services などのサービスに、資格情報を再度要求されることなく接続できます。|
|Visual Studio Community エディションを使用し続ける|お使いの Community エディションのインストールによってライセンスが求められる場合、IDE にサインインすると Visual Studio Community を **無料** で使用し続けることができます。 |
|'Visual Studio Dev Essentials' を入手する|このプログラムには、ソフトウェアの無料オファリング、トレーニング、サポートなどが含まれます。 <br/>[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) に関するページを参照してください。|


## <a name="how-to-sign-in"></a>サインイン方法 

Visual Studio を初めて開くと、サインインして基本登録情報を入力するように求められます。

![サインイン プロンプト](../ide/media/vs2019_signinpopup.png)

1. あなたを最も的確に表す Microsoft アカウント、または職場または学校アカウントを選択します。 これらのアカウントがない場合は、サインイン ボタンの下にあるリンクをクリックして、Microsoft アカウントを無料で作成できます。 問題が発生した場合は、[Microsoft アカウントにサインアップする方法](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)に関するページをご覧ください。

2. Visual Studio で使用する UI 設定や配色テーマを選択します。 これらの設定は Visual Studio に保存され、サインインしたすべての Visual Studio 環境間で同期されます。 同期される設定の一覧については、「[Visual Studio での同期された設定](../ide/synchronized-settings-in-visual-studio.md)」を参照してください。 Visual Studio の **[ツール]** 、 **[オプション]** メニューを開けば、これらの設定は後で変更できます。
   設定が終わったら、Visual Studio が起動し、サインインして、作業を開始できるようになります。 
   
1. ログインしているかどうかを確認するには、Visual Studio 環境の右上隅に表示されているプロファイル名を探します。

![VS2019 に現在ログインしているユーザー](../ide/media/vs2019_username.png)

最初に Visual Studio を開いたときにサインインしないように選択した場合、後から簡単にサインインできます。 Visual Studio 環境の右上隅にある **[サインイン]** リンクを探してください。

![サインインしていないユーザー](../ide/media/vs2019_usernotsignedin.png)

サインアウトしない限り、Visual Studio を起動すると自動的にサインインすることになり、同期された設定への変更が自動的に適用されます。 サインアウトするには、Visual Studio 環境の右上隅にある自分のプロファイル名が表示されたアイコンを選択し、 **[アカウント設定]** コマンドを選択してから **[サインアウト]** リンクを選択します。 再度サインインするには、Visual Studio 環境の右上隅の **[サインイン]** をクリックします。

## <a name="update-your-profile"></a>自分のプロファイルを更新する

1. **[ファイル]** 、 **[アカウント設定]** の順に進み、 **[Visual Studio プロファイルの管理]** リンクを選択します。

1. ブラウザー ウィンドウで、 **[プロファイルの編集]** を選択し、必要な設定を変更します。

1. 完了したら、 **[変更の保存]** を選択します。

## <a name="troubleshooting"></a>トラブルシューティング

ヘルプが必要な場合には、[サブスクリプションのサポート](https://visualstudio.microsoft.com/subscriptions/support/)に関するページを参照してください。
