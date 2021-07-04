---
title: 'チュートリアル: Visual Studio 2019 でリポジトリからプロジェクトを開く'
description: Visual Studio 2019 を使用して Git または Azure DevOps リポジトリのプロジェクトを開く方法について説明します。
ms.custom: vs-acquisition, get-started
ms.date: 03/18/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
monikerRange: vs-2019
ms.openlocfilehash: b6f7cd57a1753ca5926ac73a9bb4c8c918d1bd10
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389944"
---
# <a name="tutorial-open-a-project-from-a-repo"></a>チュートリアル: リポジトリからプロジェクトを開く

このチュートリアルでは、最初に Visual Studio を使ってリポジトリに接続した後、そこからプロジェクトを開きます。

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

## <a name="open-a-project-from-a-github-repo"></a>GitHub リポジトリからプロジェクトを開く

Visual Studio 2019 を使用して GitHub リポジトリからプロジェクトを開く方法は、使用しているバージョンによって異なります。 具体的には、[**バージョン 16.8**](/visualstudio/releases/2019/release-notes/) 以降をインストールしてある場合は、より完全に統合された新しい [Git エクスペリエンスを Visual Studio で](../ide/git-with-visual-studio.md)利用できます。

ただし、どのバージョンがインストールされていても、Visual Studio を使用して GitHub リポジトリからプロジェクトを開くことはいつでもできます。

#### <a name="168-and-later"></a>[16.8 以降](#tab/vs168later)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>GitHub リポジトリをクローンしてからプロジェクトを開く

1. Visual Studio 2019 を開きます。

1. 開始ウィンドウで、 **[リポジトリを複製]** を選択します。

   ![Visual Studio 2019 バージョン 16.8 以降での [リポジトリの複製] ダイアログのスクリーンショット](../ide/media/vs-2019/clone-repository.png)

1. リポジトリの場所を入力し、 **[複製]** を選択します。

   ![Visual Studio 2019 バージョン 16.8 以降で Git リポジトリの URL を入力する [リポジトリの複製] ダイアログのスクリーンショット](../ide/media/vs-2019/clone-repository-enter-location.png)

1. **[Git ユーザー情報]** ダイアログ ボックスで、ユーザーのサインイン情報を求められる場合があります。 情報を追加するか、既定で提供される情報を編集することができます。

   ![Visual Studio 2019 バージョン 16.8 以降でアカウント情報を入力または編集する [Git ユーザー情報] ダイアログのスクリーンショット](../ide/media/vs-2019/git-user-information-dialog.png)

    **[保存]** を選択して、グローバルな .gitconfig ファイルに情報を追加します。 (または、 **[キャンセル]** を選択して、後でこれを行うこともできます。)

    > [!TIP]
    > Visual Studio へのサインインの詳細については、「[Visual Studio にサインイン](../ide/signing-in-to-visual-studio.md)」ページを参照してください。 また、GitHub アカウントを使用してサインインする方法の詳細については、「[Visual Studio の GitHub アカウントを使って作業する](../ide/work-with-github-accounts.md)」ページを参照してください。

    次に、Visual Studio によって自動的にリポジトリからソリューションが読み込まれて開かれます。

   ![Visual Studio 2019 バージョン 16.8 以降のソリューション エクスプローラーで開かれている Git のプロジェクトのスクリーンショット](../ide/media/vs-2019/git-solution-explorer.png )

