---
title: Microsoft Endpoint Configuration Manager を使用して Visual Studio の管理者向け更新プログラムを使用できるようにする
titleSuffix: ''
description: Visual Studio に管理者向け更新プログラムを展開する方法について説明します。
ms.date: 04/06/2021
ms.custom: ''
ms.topic: overview
ms.assetid: 546fbad6-f12b-49cf-bccc-f2e63e051a18
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: affb5a0c78c1ad1e230c571485385d9f55fc2bec
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307454"
---
# <a name="enabling-administrator-updates-to-visual-studio-with-microsoft-endpoint-configuration-manager"></a>Microsoft Endpoint Configuration Manager を使用して Visual Studio の管理者向け更新プログラムを使用できるようにする

Visual Studio 2017 および Visual Studio 2019 の管理者向け更新プログラムは、Microsoft Endpoint Configuration Manager (SCCM) のソフトウェア更新プログラム管理者ワークフローを使用して管理できます。

> [!NOTE]
> 以下のコンテンツでは、ドキュメント上わかりやすくするために、Visual Studio 2017、Visual Studio 2019、Visual Studio 2022 製品を総称して、"Visual Studio" と呼びます。

Microsoft が Content Delivery Network (CDN) に新しい Visual Studio の更新プログラムを発行する場合、Microsoft では同時に対応する管理者向け更新プログラム パッケージを Microsoft Update サーバーに発行します。 これにより、管理者は [Microsoft Update カタログ](https://www.catalog.update.microsoft.com/Home.aspx) (MUC) または [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) (WSUS) を使用して Visual Studio の更新プログラムを配布できるようになります。 Visual Studio の管理者向け更新プログラムを WSUS カタログからサイト サーバーに同期し、その後、更新プログラムをダウンロードし、組織全体の Visual Studio クライアント コンピューターに配布するよう、Configuration Manager を設定できます。 Visual Studio の各リリースに含まれる修正プログラムの詳細については、[リリース ノート](/visualstudio/releases/2019/release-notes)を参照してください。

Visual Studio の管理者向け更新プログラムを Configuration Manager を使用して配布するには、初期準備として次の 2 つの手順を実行する必要があります。
1. Configuration Manager が Visual Studio の管理者向け更新プログラムの通知を受信できるようにします。 
2. クライアント コンピューターが、Configuration Manager から Visual Studio の管理者向け更新プログラムを受信できるよう (またはできないよう) にします。

これらの手順を実行すると、Configuration Manager のソフトウェア更新プログラムの管理機能を使用して、Visual Studio の管理者向け更新プログラムを展開できます。 Visual Studio の管理者向け更新プログラムのさまざまな種類と特性については、[管理者向け更新プログラムの適用](../install/applying-administrator-updates.md)に関するページで説明しています。ここでは、それらを自分の組織にいつ、どのように配布するかについて説明しています。 Configuration Manager の機能とオプションの詳細については、[Microsoft Endpoint Configuration Manager でのソフトウェアの更新プログラムの展開](/mem/configmgr/sum/deploy-use/deploy-software-updates)に関するページを参照してください。

## <a name="enable-configuration-manager-to-receive-visual-studio-administrator-update-notifications"></a>Configuration Manager で Visual Studio の管理者向け更新プログラムの通知を受信できるようにする

Configuration Manager で Visual Studio の管理者向け更新プログラムを管理するには、次が必要です。

* Microsoft Endpoint Configuration Manager (Current Branch) および Windows Server Update Services (WSUS) を実行している現在のライセンス バージョンの Windows Server。 WSUS 自体では、これらの更新プログラムは展開できません。Configuration Manager と組み合わせて使用する必要があります。

* 階層の最上位の WSUS サーバーと最上位の Configuration Manager サイト サーバーが、「[ファイアウォールまたはプロキシ サーバーの内側に Visual Studio と Azure サービスをインストールして使用する](../install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)」に記載されている Visual Studio の URL とポートにアクセスできること。  

* Visual Studio の管理者向け更新プログラム パッケージが利用できるようになったとき、通知を受信する構成が、Microsoft Endpoint Configuration Manager でされていること。  そのためには、次の手順を使用します。詳細については、[Configuration Manager のソフトウェア更新プログラムの概要](/mem/configmgr/sum/understand/software-updates-introduction)に関するページを参照してください。

  1. Configuration Manager のコンソールで、 **[管理]** (左下) を選択し、 **[サイトの構成]** (中央左)、 **[サイト]** の順に選択して、お使いのサイト サーバーを選択します。

  2. 上部の **[ホーム]** タブのリボンの **[設定]** グループ ボタンの **[サイト コンポーネントの構成]** を選択し、 **[ソフトウェアの更新ポイント]** を選択します。

  3. **[ソフトウェアの更新ポイント コンポーネントのプロパティ]** ダイアログ ボックスで、次を実行します。

        * **[製品]** タブで **[Developer Tools, Runtimes, and Redistributables]\(開発者ツール、ランタイム、および再頒布可能ファイル\)** 階層から、同期する Visual Studio のバージョンを選択します。

        * **[分類]** タブで、[セキュリティ更新プログラム]、[機能パック]、[更新プログラム] が選択されていることを確認します。

  4. 次に、 **[ソフトウェア ライブラリ]** (左下) を選択して、ソフトウェア更新プログラムを WSUS サーバーと同期します。次に、上部の **[ホーム]** タブ リボンで、 **[ソフトウェア更新プログラムの同期]** ボタンを選択します。 ソフトウェア更新プログラムを同期すると、Configuration Manager コンソールに使用可能な Visual Studio の管理者向け更新プログラムが表示され、それを展開できるようになります。

## <a name="enable-or-disable-client-machines-ability-to-receive-visual-studio-administrator-updates-from-configuration-manager"></a>クライアント コンピューターが Configuration Manager から Visual Studio の管理者向け更新プログラムを受信できるよう (またはできないよう) にする

クライアント コンピューターで Visual Studio の管理者向け更新プログラムを受信するには、Visual Studio のクライアント検出ユーティリティが正しくインストールされている必要があります。また、レジストリ キーが設定され、クライアントが管理者向け更新プログラムを受信できる必要があります。  

### <a name="visual-studio-client-detector-utility"></a>Visual Studio クライアント検出ユーティリティ

クライアント コンピューターで管理者向け更新プログラムを正しく認識し、受信するには、[Visual Studio クライアント検出ユーティリティ](https://support.microsoft.com/help/5001148)がインストールされている必要があります。 このユーティリティは、2020 年 5 月 12 日以降にリリースされたすべての Visual Studio 2017 および Visual Studio 2019 の製品の更新プログラムに含まれていました。これは、すべての Visual Studio 管理者向け更新プログラムの前提条件として含まれており、[Microsoft Update カタログ](https://catalog.update.microsoft.com)で個別にインストールすることもできます。

### <a name="encoding-administrator-intent-on-the-client-machines"></a>クライアント コンピューターでの管理者の意図のエンコード

管理者向け更新プログラムは、クライアント コンピューターでそれが受信できるようになっている必要があります。 この手順は、予期しないクライアント コンピューターに更新プログラムが意図せず、または偶発的にプッシュされないようにするために必要です。

 **AdministratorUpdatesEnabled** キーは、管理者が管理者の意図をエンコードできるよう設計されています。 このキーは、「 [Visual Studio のエンタープライズ展開に既定値を設定する](/visualstudio/install/set-defaults-for-enterprise-deployments)」で説明のとおり、Visual Studio の標準的なすべての場所に配置できます。 このキー値を作成および設定するには、クライアント コンピューターの管理者権限が必要です。

* クライアント コンピューターで管理者向け更新プログラムを受信できるよう構成するには、 **AdministratorUpdatesEnabled** REG_DWORD キーを  **1** に設定します。
*  **AdministratorUpdatesEnabled** REG_DWORD キーが **ないか、0 に設定されている場合**、管理者向け更新プログラムはブロックされ、クライアント コンピューターに適用されません。

## <a name="feedback-and-support"></a>フィードバックとサポート

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

次の方法を使用して、Visual Studio の管理者向け更新プログラムに関するフィードバックを提供したり、更新プログラムに影響する問題を報告したりできます。

* 「[Visual Studio のインストールとアップグレードの問題のトラブルシューティング](../install/troubleshooting-installation-issues.md)」ガイダンスをご覧ください。
* [Visual Studio セットアップ Q&A フォーラム](/answers/topics/vs-setup.html)でコミュニティに質問してください。
* [Visual Studio のサポート ページ](https://visualstudio.microsoft.com/vs/support/)にアクセスし、ご自分の問題がよくあるご質問に記載されているかどうかを確認します。  チャット ヘルプの [[サポート リンク]](https://visualstudio.microsoft.com/vs/support/#talktous) ボタンを選択することもできます。
* 管理者向け更新プログラムの有効化エクスペリエンスに関して、Visual Studio チームに[機能に関するフィードバックを提供するか、問題を報告](https://aka.ms/vs/wsus/feedback)してください。
* 組織の Microsoft のテクニカル アカウント マネージャーにお問い合わせください。

## <a name="see-also"></a>関連項目

* [管理者の更新を適用する](../install/applying-administrator-updates.md)
* [Visual Studio 管理者ガイド](../install/visual-studio-administrator-guide.md)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/productinfo/vs-servicing-vs)
* [Visual Studio 2019 リリース ノート](/visualstudio/releases/2019/release-notes)
* [Visual Studio 2017 リリース ノート](/visualstudio/releasenotes/vs2017-relnotes)
* [Visual Studio のインストール](../install/install-visual-studio.md)
* [Microsoft Update カタログのよく寄せられる質問](https://www.catalog.update.microsoft.com/faq.aspx)
* [Microsoft Endpoint Configuration Manager (SCCM) のドキュメント](/mem/configmgr)
* [Microsoft カタログから Configuration Manager に更新プログラムをインポートする](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)
* [Windows Server Update Services (WSUS) のドキュメント](/windows-server/administration/windows-server-update-services/get-started-windows-server-update-services-wsus)
