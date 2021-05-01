---
title: Visual Studio 2019 での Git エクスペリエンス
titleSuffix: ''
description: Visual Studio 2019 での新しい統合 Git エクスペリエンスが、生産性の向上にどのように役立つかについて学習します。
ms.date: 04/01/2021
ms.topic: overview
ms.author: tglee
author: TerryGLee
ms.manager: jillfra
ms.openlocfilehash: 96018a203a6a0e5d404a818817ea4e9fb7e18551
ms.sourcegitcommit: 5fb684ff8729eb118aa91ce9f049c79eeb9747b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2021
ms.locfileid: "107920947"
---
# <a name="git-experience-in-visual-studio"></a>Visual Studio での Git エクスペリエンス

Git が Visual Studio 2019 での既定のバージョン管理エクスペリエンスになりました。 [バージョン 16.6](/visualstudio/releases/2019/release-notes-v16.6) 以降、機能セットの構築と、お客様のフィードバックに基づくその反復処理に取り組んできました。 [バージョン 16.8](/visualstudio/releases/2019/release-notes/) のリリースでは、すべてのユーザーに対して既定で新しい Git エクスペリエンスが有効になります。

> [!TIP]
> Git は最も広く使用されている最新のバージョン管理システムであるため、プロフェッショナルな開発者であるか、コードの作成方法を学習しているかに関係なく、Git は非常に役に立ちます。 Git を初めて使用する場合は、 https://git-scm.com/ の Web サイトから開始することをお勧めします。 そこには、チート シート、人気のあるオンライン ブック、および Git の基本のビデオがあります。

## <a name="how-to-use-git-in-visual-studio"></a>Visual Studio で Git を使用する方法

Visual Studio 2019 で新しい Git エクスペリエンスを使用する方法について説明しますが、最初に概要を確認したい場合は、次のビデオをご覧ください。 <br><br>"*ビデオの長さ:5.27 分*"