1. リポジトリに複数のソリューションが含まれている場合は、ソリューション エクスプローラーにそれらが表示されます。 ソリューション エクスプローラーで **[表示形式の切り替え]** ボタンを選択することにより、ソリューションの一覧を表示できます。

   ![Visual Studio 2019 バージョン 16.8 以降で、[表示形式の切り替え] ボタンが強調表示されている、ソリューション エクスプローラーで開かれている Git のプロジェクトのスクリーンショット](../ide/media/vs-2019/git-solution-explorer-switch-views.png)

   その後、ソリューション エクスプローラーには、**フォルダー ビュー** でルート フォルダーを開くか、ソリューション ファイルを選択して開くためのオプションが表示されます。

   ![Visual Studio 2019 バージョン 16.8 以降で [表示形式の切り替え] ボタンを選択した後、ソリューション エクスプローラーで開かれている Git の .sln ファイルのスクリーンショット](../ide/media/vs-2019/git-solution-explorer-view-solution.png)

    ビューを切り替えるには、 **[表示形式の切り替え]** ボタンをもう一度選択します。

    > [!TIP]
    > Visual Studio IDE の **[Git]** メニューを使用して、リポジトリをクローンし、プロジェクトを開くこともできます。
    >
    > ![Visual Studio 2019 バージョン 16.8 以降での [Git] メニューのスクリーンショット](../ide/media/vs-2019/git-menu-clone-create-git-repository.png)

#### <a name="open-a-project-locally-from-a-previously-cloned-github-repo"></a>以前にクローンした GitHub リポジトリからローカル環境でプロジェクトを開く

1. Visual Studio 2019 を開きます。

1. 開始ウィンドウで、 **[プロジェクトやソリューションを開く]** を選択します。

    Visual Studio によってエクスプローラーのインスタンスが開かれ、そこでソリューションまたはプロジェクトを参照して選択し、それを開くことができます。

   ![Visual Studio 2019 バージョン 16.8 以降の [プロジェクトやソリューションを開く] ウィンドウのスクリーンショット](../ide/media/vs-2019/open-local-project-from-cloned-repo.png)

    最近開いたプロジェクトまたはソリューションがある場合は、 **[最近開いた項目]** セクションから選択して、すぐに開くことができます。

    > [!TIP]
    > また、Visual Studio IDE の **[Git]** メニューを使用して、以前にクローンしたリポジトリから、ローカル環境のフォルダーやファイルを開くこともできます。
    >
    > ![Visual Studio 2019 バージョン 16.8 以降で [Local Repositories]\(ローカル リポジトリ\) オプションが展開されている [Git] メニューのスクリーンショット](../ide/media/vs-2019/git-menu-local-repositories.png)

    コーディングを始めます

#### <a name="167-and-earlier"></a>[16.7 以前](#tab/vs167earlier)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>GitHub リポジトリをクローンしてからプロジェクトを開く

1. Visual Studio 2019 を開きます。

