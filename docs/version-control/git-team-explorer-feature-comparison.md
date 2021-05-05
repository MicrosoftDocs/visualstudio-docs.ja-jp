---
title: Visual Studio での Git とチーム エクスプローラーを並べて比較する
titleSuffix: ''
description: ソース コントロールを管理するために Visual Studio で新しい Git エクスペリエンスを使用する方法とチーム エクスプローラーを使用する方法を比較対照します。
ms.date: 04/01/2021
ms.topic: how-to
ms.author: tglee
author: TerryGLee
ms.manager: jmartens
ms.openlocfilehash: 6ae09069e021ee9ff5699641bbe8662bf84ad327
ms.sourcegitcommit: 5fb684ff8729eb118aa91ce9f049c79eeb9747b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2021
ms.locfileid: "108635393"
---
# <a name="side-by-side-comparison-of-git-and-team-explorer"></a>Git とチーム エクスプローラーを並べて比較する

Visual Studio 2019 [バージョン 16.8](/visualstudio/releases/2019/release-notes/) で、新しい Git エクスペリエンスの最初のバージョンを発表しました。 この新しいエクスペリエンスにより、一般的な Git タスクを含むシンプルな **[Git 変更]** ウィンドウでコンテキストの切り替えを減らすことができます。 また、これには、ブランチの管理やリポジトリの参照など、より高度な Git 操作のための全画面の **[Git リポジトリ]** ウィンドウも含まれています。

チーム エクスプローラーを使用している場合は、新しい Git エクスペリエンスを使用する方法について、次の手順を追ったガイドを参照してください。

> [!NOTE]
> 次のセクションでは、テーブルの列に合わせてサイズ変更されたスクリーンショットを示します。 各スクリーンショットをクリックすると、より大きなバージョンが表示されます (タッチスクリーン デバイスを使用している場合は、各スクリーンショットをタップして、より大きなバージョンを表示してください)。

## <a name="get-started"></a>開始