> [!VIDEO https://www.youtube.com/embed/UHrAg3iKoe0]

生産性を向上させるために Visual Studio で Git の使用を開始するには、次の 3 つの方法があります。

- [既存の Git リポジトリを開く](#open-an-existing-local-repository)。 お使いのマシン上に既にコードがある場合は、 **[ファイル]**  >  **[開く]**  >  **[プロジェクト/ソリューション]** (または **[フォルダー]** ) を使用して開くことができます。VisualStudio によって、初期化された Git リポジトリがあるかどうかが自動的に検出されます。
- [新しい Git リポジトリを作成する](#create-a-new-git-repository)。 コードが Git に関連付けられていない場合は、新しい Git リポジトリを作成できます。
- [既存の Git リポジトリをクローンする](#clone-an-existing-git-repository)。 使用するコードがお使いのマシン上にない場合は、既存の任意のリモート リポジトリをクローンすることができます。

> [!NOTE]
> また[バージョン 16.8](/visualstudio/releases/2019/release-notes/) からは、Visual Studio 2019 には完全に統合された GitHub アカウントのエクスペリエンスが含まれています。 これで、GitHub と GitHub Enterprise 両方のアカウントをキーチェーンに追加できるようになりました。 Microsoft アカウントの場合と同様にそれらを追加して活用できるようになります。つまり、Visual Studio 全体で GitHub リソースにより簡単にアクセスできるようになります。 詳細については、「[Visual Studio の GitHub アカウントを使って作業する](../ide/work-with-github-accounts.md)」ページを参照してください。

## <a name="create-a-new-git-repository"></a>新しい Git リポジトリを作成する

コードが Git に関連付けられていない場合は、新しい Git リポジトリを作成することから始めることができます。 これを行うには、メニュー バーから **[Git]**  >  **[Git リポジトリの作成]** を選択します。 次に、 **[Git リポジトリの作成]** ダイアログ ボックスに情報を入力します。

:::image type="content" source="media/git-create-repository.png" alt-text="Visual Studio の [Git リポジトリの作成] ダイアログ ボックス。":::

**[Git リポジトリの作成]** ダイアログ ボックスを使用すると、新しいリポジトリを GitHub に簡単にプッシュできます。 既定では、新しいリポジトリはプライベートになります。つまり、アクセスできるのは自分だけです。 このチェックボックスをオフにすると、リポジトリはパブリックになります。つまり、GitHub のすべてのユーザーに表示されます。

> [!TIP]
> リポジトリがパブリックかプライベートかに関係なく、チームで作業していない場合でも、コードのリモート バックアップを GitHub に安全に保存することをお勧めします。 これにより、使用しているコンピューターに関係なく、コードを使用できるようになります。

ローカル専用の Git リポジトリを作成するには、 **[ローカルのみ]** オプションを使用します。 または、 **[既存のリモート]** オプションを使用して、Azure DevOps または他の Git プロバイダー上の既存の空のリモート リポジトリに自分のローカル プロジェクトをリンクすることもできます。

## <a name="clone-an-existing-git-repository"></a>既存の Git リポジトリをクローンする

Visual Studio には、簡単なクローン エクスペリエンスが含まれています。 クローンするリポジトリの URL がわかっている場合は、 **[リポジトリの場所]** セクションに URL を貼り付けてから、Visual Studio のクローン先となるディスクの場所を選択します。

:::image type="content" source="media/git-clone-repository.png" alt-text="Visual Studio の [Clone a Git Repository]\(Git リポジトリのクローン\) ダイアログ ボックス。":::

リポジトリの URL がわからない場合は、Visual Studio を使用すると、既存の GitHub または Azure DevOps リポジトリを参照してクローンすることが簡単にできます。

### <a name="open-an-existing-local-repository"></a>既存のローカル リポジトリを開く

リポジトリをクローンまたは作成すると、Visual Studio によって Git リポジトリが検出され、Git メニューの **[Local Repositories]\(ローカル リポジトリ\)** の一覧に追加されます。 ここから、Git リポジトリにすばやくアクセスして切り替えることができます。

:::image type="content" source="media/git-local-repositories.png" alt-text="Visual Studio の Git メニューの [Local Repositories]\(ローカル リポジトリ\) オプション ":::

## <a name="view-files-in-solution-explorer"></a>ソリューション エクスプローラーにファイルを表示する

リポジトリをクローンするか、ローカル リポジトリを開くと、Visual Studio では、以前に開いていたソリューションとプロジェクトを保存して閉じることにより、その Git コンテキストに切り替えられます。 ソリューション エクスプローラーによって、Git リポジトリのルートにあるフォルダーが読み込まれ、すべてのビュー ファイルのディレクトリ ツリーがスキャンされます。 これには、CMakeLists.txt などのファイルや、.sln ファイル拡張子を持つファイルが含まれます。

ソリューション エクスプローラーに読み込むビュー ファイルに基づいて、Visual Studio でそのビューが調整されます。

- 単一の .sln ファイルを含むリポジトリをクローンすると、ソリューション エクスプローラーによってそのソリューションが直接読み込まれます。
- ソリューション エクスプローラーでリポジトリ内の .sln ファイルが検出されない場合は、既定でフォルダー ビューが読み込まれます。
- リポジトリに複数の .sln ファイルが含まれている場合は、ソリューション エクスプローラーによって選択可能なビューの一覧が表示されます。

ソリューション エクスプローラーのツールバーにある **[表示の切替]** ボタンを使用して、現在開いているビューとビューの一覧を切り替えることができます。

:::image type="content" source="media/git-solution-explorer-views.png" alt-text="Visual Studio で [表示の切替] ボタンが選択されているソリューション エクスプローラー。":::

## <a name="git-changes-window"></a>[Git Changes]\(Git 変更\) ウィンドウ

Git により、作業中のリポジトリ内のファイルの変更が追跡され、リポジトリ内のファイルが 3 つのカテゴリに分割されます。 これらの変更は、コマンド ラインで `git status` コマンドを入力したときに表示されるものと同じです。

- **未変更のファイル**: これらのファイルは、最後のコミットから変更されていません。
- **変更されたファイル**: これらのファイルには最後のコミットからの変更が含まれていますが、まだ次回のコミット用にステージされていません。
- **ステージされたファイル**: これらのファイルには、次のコミットに追加される変更が含まれています。

作業を行っている間、Visual Studio により、 **[Git Changes]\(Git 変更\)** ウィンドウの **[変更]** セクションで、プロジェクトに対するファイルの変更が追跡されます。

:::image type="content" source="media/git-changes-window.png" alt-text="Visual Studio の [Git Changes]\(Git 変更\) ウィンドウ。":::

変更をステージする準備ができたら、ステージングする各ファイルの [ **+** ] (プラス) ボタンをクリックするか、ファイルを右クリックして **[ステージ]** を選択します。 **[変更]** セクションの上部にある、すべての [ **+** ] (プラス) ボタンを使用して、変更したすべてのファイルをワンクリックでステージすることもできます。

変更をステージすると、Visual Studio によって **[ステージされている変更]** セクションが作成されます。 **[ステージされている変更]** セクションの変更のみが次のコミットに追加されます。これを行うには、 **[ステージ済みをコミット]** を選択します。 このアクションの同等のコマンドは、`git commit -m "Your commit message"` です。 **[–]** (マイナス) ボタンをクリックして、変更をステージング解除することもできます。 このアクションの同等のコマンドは、1 つのファイルをステージ解除する `git reset <file_path>`、またはディレクトリ内のすべてのファイルをステージング解除する `git reset <directory_path>` です。

ステージ領域をスキップして、変更されたファイルをステージしないように選択することもできます。 この場合、Visual Studio を使用すると、変更をステージせずに直接コミットできます。 コミット メッセージを入力し、 **[すべてコミット]** を選択します。 このアクションの同等のコマンドは、`git commit -a` です。

また、Visual Studio では、 **[すべてをコミットしてプッシュ]** と **[すべてをコミットして同期]** を使用して、コミットと同期をワンクリックで簡単に行えます。 **[変更]** セクションと **[ステージされている変更]** セクションのいずれかのファイルをダブルクリックすると、変更されていないバージョンのファイルとの行ごとの比較を確認できます。

:::image type="content" source="media/git-file-version-compare.png" alt-text="Visual Studio でのファイル バージョンの行ごとの比較 ":::

> [!TIP]
> Azure DevOps リポジトリに接続している場合は、"#" 文字を使用して、Azure DevOps 作業項目をコミットに関連付けることができます。 **[チーム エクスプローラー]**  >  **[接続の管理]** を介して、Azure DevOps リポジトリに接続することができます。

### <a name="select-an-existing-branch"></a>既存のブランチを選択する

Visual Studio の **[Git Changes]\(Git 変更\)** ウィンドウの上部にあるセレクターに現在のブランチが表示されます。

:::image type="content" source="media/git-changes-current-branch-selector.png" alt-text="Visual Studio の Git 変更セレクターの上部にあるセレクターを使用して表示できる現在のブランチ ":::

現在のブランチは、Visual Studio IDE の右下隅にあるステータス バーでも使用できます。

:::image type="content" source="media/git-changes-current-branch-status-bar.png" alt-text="Visual Studio IDE の右下隅にあるステータス バーを使用して表示できる現在のブランチ ":::

どちらの場所からでも、既存のブランチを切り替えることができます。

### <a name="create-a-new-branch"></a>新しいブランチを作成する

新しいブランチを作成することもできます。 このアクションの同等のコマンドは、`git checkout -b <branchname>` です。

新しいブランチの作成は、ブランチ名を入力して既存のブランチを基にするだけの簡単なものです。

:::image type="content" source="media/git-changes-create-new-branch.png" alt-text="Visual Studio の [新しいブランチを作成] ダイアログ ボックス ":::

ベースとして、既存のローカルまたはリモート ブランチを選択できます。 **[ブランチのチェックアウト]** チェックボックスをオンにすると、新しく作成されたブランチに自動的に切り替わります。 このアクションの同等のコマンドは、`git checkout -b <new-branch><existing-branch>` です。

## <a name="git-repository-window"></a>[Git リポジトリ] ウィンドウ

Visual Studio には、新しい **[Git リポジトリ]** ウィンドウがあります。これは、リポジトリ内のすべての詳細 (すべてのブランチ、リモート、およびコミット履歴を含む) を統合したビューです。 このウィンドウには、メニュー バーまたはステータス バーの **[Git]** または **[表示]** から直接アクセスできます。

### <a name="manage-branches"></a>ブランチを管理する

**[Git]** メニューから **[ブランチの管理]** を選択すると、 **[Git リポジトリ]** ウィンドウにブランチ ツリービューが表示されます。 左ペインからは、右クリックのコンテキスト メニューを使用して、ブランチのチェックアウト、新しいブランチの作成、マージ、リベース、チェリーピックなどを行うことができます。 ブランチをクリックすると、右ペインにそのコミット履歴のプレビューが表示されます。

### <a name="incoming-and-outgoing-commits"></a>送信および発信中のコミット

ブランチをフェッチすると、 **[Git Changes]\(Git 変更\)** ウィンドウのブランチ ドロップダウンの下にインジケーターが表示され、リモート ブランチからプルされていないコミットの数が表示されます。 このインジケーターには、プッシュされていないローカル コミットの数も表示されます。

:::image type="content" source="media/git-repo-drop-down-indicator.png" alt-text="Visual Studio のインジケーター ドロップダウン UI 要素を示す [Git Changes]\(Git 変更\) ウィンドウ ":::

このインジケーターは、 **[Git リポジトリ]** ウィンドウでそのブランチのコミット履歴に移動するためのリンクとしても機能します。 履歴の一番上には、これらの送信および発信中のコミットの詳細が表示されます。 ここから、コミットをプルまたはプッシュすることもできます。

:::image type="content" source="media/git-branch-commit-history.png" alt-text="Visual Studio のブランチのコミット履歴を表示する [Git リポジトリ] ウィンドウ ":::

#### <a name="commit-details"></a>コミットの詳細

**コミット** をダブルクリックすると、Visual Studio によってその詳細が別のツール ウィンドウに表示されます。 ここからコミットを元に戻したり、コミットをリセットしたり、コミット メッセージを修正したり、コミット時にタグを作成したりできます。 コミット時に変更されたファイルをクリックすると、Visual Studio によって、コミットとその親の **[差分]** ビューが並べて表示されます。

:::image type="content" source="media/git-branch-commit-details.png" alt-text="Visual Studio の [コミットの詳細] ダイアログ ボックス ":::

## <a name="handle-merge-conflicts"></a>マージ競合を処理する

2 人の開発者がファイル内の同じ行を変更し、Git でどちらが正しいかが自動的に認識されない場合、マージ中に競合が発生する可能性があります。 Git によってマージが停止され、競合している状態であることが通知されます。

Visual Studio を使用すると、マージの競合を簡単に識別して解決できます。 最初に、 **[Git リポジトリ]** ウィンドウの上部に金色の情報バーが表示されます。

:::image type="content" source="media/git-merge-conflict-gold-bar.png" alt-text="Visual Studio での &quot;マージが完了し、競合が発生しました&quot; というメッセージ ":::

**[Git Changes]\(Git 変更\)** ウィンドウにも、"*Merge is in progress with conflicts*" (競合があるマージが進行中) というメッセージが表示され、その下の別のセクションには、マージされていないファイルが表示されます。

:::image type="content" source="media/git-merge-progress-conflicts-message.png" alt-text="Visual Studio での &quot;Merge is in progress with conflicts&quot; (競合があるマージが進行中) というメッセージ ":::

ただし、どちらのウィンドウも開いておらず、代わりにマージ競合があるファイルに移動する場合は、次のテキストを検索する必要はありません。

```bash
    <<<<<<< HEAD
    =======
    >>>>>>> main
```

代わりに、Visual Studio では、開いているファイルに競合があることを示す金色の情報バーがページの上部に表示されます。 次に、リンクをクリックして、**マージ エディター** を開きます。

:::image type="content" source="media/git-merge-conflict-gold-info-bar.png" alt-text="Visual Studio での &quot;File contains merge conflicts&quot; (ファイルにマージ競合が含まれています) というメッセージのスクリーンショット ":::

### <a name="the-merge-editor"></a>マージ エディター

Visual Studio のマージ エディターは、入力方向の変更、現在の変更、およびマージの結果を表示する 3 方向マージ ツールです。 **マージ エディター** の最上位レベルにあるツール バーを使用して、ファイル内の競合と自動マージされた相違点の間を移動できます。

:::image type="content" source="media/git-merge-editor.png" alt-text="Visual Studio のマージ エディター ":::

また、トグルを使用して、相違点の表示/非表示を切り替えたり、単語の違いを表示/非表示にしたり、レイアウトをカスタマイズしたりすることもできます。 両側の上部にチェックボックスがあり、これを使用して、一方または他方からすべての変更を取り込むことができます。 ただし、個々の変更を行うには、どちらか一方の競合する行の左側にあるチェックボックスをクリックします。 最後に、競合の解決が終了したら、マージ エディターの **[マージの許可]** ボタンを選択します。 次に、コミット メッセージを作成し、変更をコミットして解決を完了します。

## <a name="personalize-your-git-settings"></a>Git 設定をパーソナル化する

リポジトリ レベルとグローバル レベルで Git 設定をパーソナル化してカスタマイズするには、メニュー バーで **[Git]**  >  **[設定]** に移動するか、メニュー バーで **[ツール]**  >  **[オプション]**  >  **[ソース管理]** に移動します。 次に、目的のオプションを選択します。

:::image type="content" source="media/git-options-settings.png" alt-text="パーソナル化とカスタマイズの設定を選択できる、Visual Studio IDE の [オプション] ダイアログ ボックス ":::

## <a name="how-to-use-the-full-team-explorer-experience-in-visual-studio"></a>Visual Studio でチーム エクスプローラーの完全なエクスペリエンスを使用する方法

新しい Git エクスペリエンスは、[バージョン 16.8](/visualstudio/releases/2019/release-notes/) 以降の Visual Studio 2019 での既定のバージョン管理システムです。 しかし、それを無効にしたい場合は、そのようにできます。 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[プレビュー機能]** の順に移動してから、 **[New Git user experience]\(新しい Git ユーザー エクスペリエンス\)** チェックボックスを切り替えます。これにより、Git のチーム エクスプローラーに戻ります。

:::image type="content" source="media/git-opt-new-user-experience.png" alt-text="Visual Studio の [オプション] ダイアログ ボックスの [プレビュー機能] セクション ":::

## <a name="whats-next"></a>参照トピック

Visual Studio 2019 [バージョン 16.8](/visualstudio/releases/2019/release-notes/) で新しい Git エクスペリエンスが既定でオンになるようになりましたが、エクスペリエンスを向上させるために新しい機能が引き続き追加されます。 Preview リリースで Git エクスペリエンスの新しい更新プログラムを確認する場合は、[Visual Studio Preview](https://aka.ms/vspreview/) ページからダウンロードしてインストールできます。

> [!IMPORTANT]
> ご提案がございましたら、お知らせください。 [**Developer Community**](https://aka.ms/vs-suggest) ポータルを通じて、設計上の決定についてお客様と関わる機会を持てることに感謝いたします。

## <a name="see-also"></a>関連項目

- Microsoft Learn の「[Visual Studio で Git と GitHub の使用を開始する](/learn/modules/visual-studio-github-push/)」チュートリアル
- YouTube の [Visual Studio での Git の概要](https://www.youtube.com/watch?v=GCZ9x3yqkyc)のビデオ
- 「[Visual Studio での Git エクスペリエンスのリリースの発表](https://devblogs.microsoft.com/visualstudio/announcing-the-release-of-the-git-experience-in-visual-studio/)」ブログ記事
- YouTube の動画「[新しい Git エクスペリエンスの起動](https://www.youtube.com/watch?v=UHrAg3iKoe0&t)」
- [Visual Studio のツールボックス シリーズでは、以下が示されます: 新しい Git エクスペリエンス](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/The-New-Git-Experience)の動画 (Channel 9)。[YouTube](https://www.youtube.com/watch?v=ZiQ2LXtAJ6I&feature=youtu.be) でもご覧いただけます
- [Visual Studio での Git エクスペリエンスに関する新しい更新プログラム](https://devblogs.microsoft.com/visualstudio/exciting-new-updates-to-the-git-experience-in-visual-studio/)のブログ記事
- [Visual Studio 2019 での Git エクスペリエンスの向上](https://devblogs.microsoft.com/visualstudio/improved-git-experience-in-visual-studio-2019/)のブログ記事
- [Visual Studio の GitHub アカウントを使って作業する](../ide/work-with-github-accounts.md)
- [Visual Studio 2019 リリース ノート](/visualstudio/releases/2019/release-notes)
