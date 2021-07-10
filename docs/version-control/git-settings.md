---
title: Visual Studio での Git 設定
titleSuffix: ''
description: Visual Studio で .gitconfig ファイルと Git 設定を使用して優先設定を管理する方法について説明します。
ms.date: 06/08/2021
ms.topic: conceptual
ms.author: prnadago
author: prnadago
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.manager: jmartens
monikerRange: '>=vs-2019'
ms.openlocfilehash: f8dd9781833706a73b82a71236d42cc71c9fb9ec
ms.sourcegitcommit: 113b7df611583307d3965984233a33355d6b0318
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2021
ms.locfileid: "112127027"
---
# <a name="git-settings-and-preferences-in-visual-studio"></a>Visual Studio での Git 設定と優先設定

Visual Studio では、ユーザーの名前とメール アドレス、優先する差分ツールやマージ ツールなど、一般的な Git 設定と優先設定を構成および表示できます。 これらの設定と優先設定は、 **[Git グローバル設定]** ページ (すべてのリポジトリに適用) または **[Git リポジトリの設定]** ページ (現在のリポジトリに適用) のいずれかの **[オプション] ダイアログ ボックス** で表示および構成できます。

次の 2 種類の設定を構成できます。

- [Git 設定](#git-settings) - このセクションの設定は、Git 構成ファイルに保存されている Git 設定に対応します。 これらの設定は、Visual Studio で表示および構成できますが、Git 構成ファイルによって管理されます。
- [Visual Studio 設定](#visual-studio-settings) - このセクションの設定では、Visual Studio によって管理される Git 関連の設定と優先設定を構成します。

## <a name="how-to-configure-settings"></a>設定の構成方法

1. Visual Studio で Git 設定を構成するには、トップ レベルの Git メニューから **[設定]** を選択します。

   :::image type="content" source="media/git-menu-settings.png" alt-text="[設定] コマンドへのコールアウトが表示されている Git メニュー。":::

2. グローバルレベルまたはリポジトリレベルの設定を表示および構成するには、 **[Git グローバル設定]** または **[Git リポジトリの設定]** を選択します。

   :::image type="content" source="media/source-control-settings.png" alt-text="Git 設定へのコールアウトが表示されている [オプション] ダイアログ ボックスのナビゲーション ウィンドウ。":::

3. この記事の以降のセクションで説明するように、いくつかの一般的な Git 設定を構成できます。 必要な設定を構成したら、 **[OK]** を選択して、更新した設定を保存します。

   :::image type="content" source="media/ok-button.png" alt-text="[OK] ボタンへのコールアウトが表示されている [オプション] ダイアログ ボックスの表示領域。":::

## <a name="git-settings"></a>Git 設定

また、最も一般的な Git 構成設定の一部を構成および確認することもできます。 次の設定は、Git 構成ファイルによって管理されている場合でも、Visual Studio で表示および変更できます。

- [名前とメール](#name-and-email)
- [フェッチ中にリモート ブランチを取り除く](#prune-remote-branches-during-fetch)
- [プルするときにローカル ブランチをリベースする](#rebase-local-branch-when-pulling)
- [暗号化ネットワーク プロバイダー](#cryptographic-network-provider)
- [資格情報ヘルパー](#credential-helper)
- [差分ツールおよびマージ ツール](#diff--merge-tools)
- [Git ファイル](#git-files)
- [リモート](#remotes)
- "[その他の設定](#other-settings)"

>[!NOTE]
>Visual Studio の **[グローバル設定]** で構成された Git 設定は、ユーザー固有の Git 構成ファイル内の設定に対応します。 **[リポジトリの設定]** 内の設定は、リポジトリ固有の構成ファイル内の設定に対応します。 Git 構成の詳細については、[Git のカスタマイズに関する Pro Git の章](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)、[git-config のドキュメント](https://git-scm.com/docs/git-config)、[構成ファイルに関する Pro Git リファレンス](https://git-scm.com/docs/git-config#FILES)を参照してください。 Visual Studio で公開されない Git 設定を構成するには、`git config` コマンド (`git config [--local|--global|--system] section.key value`) を使用して、値を構成ファイルに書き込みます。

### <a name="name-and-email"></a>名前とメール

ユーザーが指定する名前とメールは、作成するコミットのコミッター情報として使用されます。 この設定は、グローバルとリポジトリの両方のスコープで使用でき、`git config` [user.name](https://git-scm.com/docs/git-config#Documentation/git-config.txt-username) および [user.email](https://git-scm.com/docs/git-config#Documentation/git-config.txt-useremail) の設定に対応します。

1. Git メニューから、 **[設定]** に移動します。 ユーザー名とメールをグローバル レベルで設定するには、 **[Git グローバル設定]** に移動します。ユーザー名とメールをリポジトリ レベルで設定するには、 **[Git リポジトリの設定]** に移動します。

2. ユーザー名とメールを指定し、 **[OK]** を選択して保存します。 

   :::image type="content" source="media/user-email-setting.png" alt-text="ユーザー名とメールへのコールアウトが表示されている [オプション] ダイアログ ボックスの [グローバル設定] ウィンドウ。":::

### <a name="prune-remote-branches-during-fetch"></a>フェッチ中にリモート ブランチを取り除く

排除によって、リモートに存在しなくなったリモート追跡ブランチが削除され、ブランチの一覧を最新で無駄がない状態に保てるようになります。 この設定は、グローバルとリポジトリの両方のスコープで使用でき、`git config` [fetch.prune](https://git-scm.com/docs/git-config#Documentation/git-config.txt-fetchprune) の設定に対応します。

グローバル レベルでは、このオプションを **[True]** に設定することをお勧めします。 有効な設定は次のとおりです。

- True (推奨)
- 誤り
- 未設定 (既定)

1. Git メニューから、 **[設定]** に移動します。 このオプションをグローバル レベルで構成するには、 **[Git グローバル設定]** に移動します。このオプションをリポジトリ レベルで構成するには、 **[Git リポジトリの設定]** に移動します。

2. **[フェッチ中にリモート ブランチを取り除く]** を **[True]** に設定します (推奨)。 **[OK]** を選択して保存します。

:::image type="content" source="media/prune-setting.png" alt-text="[フェッチ中にリモート ブランチを取り除く] が強調表示され、ドロップダウンから [True] が選択された状態を示すスクリーンショット。":::    

### <a name="rebase-local-branch-when-pulling"></a>プルするときにローカル ブランチをリベースする

リベースでは、上流ブランチにはない現在のブランチ内のコミットによって加えられた変更を確保し、現在のブランチを上流ブランチにリセットした後、確保されている変更を適用します。 この設定は、グローバルとリポジトリの両方のスコープで使用でき、`git config` [pull.rebase](https://git-scm.com/docs/git-config#Documentation/git-config.txt-pullrebase) の設定に対応します。 有効な設定は次のとおりです。

- True: フェッチ後、上流ブランチの上に現在のブランチをリベースします。
- False: 現在のブランチを上流ブランチにマージします。
- 未設定 (既定): 他の構成ファイルで指定されている場合を除いて、現在のブランチを上流ブランチにマージします。
- 対話型: 対話モードでリベースします。
- 保持: ローカルに作成されたマージ コミットをフラット化せずにリベースします。

1. Git メニューから、 **[設定]** に移動します。 このオプションをグローバル レベルで構成するには、 **[Git グローバル設定]** に移動します。このオプションをリポジトリ レベルで構成するには、 **[Git リポジトリの設定]** に移動します。

2. **[プルするときにローカル ブランチをリベースする]** を目的の設定に設定し、 **[OK]** を選択して保存します。

    :::image type="content" source="media/rebase-setting.png" alt-text="[プルするときにローカル ブランチをリベースする] が強調表示され、ドロップダウンから [True] が選択された状態を示すスクリーンショット。":::

Visual Studio では、`pull.rebase` を **[対話型]** に構成することはできません。 Visual Studio では、対話形式のリベースはサポートされていません。
対話モードを使用するように `pull.rebase` を構成するには、コマンド ラインを使用します。

### <a name="cryptographic-network-provider"></a>暗号化ネットワーク プロバイダー

暗号化ネットワーク プロバイダーは、グローバル スコープでの Git 構成設定であり、ランタイムで使用する TLS/SSL バックエンドを構成します。これは、`git config` [http.sslBackend](https://git-scm.com/docs/git-config#Documentation/git-config.txt-httpsslBackend) 設定に対応します。 値は次のとおりです。

- OpenSSL: TLS および SSL プロトコルに [OpenSSL](https://www.openssl.org/) を使用します。
- セキュリティで保護されたチャネル: TLS および SSL プロトコルに [セキュリティで保護されたチャネル (schannel)](/windows/win32/secauthn/secure-channel) を使用します。 Schannel は、Windows Credential Store にアクセスするネイティブの Windows ソリューションであり、エンタープライズ全体にわたる証明書の管理に使用できます。
- 未設定 (既定): この設定が未設定の場合、OpenSSL が既定値になります。

1. Git メニューから、 **[設定]** に移動します。 **[Git グローバル設定]** に移動して、この設定を構成します。

2. **[暗号化ネットワーク プロバイダー]** を目的の値に設定し、 **[OK]** を選択して保存します。

   :::image type="content" source="media/network-provider-setting.png" alt-text="[暗号化ネットワーク プロバイダー] が強調表示され、ドロップダウンから [OpenSSL] が選択された状態を示すスクリーンショット。":::

### <a name="credential-helper"></a>資格情報ヘルパー

Visual Studio でリモート Git 操作を実行すると、要求と共に資格情報を提供する必要があるため、リモート エンドポイントによって要求が拒否される場合があります。 その場合、Git により、資格情報ヘルパーが呼び出されます。資格情報ヘルパーは、操作を実行するために必要な資格情報を返して、要求を再度試行します。 使用される資格情報ヘルパーは、`git config` [credential.helper](https://git-scm.com/docs/gitcredentials) 設定に対応します。 これはグローバル スコープで使用でき、次の値を指定できます。

- GCM for Windows: ヘルパーとして [Git Credential Manager for Windows](https://github.com/microsoft/Git-Credential-Manager-for-Windows) を使用します。
- GCM Core: ヘルパーとして [Git Credential Manager Core](https://github.com/microsoft/Git-Credential-Manager-Core) を使用します。
- 未設定 (既定): この設定が未設定の場合、システム構成で設定された資格情報ヘルパーが使用されます。 Git for Windows 2.29 の時点で、既定の資格情報ヘルパーは GCM Core です。

1. Git メニューから、 **[設定]** に移動します。 **[Git グローバル設定]** に移動して、この設定を構成します。

2. **[資格情報ヘルパー]** を目的の値に設定し、 **[OK]** を選択して保存します。

:::image type="content" source="media/credential-helper-setting.png" alt-text="[オプション] ダイアログ ボックスの [資格情報ヘルパー] 設定を示すスクリーンショット。":::

### <a name="diff--merge-tools"></a>差分ツールおよびマージ ツール

Git では、好みのツールで差分を表示し、競合をマージします。 このセクションの設定は、`git config` [diff.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) および [merge.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool) の設定に対応します。 マージまたは差分ツールとして Visual Studio を使用するように Git を構成するには、 **[Git グローバル設定]** および **[Git リポジトリの設定]** で **[Visual Studio を使用する]** を選択します。 他の差分およびマージ ツールを構成するには、[diff.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) または [merge.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool) スイッチを指定した `git config` を使用します。

:::image type="content" source="media/tools-setting.png" alt-text="[オプション] ダイアログ ボックスで既定の差分ツールとマージ ツールを設定するセクションを示すスクリーンショット。":::

### <a name="git-files"></a>Git ファイル

**[Git リポジトリの設定]** スコープの **[Git ファイル]** セクションを使用して、お使いのリポジトリの [gitignore](https://git-scm.com/docs/gitignore) および [gitattributes](https://git-scm.com/docs/gitattributes) の各ファイルを表示および編集できます。

:::image type="content" source="media/git-files-setting.png" alt-text="リポジトリ内の Ignore ファイルと Attributes ファイルを表示および編集するセクションを示すスクリーンショット。":::

### <a name="remotes"></a>リモート

**[Git リポジトリの設定]** の **[リモート]** ウィンドウを使用して、お使いのリポジトリのリモートを構成できます。 この設定は、[git remote](https://git-scm.com/docs/git-remote) コマンドに対応し、リモートの追加、編集、または削除に使用できます。

:::image type="content" source="media/remotes-settings.png" alt-text="[オプション] ダイアログ ボックスの [Git リモート] ウィンドウを示すスクリーンショット。":::

### <a name="other-settings"></a>その他の設定

他のすべての Git 構成設定を表示するには、構成ファイル自体を開いて表示するか、`git config --list` を実行して設定を表示します。

## <a name="visual-studio-settings"></a>Visual Studio の設定

次の設定では、Visual Studio 内の Git 関連の優先設定を管理します。これらは、Git 構成ファイルではなく Visual Studio によって管理されます。 このセクションの設定はすべて、 **[Git グローバル設定]** で構成されます。

- [既定の場所](#default-location)
- [リポジトリを開くときに、Git の下にない開いているソリューションを閉じる](#close-open-solutions-not-under-git-when-opening-a-repository)
- [サード パーティ ソースからの作成者のイメージのダウンロードを有効にする](#enable-download-of-author-images-from-third-party-sources)
- [既定でマージ後に変更をコミットする](#commit-changes-after-merge-by-default)
- [push --force を有効にする](#enable-push---force-with-lease)
- [Git リポジトリを開くときにソリューション エクスプローラーでフォルダーを開く](#open-folder-in-solution-explorer-when-opening-a-git-repository)
- [Git リポジトリを開くときにソリューションを自動的に読み込む](#automatically-load-the-solution-when-opening-a-git-repository)
- [ダブルクリックまたは Enter キーでブランチを自動的にチェックアウトする](#automatically-check-out-branches-with-double-click-or-the-enter-key)

### <a name="default-location"></a>既定の場所

**[既定の場所]** では、リポジトリを複製する既定のフォルダーを構成します。

:::image type="content" source="media/default-location-setting.png" alt-text="[オプション] ダイアログ ボックスの [既定の場所] フィールドを示すスクリーンショット。":::

### <a name="close-open-solutions-not-under-git-when-opening-a-repository"></a>リポジトリを開くときに、Git の下にない開いているソリューションを閉じる

Visual Studio では、既定により、別のリポジトリに切り替えるとき、開いているソリューションまたはフォルダーはすべて閉じられます。 その際、[[Git リポジトリを開くときにソリューション エクスプローラーでフォルダーを開く]](#open-folder-in-solution-explorer-when-opening-a-git-repository) および [[Git リポジトリを開くときにソリューションを自動的に読み込む]](#automatically-load-the-solution-when-opening-a-git-repository) を選択しているかどうかに応じて、新しいリポジトリのソリューションまたはフォルダーも読み込まれます。 これにより、開いているコードと開いているリポジトリの間の整合性が維持されます。 ただし、ソリューションがリポジトリと同じフォルダー ルートにない場合、そのリポジトリに切り替えるときにソリューションを開いたままにしておくことをお勧めします。 それをこの設定で行うことができます。 値は次のとおりです。

- はい: リポジトリが開いている場合、現在開いているソリューションは常に閉じられます。
- いいえ: リポジトリが開いている場合、Visual Studio により、現在のソリューションが Git 下にあるかどうかについてチェックが実行されます。 そうではない場合は、ソリューションは開いたままです。
- 常に尋ねる (既定): これを設定すると、開いているリポジトリごとに、現在のソリューションを開いたままにするか、または閉じるかをダイアログ ボックスから選択できます。

:::image type="content" source="media/close-sln-setting.png" alt-text="[オプション] ダイアログ ボックスの [ソリューションを閉じる] 設定を示すスクリーンショット。":::


### <a name="enable-download-of-author-images-from-third-party-sources"></a>サード パーティ ソースからの作成者のイメージのダウンロードを有効にする

[サード パーティ ソースからの作成者のイメージのダウンロードを有効にする] は、Visual Studio 固有のグローバル スコープ設定です。 オンにすると、作成者のイメージが [Gravatar イメージ サービス](https://en.gravatar.com/)からダウンロードされ (使用可能な場合)、[コミット] ビューと [履歴] ビューに表示されます。

:::image type="content" source="media/download-image-setting.png" alt-text="サードパーティのソースから作成者のイメージをダウンロードできるようにするための [オプション] ダイアログ ボックスのチェックボックスを示すスクリーンショット。":::

>[!IMPORTANT]
>[コミット] ビューと [履歴] ビューに作成者のイメージを表示するために、アクティブなリポジトリに格納されている作成者のメール アドレスの MD5 ハッシュがツールによって作成されます。 その後、このハッシュは Gravatar に送信され、以前にこのサービスにサインアップしたことがあるユーザーの一致するハッシュ値が検索されます。 一致が見つかると、ユーザーのイメージがサービスから取得され、Visual Studio で表示されます。 サービスを構成していないユーザーについては、ランダムに生成されたイメージが返されます。 メール アドレスは Visual Studio によって記録されないことにご注意ください。また、Gravatar やその他のサードパーティと共有されることもありません。

### <a name="commit-changes-after-merge-by-default"></a>既定でマージ後に変更をコミットする

**[既定でマージ後に変更をコミットする]** を有効にすると、ブランチを現在のブランチとマージするときに、Git により、新しいコミットが自動的に作成されます。

:::image type="content" source="media/merge-commit-setting.png" alt-text="既定でマージ後に変更をコミットするための [オプション] ダイアログ ボックスのチェックボックスを示すスクリーンショット。":::

- オンにすると、Visual Studio によって発行された `git merge` コマンドが、`--commit` オプションを使用して実行されます。
- オフにすると、Visual Studio によって発行された `git merge` コマンドが、`--no-commit --no-ff` オプションを使用して実行されます。

これらのオプションの詳細については、[--commit and --no-commit](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---commit) および [--no-ff](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---no-ff) を参照してください。

### <a name="enable-push---force-with-lease"></a>push --force-with-lease を有効にする

この設定を有効にすると、Visual Studio 内部から `push --force-with-lease` を実行できます。 既定では、 **[push --force-with-lease を有効にする]** は無効になっています。

:::image type="content" source="media/push-force-setting.png" alt-text="push --force-with-lease を有効にするための [オプション] ダイアログ ボックスのチェックボックスを示すスクリーンショット。":::

詳細については、[push --force-with-lease](https://git-scm.com/docs/git-push#Documentation/git-push.txt---no-force-with-lease) を参照してください。

### <a name="open-folder-in-solution-explorer-when-opening-a-git-repository"></a>Git リポジトリを開くときにソリューション エクスプローラーでフォルダーを開く
<!-- todo: write section -->
Visual Studio を使用して Git リポジトリを開くか、Git リポジトリに切り替える場合、Visual Studio によって Git コンテンツが読み込まれ、変更、コミット、ブランチを表示したり、IDE 内からリポジトリを管理したりすることができます。 さらに、Visual Studio によって、リポジトリのコードもソリューション エクスプローラー内に読み込まれます。 Visual Studio では、リポジトリ フォルダーでソリューション、CMakeLists.txt、または認識されるその他のビュー ファイルがスキャンされ、一覧としてソリューション エクスプローラーに表示されます。 そこから、読み込むソリューションまたはフォルダーを選択して、ディレクトリの内容を表示することができます。 このチェックボックスをオフにすると、Visual Studio はソリューション エクスプローラーでリポジトリ フォルダーを開きません。 これにより、基本的に、Visual Studio を開くことができるのは、Git リポジトリ マネージャーに限られます。 この設定は既定でオンになっています。

:::image type="content" source="media/open-folder-setting.png" alt-text="Git リポジトリを開くときにソリューション エクスプローラーでフォルダーを開くための [オプション] ダイアログ ボックスのチェックボックスを示すスクリーンショット。":::

### <a name="automatically-load-the-solution-when-opening-a-git-repository"></a>Git リポジトリを開くときにソリューションを自動的に読み込む

この設定は、[[Git リポジトリを開くときにソリューション エクスプローラーでフォルダーを開く]](#open-folder-in-solution-explorer-when-opening-a-git-repository) 設定がオンの場合のみ適用できます。 Visual Studio で Git リポジトリを開き、その後のフォルダー スキャンによって、リポジトリ内にソリューションが 1 つしかないことが検出されると、Visual Studio によって、そのソリューションが自動的に読み込まれます。 この設定をオフにすると、ソリューション エクスプローラーにより、リポジトリ内にある単一のソリューションがビューの一覧に表示されます。 ただし、ソリューションは読み込まれません。 既定では、この設定はオフです。

:::image type="content" source="media/load-solution-setting.png" alt-text="Git リポジトリを開くときにソリューションを自動的に読み込むための [オプション] ダイアログ ボックスのチェックボックスを示すスクリーンショット。":::

### <a name="automatically-check-out-branches-with-double-click-or-the-enter-key"></a>ダブルクリックまたは Enter キーでブランチを自動的にチェックアウトする

[Git リポジトリ] ウィンドウには、ブランチの一覧がツリー構造で表示されます。 ブランチを 1 回選択すると、コミット履歴ウィンドウが切り替わり、選択したブランチのコミットが表示されます。 ブランチをチェックアウトするには、右クリックしてコンテキスト メニューを開き、 **[チェックアウト]** を選択します。 この設定をオンにした場合、ダブルクリックするか、Enter キーを押すと、ブランチがチェックアウトされ、そのコミットが表示されます。 
  
:::image type="content" source="media/checkout-branch-setting.png" alt-text="ダブルクリックまたは Enter キーでブランチをチェックアウトするための [オプション] ダイアログ ボックスのチェックボックスを示すスクリーンショット。":::


## <a name="see-also"></a>関連項目

> [!IMPORTANT]
> ご提案がございましたら、お知らせください。 [**Developer Community**](https://aka.ms/vsgitsuggestions) ポータルを通じて、設計上の決定についてお客様と関わる機会を持てることに感謝いたします。

- Microsoft Learn の「[Visual Studio で Git と GitHub の使用を開始する](/learn/modules/visual-studio-github-push/)」チュートリアル
- YouTube の [Visual Studio での Git の概要](https://www.youtube.com/watch?v=GCZ9x3yqkyc)のビデオ
- ブログ記事「[Visual Studio での Git による生産性の向上](https://devblogs.microsoft.com/visualstudio/enhanced-productivity-with-git-in-visual-studio/)」
- [[オプション] ダイアログ ボックス](../ide/reference/options-dialog-box-visual-studio.md)