|         |チーム エクスプローラー  |新しい Git エクスペリエンス |
|---------|---------|---------|
|**リポジトリを複製する** | :::image type="content" source="media/clone-repo-team-explorer-sml.png" alt-text="&quot;リポジトリを複製&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [接続] ウィンドウのスクリーンショット。" lightbox="media/clone-repo-team-explorer-lrg.png":::  </p>1. **[接続]** ページを開きます。 <br> 2. **[接続の管理]** を展開します。 <br> 3. **[プロジェクトに接続]** を選択します。 | :::image type="content" source="media/clone-repo-new-git-sml.png" alt-text="&quot;リポジトリを複製&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git] メニューのスクリーンショット。" lightbox="media/clone-repo-new-git-lrg.png":::  </p> 1. **[Git]** メニューを開きます。 <br>2. **[リポジトリの複製]** を選択します。 <br><br> |
|**レポジトリの切り替え**  | :::image type="content" source="media/switch-repos-team-explorer-sml.png" alt-text="&quot;リポジトリの切り替え&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [接続] ウィンドウのスクリーンショット。" lightbox="media/switch-repos-team-explorer-lrg.png":::  </p>1. **[接続]** ページを開きます。 <br>2. **[ローカル リポジトリ]** リストからリポジトリを選択します。 | :::image type="content" source="media/switch-repos-new-git-sml.png" alt-text="&quot;リポジトリを複製&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [ローカル リポジトリ] メニュー項目のスクリーンショット。" lightbox="media/switch-repos-new-git-lrg.png"::: </p> 1. **[Git]** メニューを開きます。 <br>2. **[ローカル リポジトリ]** リストからリポジトリを選択します。  |
|**ソリューションを開く**  |  :::image type="content" source="media/open-solution-team-explorer-sml.png" alt-text="&quot;ソリューションを開く&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [ホーム] ウィンドウのスクリーンショット。" lightbox="media/open-solution-team-explorer-lrg.png":::</p>1.**チーム エクスプローラー** で **[ホーム]** ページを開きます。 <br>2.ソリューションのリストからソリューションを選択します。  |  :::image type="content" source="media/open-solution-new-git-sml.png" alt-text="&quot;ソリューションを開く&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のソリューション エクスプローラーのスクリーンショット。" lightbox="media/open-solution-new-git-lrg.png":::</p>1.**ソリューション エクスプローラー** で **[ビューの切り替え]** ページを開きます。 <br>2.ソリューションのリストからソリューションを選択します。  |
|**ソース コントロールにソリューションを追加し、新しいリポジトリを作成する**  | :::image type="content" source="media/source-control-team-explorer-sml.png" alt-text="&quot;ソース コントロールに追加 - リポジトリの作成&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラー オプションのスクリーンショット コラージュ。" lightbox="media/source-control-team-explorer-lrg.png":::</p>1. **[ソース コントロールに追加]** ステータス バー メニューで **[Git]** を選択します。 <br>2. **[発行]** を選びます。  | :::image type="content" source="media/source-control-new-git-sml.png" alt-text="&quot;ソース コントロールに追加 - リポジトリの作成&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の Git オプションのスクリーンショット コラージュ。" lightbox="media/source-control-new-git-lrg.png":::</p>1. **[ソース コントロールに追加]** ステータス バー メニューで **[Git]** を選択するか、最上位の Visual Studio メニュー バーで **[Git]**  >  **[Create Git Repository]\(Git リポジトリの作成\)** を選択します。 <br>2. **[Create and Push]\(作成してプッシュ\)** を選択します。 </p> **注**: Azure DevOps にコードを追加する場合は、既存のリモート オプションを使用します。 この場合、最初に Azure DevOps リポジトリを作成する必要があります。 |
> [!TIP]
> [新しい Git エクスペリエンス](git-with-visual-studio.md)は、開いたリポジトリまたはソリューションに基づいて、適切な Azure DevOps リポジトリに自動的に接続されます。 ただし、リポジトリに手動で接続する必要がある場合でも、チーム エクスプローラーを使用してこれを行うことができます。 Visual Studio のメニュー バーで、 **[表示]**  >  **[チーム エクスプローラー]**  >  **[接続の管理]**  >  **[接続]** を選択します。

## <a name="git-changes"></a>Git 変更

|         |チーム エクスプローラー  |新しい Git エクスペリエンス |
|---------|---------|---------|
|**[Commit and stage]\(コミットとステージ\)** | :::image type="content" source="media/commit-stage-team-explorer-sml.png" alt-text="&quot;コミットとステージ&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [変更] ウィンドウのスクリーンショット。" lightbox="media/commit-stage-team-explorer-lrg.png":::  </p>1.コミット メッセージを入力します。 <br>2. **[すべてをコミット]** を選択します。 <br>3.特定のファイルをステージングするには、そのファイルを右クリックし、 **[ステージ]** を選択します。  | :::image type="content" source="media/commit-stage-new-git-sml.png" alt-text="&quot;コミットとステージ&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウのスクリーンショット。" lightbox="media/commit-stage-new-git-lrg.png"::: </p>1.コミット メッセージを入力します。 <br>2. **[すべてをコミット]** を選択します。 <br>3.特定のファイルをステージングするには、その上にマウス ポインターを移動し、" **+** " アイコンをクリックします。 |
|**コミットの修正** |  :::image type="content" source="media/amend-commit-team-explorer-sml.png" alt-text="&quot;コミットの修正&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [変更] ウィンドウのスクリーンショット。" lightbox="media/amend-commit-team-explorer-lrg.png":::</p>1. **[アクション]** ドロップダウンをクリックします。 <br>2. **[以前のコミットを修正]** を選択します。 | :::image type="content" source="media/amend-commit-new-git-sml.png" alt-text="&quot;コミットの修正&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウのスクリーンショット。" lightbox="media/amend-commit-new-git-lrg.png"::: </p>1. **[修正]** チェックボックスをクリックします。 <br>2. **[すべてコミット]** をクリックして、更新をコミットします。  |
|**変更の一時退避** | :::image type="content" source="media/stash-change-team-explorer-sml.png" alt-text="&quot;変更の一時退避&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [変更] ウィンドウのスクリーンショット。" lightbox="media/stash-change-team-explorer-lrg.png":::</p>1. **[一時退避]** ドロップダウンをクリックします。 <br>2.関連する **[一時退避]** オプションを選択します。 | :::image type="content" source="media/stash-change-new-git-sml.png" alt-text="&quot;変更の一時退避&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウのスクリーンショット。" lightbox="media/stash-change-new-git-lrg.png":::</p>1. **[すべてコミット]** ドロップダウンをクリックします。 <br>2.関連する **[一時退避]** オプションを選択します。 |