1. 開始ウィンドウで、 **[コードを複製またはチェックアウトする]** を選択します。

   ![Visual Studio 2019 バージョン 16.7 以前での [新しいプロジェクトの作成] ウィンドウのスクリーンショット](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. リポジトリの場所を入力し、 **[複製]** を選択します。

   ![Visual Studio 2019 バージョン 16.7 以前での [コードを複製またはチェックアウトする] ウィンドウのスクリーンショット](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Visual Studio でリポジトリからプロジェクトが開かれます。

1. 使用可能なソリューション ファイルがある場合は、それが "ソリューションおよびフォルダー" スライド アウト メニューに表示されます。 それを選択すると、Visual Studio でソリューションが開かれます。

   ![Visual Studio 2019 バージョン 16.7 以前でのソリューション エクスプローラーのドロップダウン リストのスクリーンショット](./media/open-proj-repo-github-solutions-folders-picker.png)

   リポジトリ内にソリューション ファイル (具体的には、.sln ファイル) がない場合は、ポップアップ メニューに "ソリューションが見つかりません" と表示されます。 ただし、フォルダーのメニューから任意のファイルをダブルクリックして、それを Visual Studio コード エディターで開くことができます。

    コーディングを始めます

---

> [!NOTE]
> Visual Studio 2017 に固有の問題については、[Visual Studio 2017 でリポジトリのプロジェクトを開く](tutorial-open-project-from-repo-visual-studio-2017.md)方法に関するページを参照してください。

## <a name="connect-to-an-azure-devops-server"></a>Azure DevOps サーバーに接続する

Visual Studio 2019 を使用して Azure DevOps サーバーに接続したときに表示される内容は、使用しているバージョンによって異なります。 具体的には、[**バージョン 16.8**](/visualstudio/releases/2019/release-notes/) 以降をインストールしてある場合は、より完全に統合された新しい [Visual Studio の Git エクスペリエンス](../ide/git-with-visual-studio.md)を利用できるように UI が変更されています。

ただし、どのバージョンがインストールされていても、Visual Studio でいつでも Azure DevOps サーバーに接続できます。

#### <a name="168-and-later"></a>[16.8 以降](#tab/vs168later)

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

#### <a name="167-and-earlier"></a>[16.7 以前](#tab/vs167earlier)

1. Visual Studio 2019 を開きます。

1. 開始ウィンドウで、 **[コードを複製またはチェックアウトする]** を選択します。

   ![Visual Studio 2019 バージョン 16.7 以前での [新しいプロジェクトの作成] ウィンドウのスクリーンショット](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. **[リポジトリを参照する]** セクションで、 **[Azure DevOps]** を選択します。

   ![Visual Studio 2019 バージョン 16.7 以前の、Azure DevOps の一覧が表示される [リポジトリを参照する] セクションが含まれる [コードを複製またはチェックアウトする] ウィンドウのスクリーンショット](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   サインイン ウィンドウが表示される場合は、アカウントにサインインします。

1. **[プロジェクトに接続]** ダイアログ ボックスで、接続するリポジトリを選択してから、 **[クローン]** を選択します。

      ![Visual Studio 2019 バージョン 16.7 以前から生成される [プロジェクトに接続] ダイアログ ボックスのスクリーンショット](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > リスト ボックスに表示される内容は、自分がアクセスできる Azure DevOps リポジトリによって異なります。

   複製が完了すると、Visual Studio で **[チーム エクスプローラー]** が開いて通知が表示されます。

     ![Visual Studio 2019 バージョン 16.7 以前の、クローンが完了した後の [チーム エクスプローラー] ウィンドウのスクリーンショット](./media/vs-2019/clone-complete-azure-devops.png)

1. フォルダーやファイルを表示するには、 **[フォルダー ビューの表示]** リンクを選択します。

     ![Visual Studio 2019 バージョン 16.7 以前の、クローンが完了した後の [チーム エクスプローラー] ウィンドウの [ソリューション] セクションのスクリーンショット](./media/vs-2019/show-folder-view-azure-devops.png)

     Visual Studio で **[ソリューション エクスプローラー]** が開きます。

1. **[ソリューションおよびフォルダー]** リンクを選択し、ソリューション ファイル (具体的には .sln ファイル) を検索して開きます。

      ![Visual Studio 2019 バージョン 16.7 以前の、チーム エクスプローラーからの "ソリューションおよびフォルダー" 通知のスクリーンショット](./media/open-proj-repo-solutions-folders.png)

   リポジトリにソリューション ファイルがない場合は、"ソリューションが見つかりません" というメッセージが表示されます。 ただし、フォルダーのメニューから任意のファイルをダブルクリックして、それを Visual Studio コード エディターで開くことができます。

---

## <a name="next-steps"></a>次のステップ

Visual Studio を使ってコードを書く準備が整ったら、次の言語固有のチュートリアルのいずれかを開始します。

- [Visual Studio のチュートリアル | **C#**](./csharp/index.yml)
- [Visual Studio のチュートリアル | **Visual Basic**](./visual-basic/index.yml)
- [Visual Studio のチュートリアル | **C++**](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio のチュートリアル | **Python**](../python/index.yml)
- [Visual Studio のチュートリアル | **JavaScript**、**TypeScript**、**Node.js**](../javascript/index.yml)

## <a name="see-also"></a>関連項目

- [Visual Studio 2017 でリポジトリからプロジェクトを開く](tutorial-open-project-from-repo-visual-studio-2017.md)
- [Visual Studio 2019 での新しい Git エクスペリエンス](../ide/git-with-visual-studio.md)
- [Git とチーム エクスプローラーを並べて比較する](../ide/git-team-explorer-feature-comparison.md)
- [Azure DevOps Services:Azure Repos と Visual Studio の概要](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn:Azure DevOps の概要](/learn/modules/get-started-with-devops/)
