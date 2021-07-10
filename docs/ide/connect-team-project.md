---
title: チーム エクスプローラーのプロジェクトに接続する
description: Visual Studio でチーム エクスプローラーを使用し、チーム メンバーと連携してプロジェクトを開発および管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/11/2021
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jillfra
monikerRange: <=vs-2019
ms.openlocfilehash: b45399f7a4115ce5946a67caca22ca92148e7434
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308247"
---
# <a name="connect-to-projects-in-team-explorer"></a>チーム エクスプローラーのプロジェクトに接続する

::: moniker range="vs-2017"

**チーム エクスプローラー** ツール ウィンドウを使用し、プロジェクトの開発に必要なプログラミング作業を他のチーム メンバーとの間で調整し、自分、チーム、またはプロジェクトに割り当てられている作業を管理します。 **チーム エクスプローラー** は Git と GitHub のリポジトリ、Team Foundation バージョン管理 (TFVC) のリポジトリ、[Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) またはオンプレミス [Azure DevOps Server](/azure/devops/index-all) (以前の TFS) でホストされているプロジェクトに Visual Studio を接続します。 ソース コード、作業項目、およびビルドを管理できます。

::: moniker-end

::: moniker range="vs-2019"

チーム エクスプローラーにより Team Foundation バージョン管理 (TFVC) のリポジトリと、[Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) またはオンプレミス [Azure DevOps Server](/azure/devops/user-guide/about-azure-devops-services-tfs?view=azure-devops&preserve-view=true) (以前の TFS) でホストされているプロジェクトに Visual Studio が接続されます。 ソース コード、作業項目、およびビルドを管理できます。

> [!IMPORTANT]
> Visual Studio 2019 [**バージョン 16.8**](/visualstudio/releases/2019/release-notes-history) のリリースでは、Git バージョン コントロール エクスペリエンスが既定でオンになっています。 チーム エクスプローラーとの違いに関する詳細については、「[**Git とチーム エクスプローラーを並べて比較する**](../version-control/git-team-explorer-feature-comparison.md)」ページを参照してください。
>
> ただし、引き続きチーム エクスプローラーをお使いになる場合は、 **[ツール]** 、 **[オプション]** 、 **[環境]** 、 **[プレビュー機能]** の順に移動してから、 **[New Git user experience]\(新しい Git ユーザー エクスペリエンス\)** チェックボックスを切り替えます。

チーム エクスプローラーを使用してプロジェクトに接続する方法は、お使いの Visual Studio 2019 のバージョンによって異なります。

## <a name="in-version-168-and-later"></a>バージョン 16.8 以降の場合

1. Visual Studio 2019 を開きます。

1. 開始ウィンドウで、 **[リポジトリを複製]** を選択します。

   ![Visual Studio 2019 バージョン 16.8 以降での Azure DevOps 用の [リポジトリの複製] ダイアログのスクリーンショット](../ide/media/vs-2019/clone-repository.png)

1. **[リポジトリを参照する]** セクションで、 **[Azure DevOps]** を選択します。

    ![Visual Studio 2019 バージョン 16.8 以降での [プロジェクトに接続] ダイアログ ボックスの [リポジトリを参照する] セクションのスクリーンショット](../ide/media/vs-2019/browse-repository-azure-devops.png)

1. サインイン ウィンドウが表示される場合は、アカウントにサインインします。

1. **[プロジェクトに接続]** ダイアログ ボックスで、接続するリポジトリを選択してから、 **[クローン]** を選択します。

      ![Visual Studio 2019 バージョン 16.8 以降から生成される [プロジェクトに接続] ダイアログ ボックスのスクリーンショット](../ide/media/vs-2019/connect-project-azure-devops.png)

      > [!TIP]
      > 事前に設定された接続先リポジトリの一覧が表示されない場合は、 **[Azure DevOps Server の追加]** を選択してサーバーの URL を入力します。 (または、既存の Azure DevOps Server を追加したり、Azure DevOps アカウントを作成したりするためのリンクが含まれる、"サーバーは見つかりませんでした" というプロンプトが表示されることもあります。)

   次に、Visual Studio によって **ソリューション エクスプローラー** が開かれてフォルダーとファイルが表示されます。

1. **[チーム エクスプローラー]** タブを選択して、Azure DevOps のアクションを表示します。

      ![Visual Studio 2019 バージョン 16.8 以降から生成される [チーム エクスプローラー] ダイアログ ボックスのスクリーンショット](../ide/media/vs-2019/team-explorer-azure-devops.png)

## <a name="in-version-167-and-earlier"></a>バージョン 16.7 以前の場合

1. Visual Studio 2019 を開きます。

