---
title: 'チュートリアル: Visual Studio 2017 でリポジトリからプロジェクトを開く'
description: Visual Studio 2017 を使って Git または Azure DevOps リポジトリのプロジェクトを開く方法について学習します。
ms.custom: vs-acquisition, get-started
ms.date: 02/15/2021
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
monikerRange: vs-2017
ms.openlocfilehash: 5543a568f7246d9600ba375d9a1cf19af4cbd2d4
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389203"
---
# <a name="tutorial-open-a-project-from-a-repo-in-visual-studio-2017"></a>チュートリアル: Visual Studio 2017 でリポジトリからプロジェクトを開く

このチュートリアルでは、最初に Visual Studio 2017 を使ってリポジトリに接続した後、そこからプロジェクトを開きます。

> [!TIP]
> [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) には、GitHub リポジトリに接続するための新しく、より完全に統合された方法があります。 詳細については、[**Visual Studio 2019 での新しい Git エクスペリエンス**](../ide/git-with-visual-studio.md?view=vs-2019&preserve-view=true)に関するページを参照してください。

## <a name="open-a-project-from-a-github-repo-by-using-visual-studio-2017"></a>Visual Studio 2017 を使って GitHub リポジトリからプロジェクトを開く

1. Visual Studio 2017 を開きます。

1. 上部のメニュー バーで、 **[ファイル]**  >  **[開く]**  >  **[ソース管理から開く]** の順に選択します。

   **[チーム エクスプローラー - 接続]** ページが開きます。

    ![Visual Studio IDE 内の [チーム エクスプローラー] ウィンドウ](./media/open-proj-repo-team-explorer.png)

1. **[ローカル Git リポジトリ]** セクションで、 **[クローン]** を選択します。

    ![[ローカル Git リポジトリ] セクションから [複製] を選択する](./media/open-proj-repo-local-git-repo-clone.png)

1. "**複製する Git リポジトリの URL を入力してください**" と表示されているボックスに、リポジトリの URL を入力または貼り付けてから、_*Enter** キーを押します。 (GitHub にサインインするよう求められた場合は、サインインします。)

   Visual Studio でリポジトリが複製されると、チーム エクスプローラーが閉じてソリューション エクスプローラーが開きます。 "*ソリューションの一覧を表示するには、上記のソリューションおよびフォルダーをクリックします*" というメッセージが表示されます。 **[ソリューションおよびフォルダー]** を選択します。

   ![ソリューション エクスプローラーから "ソリューションおよびフォルダー" を選択する](./media/open-proj-repo-github-solutions-folders.png)

1. 使用可能なソリューション ファイルがある場合は、それが "ソリューションおよびフォルダー" スライド アウト メニューに表示されます。 それを選択すると、Visual Studio でソリューションが開きます。

   ![ソリューション エクスプローラーのドロップダウン リストから開きたいものを選択する](./media/open-proj-repo-github-solutions-folders-picker.png)

   リポジトリ内にソリューション ファイル (具体的には、.sln ファイル) がない場合は、スライド アウト メニューに "ソリューションが見つかりません" と表示されます。 ただし、フォルダーのメニューから任意のファイルをダブルクリックして、それを Visual Studio コード エディターで開くことができます。

### <a name="review-your-work"></a>作業内容の確認

次のアニメーションを見て、前のセクションで完了した作業を確認します。

   ![Visual Studio を使って GitHub リポジトリのプロジェクトを開くアニメーション](./media/open-project-from-github.gif)

> [!NOTE]
> Visual Studio 2019 に固有の問題については、[Visual Studio 2019 でリポジトリのプロジェクトを開く](tutorial-open-project-from-repo-visual-studio-2019.md)方法に関するページを参照してください。

## <a name="open-a-project-from-an-azure-devops-repo-by-using-visual-studio-2017"></a>Visual Studio 2017 を使って Azure DevOps リポジトリからプロジェクトを開く

1. Visual Studio 2017 を開きます。

1. 上部のメニュー バーで、 **[ファイル]**  >  **[開く]**  >  **[ソース管理から開く]** の順に選択します。

   **[チーム エクスプローラー - 接続]** ページが開きます。

    ![Visual Studio IDE 内の [チーム エクスプローラー] ウィンドウ](./media/open-proj-repo-team-explorer.png)

1. Azure DevOps リポジトリに接続するには、次の 2 つの方法があります。

      - **[ホストされるサービスのプロバイダー]** セクションで、 **[接続...]** を選択します。

        ![Visual Studio IDE 内のチーム エクスプローラー ウィンドウの [ホストされるサービスのプロバイダー] セクション](./media/open-proj-repo-azure-devops.png)

      - **[接続の管理]** ドロップダウン リストで、 **[プロジェクトに接続...]** を選択します。

        ![Visual Studio IDE 内のチーム エクスプローラー ウィンドウの [接続の管理] セクション](./media/open-proj-repo-azuredevops-manage-connections.png)

1. **[プロジェクトに接続]** ダイアログ ボックスで、接続するリポジトリを選択してから、 **[クローン]** を選択します。

      ![Visual Studio から生成される [プロジェクトに接続] ダイアログ ボックス](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > リスト ボックスに表示される内容は、自分がアクセスできる Azure DevOps リポジトリによって異なります。

1. Visual Studio でリポジトリが複製されると、チーム エクスプローラーが閉じてソリューション エクスプローラーが開きます。 "*ソリューションの一覧を表示するには、上記のソリューションおよびフォルダーをクリックします*" というメッセージが表示されます。 **[ソリューションおよびフォルダー]** を選択します。

      ![Visual Studio のチーム エクスプローラーからの "ソリューションおよびフォルダー" 通知](./media/open-proj-repo-solutions-folders.png)

   ソリューション ファイル (具体的には、.sln ファイル) が "ソリューションおよびフォルダー" スライド アウト メニューに表示されます。 それを選択すると、Visual Studio でソリューションが開きます。

   リポジトリ内にソリューション ファイルがない場合は、スライド アウト メニューに "ソリューションが見つかりません" と表示されます。 ただし、フォルダーのメニューから任意のファイルをダブルクリックして、それを Visual Studio コード エディターで開くことができます。

## <a name="next-steps"></a>次のステップ

Visual Studio 2017 を使ってコードを書く準備が整ったら、次の言語固有のチュートリアルのいずれかを確認します。

- [Visual Studio のチュートリアル | **C#**](./csharp/index.yml)
- [Visual Studio のチュートリアル | **Visual Basic**](./visual-basic/index.yml)
- [Visual Studio のチュートリアル | **C++**](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio のチュートリアル | **Python**](../python/index.yml)
- [Visual Studio のチュートリアル | **JavaScript**、**TypeScript**、**Node.js**](../javascript/index.yml)

## <a name="see-also"></a>関連項目

- [Visual Studio 2019 でリポジトリからプロジェクトを開く](tutorial-open-project-from-repo-visual-studio-2019.md)
- [Visual Studio 2019 での新しい Git エクスペリエンス](../ide/git-with-visual-studio.md)
- [Azure DevOps Services:Azure Repos と Visual Studio の概要](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn:Azure DevOps の概要](/learn/modules/get-started-with-devops/)