## <a name="synchronization"></a>Synchronization

|         |チーム エクスプローラー  |新しい Git エクスペリエンス |
|---------|---------|---------|
|**変更のフェッチ、プル、プッシュ** | :::image type="content" source="media/fetch-pull-push-team-explorer-sml.png" alt-text="&quot;フェッチ、プル、プッシュ&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [同期] ウィンドウのスクリーンショット。" lightbox="media/fetch-pull-push-team-explorer-lrg.png":::</p>1. **[同期]** ページに移動します。 <br>2.選択したネットワーク操作をクリックします。 | :::image type="content" source="media/fetch-pull-push-new-git-sml.png" alt-text="&quot;フェッチ、プル、プッシュ&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウのスクリーンショット。" lightbox="media/fetch-pull-push-team-new-git-lrg.png"::: </p>1. **[Git 変更]** ウィンドウで、フェッチ、プル、プッシュの各ボタンを探します。 <br>2.選択したネットワーク操作をクリックします。|
|**着信および発信コミットの表示** | :::image type="content" source="media/view-commits-team-explorer-sml.png" alt-text="&quot;着信および発信コミットの表示&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [同期] ウィンドウのスクリーンショット。" lightbox="media/view-commits-team-explorer-lrg.png"::: </p>1. **[同期]** ページに移動します。 <br>2.着信および発信リストを表示します。 | :::image type="content" source="media/view-commits-new-git-sml.png" alt-text="&quot;着信および発信コミットの表示&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウと [Git リポジトリ] ウィンドウのスクリーンショット。" lightbox="media/view-commits-new-git-lrg.png":::</p>1. **[Git 変更]** ウィンドウで、**発信または着信** リンクをクリックします。 <br>2. **[Git リポジトリ]** ウィンドウの上部にあるグラフ テーブルのアイコンを使用して、着信および発信コミットを表示します。 |

## <a name="branches"></a>ブランチ