1. 開始ウィンドウで、 **[コードを複製またはチェックアウトする]** を選択します。

   ![Visual Studio 2019 バージョン 16.7 以前での [新しいプロジェクトの作成] ウィンドウのスクリーンショット](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. **[リポジトリを参照する]** セクションで、 **[Azure DevOps]** を選択します。

   ![Visual Studio 2019 バージョン 16.7 以前の、Azure DevOps の一覧が表示される [リポジトリを参照する] セクションが含まれる [コードを複製またはチェックアウトする] ウィンドウのスクリーンショット](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   サインイン ウィンドウが表示される場合は、アカウントにサインインします。

1. **[プロジェクトに接続]** ダイアログ ボックスで、接続するリポジトリを選択してから、 **[クローン]** を選択します。

      ![Visual Studio 2019 バージョン 16.7 以前から生成される [プロジェクトに接続] ダイアログ ボックスのスクリーンショット](../get-started/media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > リスト ボックスに表示される内容は、自分がアクセスできる Azure DevOps リポジトリによって異なります。

   複製が完了すると、Visual Studio で **[チーム エクスプローラー]** が開いて通知が表示されます。

     ![Visual Studio 2019 バージョン 16.7 以前の、クローンが完了した後の [チーム エクスプローラー] ウィンドウのスクリーンショット](../get-started/media/vs-2019/clone-complete-azure-devops.png)

1. フォルダーやファイルを表示するには、 **[フォルダー ビューの表示]** リンクを選択します。

     ![Visual Studio 2019 バージョン 16.7 以前の、クローンが完了した後の [チーム エクスプローラー] ウィンドウの [ソリューション] セクションのスクリーンショット](../get-started/media/vs-2019/show-folder-view-azure-devops.png)

     Visual Studio で **[ソリューション エクスプローラー]** が開きます。

1. **[ソリューションおよびフォルダー]** リンクを選択し、ソリューション ファイル (具体的には .sln ファイル) を検索して開きます。

      ![Visual Studio 2019 バージョン 16.7 以前の、チーム エクスプローラーからの "ソリューションおよびフォルダー" 通知のスクリーンショット](../get-started/media/open-proj-repo-solutions-folders.png)

   リポジトリにソリューション ファイルがない場合は、"ソリューションが見つかりません" というメッセージが表示されます。 ただし、フォルダーのメニューから任意のファイルをダブルクリックして、それを Visual Studio コード エディターで開くことができます。

::: moniker-end

::: moniker range="vs-2017"

![チーム エクスプローラー[ホーム] ページ (Visual Studio)](media/team-explorer/team-explorer.png "チーム エクスプローラー - [ホーム] ページ (Visual Studio)。")

> [!TIP]
> Visual Studio を開いても **チーム エクスプローラー** が表示されない場合、メニュー バーで **[表示]**  >  **[チーム エクスプローラー]** の順に選択するか、**Ctrl**+ **&#92;** 、**Ctrl**+**M** の順に押して開いてください。

## <a name="connect-to-a-project-or-repository"></a>プロジェクトまたはリポジトリに接続する

**[接続]** ページでプロジェクトまたはリポジトリに接続します。

![チーム エクスプローラーの [接続] ページ](media/team-explorer/connect.png "チーム エクスプローラー - [接続] ページ (Visual Studio)")

プロジェクトに接続するには:

1. **[接続の管理]** アイコンを選択し、 **[接続]** ページを開きます。

   ![チーム エクスプローラーの [接続の管理] ボタン](media/team-explorer/manage-connections.png "チーム エクスプローラー - [接続の管理] ボタン (Visual Studio)。")

1. **[接続]** ページで、 **[接続の管理]** 、 **[プロジェクトに接続]** の順に選択します。

   ![チーム エクスプローラーのプロジェクトに接続する](media/team-explorer/connect-project.png "チーム エクスプローラー - [プロジェクトに接続] (Visual Studio)。")

> [!TIP]
> リポジトリからプロジェクトを開く場合は、[リポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo-visual-studio-2017.md)方法に関するページを参照してください。 新しいプロジェクトを作成するか、ユーザーをプロジェクトに追加する場合、[プロジェクトの作成 (Azure DevOps)](/azure/devops/organizations/projects/create-project)と、[プロジェクトまたはチームへのユーザーの追加 (Azure DevOps)](/azure/devops/organizations/security/add-users-team-project)に関するページを参照してください。

::: moniker-end

## <a name="see-also"></a>関連項目

- [Git とチーム エクスプローラーを並べて比較する](git-team-explorer-feature-comparison.md)
- [Visual Studio での新しい Git エクスペリエンス](git-with-visual-studio.md)
- [チーム エクスプローラーのリファレンス](reference/team-explorer-reference.md)
- [プロジェクトに接続する (Azure DevOps)](/azure/devops/organizations/projects/connect-to-projects)
- [プロジェクトへの接続のトラブルシューティング](/azure/devops/user-guide/troubleshoot-connection?view=azure-devops&preserve-view=true)
