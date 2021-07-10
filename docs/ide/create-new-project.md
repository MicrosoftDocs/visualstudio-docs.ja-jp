---
title: 新しいプロジェクトを作成する
description: Visual Studio で新しいプロジェクトを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/23/2020
ms.topic: how-to
f1_keywords:
- vs.newproject
helpviewer_keywords:
- projects [Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 05cfb7cf053a3275b49b76b46bec8054fb105078
ms.sourcegitcommit: 529e1716924c3e1ac8a750550b996ad3c79f353b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/14/2021
ms.locfileid: "112066957"
---
# <a name="create-a-new-project-in-visual-studio"></a>Visual Studio での新しいプロジェクトの作成

この記事では、Visual Studio で新しいプロジェクトをテンプレートからすばやく作成する方法について説明します。

::: moniker range="vs-2017"

## <a name="open-the-new-project-dialog"></a>[新しいプロジェクト] ダイアログ ボックスを開く

Visual Studio 2017 では、いくつかの方法で新しいプロジェクトを作成できます。 [スタート] ページでは、 **[プロジェクト テンプレートの検索]** ボックスにプロジェクト テンプレートの名前を入力するか、 **[新しいプロジェクトの作成]** リンクを選択して **[新しいプロジェクト]** ダイアログ ボックスを開きます。 [スタート] ページの他に、メニュー バーで **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択するか、ツール バーの **[新しいプロジェクト]** ボタンをクリックするという方法もあります。

![[ファイル] > [新規作成] > [プロジェクト] オプションの順に選択されている Visual Studio のメニュー バーのスクリーンショット。](./media/vside-newproject1.png)

## <a name="select-a-template-type"></a>テンプレートの種類を選択する

**[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** カテゴリの下に、利用できるプロジェクト テンプレートが一覧表示されます。 テンプレートは、Visual C#、JavaScript、Azure Data Lake など、プログラミング言語やプロジェクトの種類に基づいて整理されています。

![インストールされたテンプレートの一覧が表示されている [新しいプロジェクト] ダイアログ ボックスのスクリーンショット。](./media/vside-newproject-templates-list.png)

> [!NOTE]
> 利用できる言語またはプロジェクト テンプレートの一覧は、実行している Visual Studio のバージョンとインストールされているワークロードに基づいて表示されます。 追加ワークロードのインストール方法については、「[ワークロードやコンポーネントを追加または削除することで Visual Studio を変更する](../install/modify-visual-studio.md)」を参照してください。

言語名の隣にある三角形をクリックして使用するプログラミング言語用のテンプレート一覧を表示してから、プロジェクトのカテゴリ (Windows デスクトップなど) を選択します。

Visual C# .NET Core プロジェクトで利用できるプロジェクト テンプレートを次の図に示します。

![選択できるプロジェクト テンプレートが一覧表示されている [新しいプロジェクト] ダイアログ ボックスのスクリーンショット。](./media/new-project-dialog-net-core.png)

## <a name="configure-your-project"></a>プロジェクトを構成する

**[名前]** ボックスに新しいプロジェクトの名前を入力します。 プロジェクトはコンピューター上の既定の場所に保存することも、**[参照]** ボタンをクリックして別の保存場所を探すこともできます。 また、ソリューション名を選択することも、新しいプロジェクトを Git リポジトリに追加する ( **[ソース管理に追加]** を選択して) こともできます。

**[OK]** をクリックして、ソリューションとプロジェクトを作成します。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="open-the-create-a-new-project-page"></a>[新しいプロジェクトの作成] ページを開く

Visual Studio 2019 では、いくつかの方法で新しいプロジェクトを作成できます。 Visual Studio を初めて開くと、スタート ウィンドウが表示されます。そこから、 **[新しいプロジェクトの作成]** を選択できます。

:::image type="content" source="media/vs-2019/start-window-create-new-project.png" alt-text="Visual Studio 2019 の [スタート] ウィンドウからアクセスする [新しいプロジェクトの作成] ダイアログのスクリーンショット":::

Visual Studio 開発環境が既に開いている場合は、メニュー バーで **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択することで、新しいプロジェクトを作成できます。 ツールバーの **[新しいプロジェクト]** ボタンをクリックする、または **Ctrl** + **Shift** + **N** キーを押すという方法もあります。

:::image type="content" source="media/vs-2019/new-project-button.png" alt-text="Visual Studio 2019 の [新しいプロジェクト] ボタンのスクリーンショット。":::

## <a name="select-a-template-type"></a>テンプレートの種類を選択する

**[新しいプロジェクトの作成]** ページの左側に、最後に選択したテンプレートの一覧が表示されます。 テンプレートは、*使用した日時が新しい* 順に並べ替えられています。

最近使用したテンプレートの中から選択しない場合は、**言語** (C# や C++ など)、**プラットフォーム** (Windows や Azure など)、および **プロジェクトの種類** (デスクトップや Web など) によってフィルター処理することで、使用できるすべてのプロジェクト テンプレートを抽出することができます。 また、検索ボックスに検索テキスト (**asp.net** など) を入力して該当するテンプレートを抽出することもできます。

:::image type="content" source="media/vs-2019/create-new-project-filters.png" alt-text="Visual Studio 2019 のプロジェクト テンプレート フィルターのスクリーンショット。":::

各テンプレートの下に表示されるタグは、3 つのドロップダウン フィルター (言語、プラットフォーム、プロジェクトの種類) に対応します。

> [!TIP]
> 探しているテンプレートが見つからない場合は、Visual Studio 用のワークロードが欠落している可能性があります。 追加のワークロード (**[Azure 開発]** または **[.NET によるモバイル開発]** など) をインストールするには、**[さらにツールと機能をインストールする]** リンクをクリックして Visual Studio インストーラーを開きます。 インストールするワークロードをそこで選択し、次に **[変更]** を選択します。 その後、追加のプロジェクト テンプレートを選択できるようになります。
>
> :::image type="content" source="media/vs-2019/install-more-tools-features.png" alt-text="Visual Studio 2019 の [さらにツールと機能をインストールする] リンクのスクリーンショット。":::

テンプレートを選択してから、**[次へ]** をクリックします。

## <a name="configure-your-project"></a>プロジェクトを構成する

**[新しいプロジェクトの構成]** ページには、プロジェクト (とソリューション) への名前付け、ディスクの場所の選択、Framework のバージョンの選択 (選択したテンプレートに適用可能な場合) を行うためのオプションが用意されています。

:::image type="content" source="media/vs-2019/configure-new-project.png" alt-text="Visual Studio 2019 の [新しいプロジェクトの構成] ページのスクリーンショット。":::

> [!NOTE]
> Visual Studio 内に既に開かれているプロジェクトまたはソリューションがある場合に新しいプロジェクトを作成するには、追加の構成オプションを使用できます。 新しいソリューションの作成、または既に開いているソリューションへの新しいプロジェクトの追加を選択することができます。
>
> :::image type="content" source="media/vs-2019/configure-new-project-solution.png" alt-text="Visual Studio 2019 の [新しいソリューションの作成] または [ソリューションに追加] ダイアログのスクリーンショット。":::

**[作成]** をクリックして、新しいプロジェクトを作成します。

::: moniker-end

## <a name="add-additional-projects-to-a-solution"></a>ソリューションにさらにプロジェクトを追加する

ソリューションにさらにプロジェクトを追加する場合は、**ソリューション エクスプローラー** 内でソリューション ノードを右クリックして、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

> [!TIP]
> ステップ バイ ステップの手順とサンプル コードを備えた、最初から作成したプロジェクトとソリューションの例については、「[プロジェクトとソリューションについて理解する](../get-started/tutorial-projects-solutions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [プロジェクトとソリューションの概要](../get-started/tutorial-projects-solutions.md)
- [ソリューションとプロジェクトの使用](creating-solutions-and-projects.md)
- [プロジェクトおよびソリューションのプロパティの管理](managing-project-and-solution-properties.md)
- [プロジェクトの作成 (Visual Studio for Mac)](/visualstudio/mac/create-new-projects)