|         |チーム エクスプローラー  |新しい Git エクスペリエンス |
|---------|---------|---------|
|**分岐を作成する** |  :::image type="content" source="media/create-branch-team-explorer-sml.png" alt-text="&quot;新しいブランチの作成&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [ブランチ] ウィンドウのスクリーンショット。" lightbox="media/create-branch-team-explorer-lrg.png":::</p>1. **[ブランチ]** ウィンドウに移動します。 <br> 2. **[新しいブランチ]** をクリックします。 | :::image type="content" source="media/create-branch-new-git-sml.png" alt-text="&quot;新しいブランチの作成&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウのスクリーンショット。" lightbox="media/create-branch-new-git-lrg.png"::: </p>1. **[Git 変更]** ウィンドウで、ブランチ ドロップダウン リストをクリックします。 <br>2. **[新しいブランチ]** をクリックします。 |
|**リモート ブランチからの最近の変更の取得** | :::image type="content" source="media/sync-remote-team-explorer-sml.png" alt-text="&quot;リモート ブランチからの最近の変更の取得&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [ブランチ] ウィンドウのスクリーンショット。" lightbox="media/sync-remote-team-explorer-lrg.png"::: </p>1. **[ブランチ] ページ** に移動します。 <br>2.リモート ブランチを右クリックし、 **[マージ元]** または **[Rebase Onto]\(リベース先\)** を選択します。  | :::image type="content" source="media/sync-remote-new-git-sml.png" alt-text="&quot;リモート ブランチからの最近の変更の取得&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウのスクリーンショット。" lightbox="media/sync-remote-new-git-lrg.png":::</p>1.ブランチ ドロップダウン リストをクリックします。 <br>2. **[リモート]** タブでリモート ブランチをクリックし、 **[Merge into Current Branch]\(現在のブランチにマージ\)** または **[Rebase Current Branch onto]\(現在のブランチのリベース先\)** を選択します。  |
|**ブランチを管理する** | :::image type="content" source="media/manage-branches-team-explorer-sml.png" alt-text="&quot;ブランチの管理&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [ブランチ] ウィンドウのスクリーンショット。" lightbox="media/manage-branches-team-explorer-lrg.png"::: </p>1. **[ブランチ]** ウィンドウに移動します。 <br>2.管理するブランチを右クリックします。 <br>3.ブランチの **履歴** を表示して、コミットを管理します。 | :::image type="content" source="media/manage-branches-new-git-sml.png" alt-text="Visual Studio 2019 でブランチを管理するために使用する 3 つの UI オプションのスクリーンショット コラージュ。" lightbox="media/manage-branches-new-git-lrg.png"::: </p>1.次のいずれかのエントリ ポイントを使用して、[Git リポジトリ] ウィンドウに移動します。 <br><br>a. 最上位の Visual Studio メニューで、 **[Git]**  >  **[ブランチの管理]** を選択します。<br> b. **[Git 変更]**  >  **[着信/発信]** を選択します。 <br>c. 右下にあるステータス バー メニューで、 **[ブランチの管理]** を選択します。<br> <br> 2.最上位の **[Git]**  >  **[ブランチの管理]** メニューで、次のいずれかの操作を実行します。 <br><br>A. ブランチを右クリックします。<br>B. 管理するコミットを複数選択します。 |

## <a name="conflict-resolution"></a>競合の解決

|         |チーム エクスプローラー  |新しい Git エクスペリエンス |
|---------|---------|---------|
|**競合のあるファイルのリストへのアクセス** | :::image type="content" source="media/resolve-conflicts-team-explorer-sml.png" alt-text="プロシージャ オーバーレイを含む、Visual Studio 2019 のチーム エクスプローラーの [変更] ウィンドウと [競合の解決] ウィンドウのスクリーンショット コラージュ。" lightbox="media/resolve-conflicts-team-explorer-lrg.png":::</p>1. **[競合]** リンクをクリックして、 **[競合の解決]** ウィンドウに移動します。 <br> 2. **[競合]** リストを使用して、マージの競合を解決します。 | :::image type="content" source="media/resolve-conflicts-new-git-sml.png" alt-text="&quot;競合の解決&quot; プロシージャ オーバーレイを含む、Visual Studio 2019 の [Git 変更] ウィンドウのスクリーンショット。" lightbox="media/resolve-conflicts-new-git-lrg.png"::: </p>1. **[Merge in progress with conflicts]\(競合のあるマージが進行中\)** が表示されることを確認します。 <br>2. **[Git 変更]** ウィンドウの **[Unmerged Changes]\(マージされていない変更\)** セクションに、マージの競合があるファイルのリストが表示されます。 <br>競合を解決します。 |

## <a name="next-steps"></a>次のステップ

新しい Git エクスペリエンスの詳細については、YouTube の最新のビデオ「[Visual Studio の Git の概要](https://www.youtube.com/watch?v=GCZ9x3yqkyc)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio での新しい Git エクスペリエンス](git-with-visual-studio.md)
- [Visual Studio で Git と GitHub の使用を開始する](/learn/modules/visual-studio-github-push/)
- [Visual Studio の GitHub アカウントを使って作業する](../ide/work-with-github-accounts.md)