---
title: 'クイック スタート: Visual Studio IDE のツアー'
description: Visual Studio 統合開発環境 (IDE) のウィンドウ、メニュー、その他の UI 機能の一部について説明します。
ms.custom: vs-acquisition
titleSuffix: ''
ms.date: 03/02/2021
ms.topic: quickstart
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0e3a0c62c1ec13ba6fec464a2903512b2acf33ad
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386294"
---
# <a name="quickstart-first-look-at-the-visual-studio-ide"></a>クイック スタート: Visual Studio IDE の表示の紹介

この 5 - 10 分程度の Visual Studio 統合開発環境 (IDE) の紹介では、ウィンドウやメニューなどの UI 機能の一部を説明します。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2017"

## <a name="start-page"></a>スタート ページ

ほとんどの場合、Visual Studio を開くと最初に **スタート ページ** が表示されます。 **スタート ページ** は、必要なコマンドとプロジェクト ファイルを見つけやすくする "ハブ" として設計されています。 **[最近]** セクションには、プロジェクトと最近作業したフォルダーが表示されます。 **[新しいプロジェクト]** の下にあるリンクをクリックすると、 **[新しいプロジェクト]** ダイアログ ボックスが開きます。また、 **[開く]** では、既存のコード プロジェクトやフォルダーを開くことができます。 右側には、最新の開発者向けニュース フィードが表示されます。

![Visual Studio の [スタート ページ]](media/start-page.png)

**スタート ページ** を閉じた後でもう一度表示する場合は、 **[ファイル]** メニューで再度開くことができます。

![Visual Studio の [ファイル] メニュー](media/quickstart-IDE-file-menu-large.png)

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="start-window"></a>スタート ウィンドウ

Visual Studio を開くと最初にスタート ウィンドウが表示されます。 スタート ウィンドウは、速やかに "コードに移動" できるようなデザインになっています。 コードを複製またはチェックアウトするオプション、既存のプロジェクトまたはソリューションを開くオプション、新しいプロジェクトを作成するオプション、いくつかのコード ファイルが含まれるフォルダーを開くためのオプションがあります。

[![Visual Studio 2019 のスタート ウィンドウ](media/vs-2019/start-window-labeled.png)](media/vs-2019/start-window-labeled.png#lightbox)

Visual Studio を初めて使用する場合、最近使用したプロジェクト リストは空になります。

MSBuild ベースではないコードベースを使用している場合、 **[ローカル フォルダーを開く]** オプションを使用し、Visual Studio でコードを開きます。 詳細については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。 そうでなければ、GitHub や Azure DevOps など、ソース プロバイダーから新しいプロジェクトを作成したり、プロジェクトを複製したりできます。

**[コードなしで続行]** オプションを使用すると、特定のプロジェクトやコードが読み込まれることなく、Visual Studio 開発環境が起動します。 [Live Share](/visualstudio/liveshare/) セッションに参加したり、デバッグ目的でプロセスに接続したりするとき、このオプションを選択することがあります。 **Esc** を押してスタート ウィンドウを閉じ、IDE を開くこともできます。

::: moniker-end

## <a name="create-a-project"></a>プロジェクトを作成する

Visual Studio の機能を引き続き確認するために、新しいプロジェクトを作成しましょう。

::: moniker range="vs-2017"

1. **[スタート ページ]** の **[新しいプロジェクト]** の下にある検索ボックスに「**console**」と入力し、プロジェクトの種類の一覧をフィルターして、名前に "console" が含まれるものに絞り込みます。

   ![Visual Studio の [スタート ページ] でプロジェクト テンプレートを検索する](media/start-page-search-templates.png)

   Visual Studio には、すぐにコーディングを開始するのに役立つ、さまざまな種類のプロジェクト テンプレートが用意されています。 C# の **[コンソール アプリ (.NET Core)]** プロジェクト テンプレートを選択します。 (Visual Basic、C++、Javascript など他の言語で開発している場合は、それらの言語のいずれかでプロジェクトを作成してもかまいません。 表示される UI はすべてのプログラミング言語でほぼ同じです)。

1. 表示された **[新しいプロジェクト]** ダイアログ ボックスで、既定のプロジェクト名をそのまま使用し、 **[OK]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

    :::image type="content" source="../get-started/media/vs-2019/start-window-create-new-project.png" alt-text="Visual Studio 2019 の [新しいプロジェクトの作成] ウィンドウのスクリーンショット。":::

   **[新しいプロジェクトの作成]** ウィンドウが開き、いくつかのプロジェクト "*テンプレート*" が表示されます。 テンプレートには、特定のプロジェクトの種類に必要な基本的なファイルと設定が含まれています。

   ここでは、プロジェクト テンプレートの検索、フィルター処理、選択を行うことができます。 また、ご自分で最近使ったプロジェクト テンプレートの一覧も表示されます。

1. 上部にある検索ボックスに「**コンソール**」と入力し、プロジェクトの種類の一覧をフィルターして、名前に "コンソール" が含まれるものに絞り込みます。 **[すべての言語]** ドロップダウン リストから **[C#]** (または他の適切な言語) を選択して、さらに検索の結果を絞り込みます。

    :::image type="content" source="media/vs-2019/create-new-project.png" alt-text="Visual Studio 2019 の [新しいプロジェクトの作成] ウィンドウのスクリーンショット。ここで必要なテンプレートを選択します。":::

1. 言語として C#、Visual Basic、または F# を選択した場合は、 **[コンソール アプリケーション]** テンプレートを選択し、 **[次へ]** を選択します。 (別の言語を選択した場合は、任意のテンプレートを選択します。 表示される UI はすべてのプログラミング言語でほぼ同じです)。

1. **[新しいプロジェクトの構成]** ウィンドウで、既定のプロジェクト名と場所をそのまま使用し、 **[次へ]** を選択します。

    :::image type="content" source="media/vs-2019/configure-new-project-console.png" alt-text="Visual Studio 2019 の [新しいプロジェクトの構成] ウィンドウのスクリーンショット。ここでプロジェクトの名前を入力します。":::

1. **[追加情報]** ウィンドウで、 **[ターゲット フレームワーク]** ドロップダウン メニューに **[.NET Core 3.1]** が表示されていることを確認し、 **[作成]** をクリックします。

    :::image type="content" source="../get-started/media/vs-2019/create-project-additional-info.png" alt-text="Visual Studio 2019 の [追加情報] ウィンドウのスクリーンショット。ここで必要な .NET Core フレームワークのバージョンを選択します。":::

::: moniker-end

   プロジェクトが作成され、*Program.cs* という名前のファイルが **[エディター]** ウィンドウに開きます。 **エディター** にファイルの内容が表示されます。Visual Studio でのコード作成作業のほとんどは、このエディターで行います。

   ![Visual Studio のエディター](media/editor.png)

## <a name="solution-explorer"></a>ソリューション エクスプローラー

通常は Visual Studio の右側にある **ソリューション エクスプローラー** には、プロジェクト、ソリューション、コード フォルダー内のファイルとフォルダーの階層がグラフィカルに表示されます。 **ソリューション エクスプローラー** 内で階層を移動し、ファイルを選択できます。

![Visual Studio のソリューション エクスプローラー](media/quickstart-IDE-solution-explorer.png)

## <a name="menus"></a>メニュー

Visual Studio の上部にあるメニュー バーには、コマンドがカテゴリごとにグループ化されています。 たとえば、 **[プロジェクト]** メニューには、作業中のプロジェクトに関連するコマンドが含まれています。 **[ツール]** メニューでは、 **[オプション]** を選択して Visual Studio の動作をカスタマイズしたり、 **[ツールと機能を取得]** を選択してインストールに機能を追加したりできます。

::: moniker range="vs-2017"

![Visual Studio 2017 のメニュー バー](media/quickstart-IDE-menu-bar.png)

::: moniker-end

::: moniker range=">=vs-2019"

![Visual Studio 2019 のメニュー バー](media/vs-2019/menu-bar.png)

::: moniker-end

## <a name="error-list"></a>エラー一覧

**[表示]** メニューの **[エラー一覧]** を選択して、 **[エラー一覧]** ウィンドウを開きます。

**[エラー一覧]** ウィンドウには、現在の状態のコードに関するエラー、警告、メッセージが表示されます。 ファイル、またはプロジェクト内のどこかにエラー (中かっこやセミコロンの欠落など) がある場合は、ここに一覧表示されます。

![Visual Studio の [エラー一覧]](media/quickstart-IDE-error-list.png)

## <a name="output-window"></a>[出力] ウィンドウ

**[出力]** ウィンドウには、プロジェクトのビルド時の出力メッセージや、ソース管理プロバイダーからの出力メッセージが表示されます。

プロジェクトをビルドして、ビルド出力をいくつか確認してみましょう。 **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。 自動的に **[出力]** ウィンドウにフォーカスされ、ビルドが成功したことを示すメッセージが表示されます。

![Visual Studio の [出力] ウィンドウ](media/build-output-minimal.png)

## <a name="search-box"></a>検索ボックス

検索ボックスを使用して、Visual Studio のほぼすべての場所にすばやく簡単に移動できます。 実行する操作に関連したテキストを入力すると、そのテキストに関係するオプションの一覧が表示されます。 たとえば、ビルドで実際に行われる内容をさらに詳しく表示するために、ビルド出力の詳細レベルを上げるとします。 これは次のように行います。

::: moniker range="vs-2017"

1. IDE の右上にある **[クイック起動]** 検索ボックスを見つけます。 (または、**Ctrl**+**Q** キーを押してアクセスします)。

2. 検索ボックスに「**詳細度**」と入力します。 **[オプション]** カテゴリで、表示された結果から **[プロジェクトおよびソリューション] --> [ビルド/実行]** を選択します。

   ![Visual Studio 2017 のクイック起動検索ボックス](media/quickstart-IDE-quick-launch.png)

   **[オプション]** ダイアログ ボックスが開き、 **[ビルド/実行]** オプションのページが表示されます。

::: moniker-end

::: moniker range=">=vs-2019"

1. IDE の上部の検索ボックスをアクティブにするには、**Ctrl** キーを押しながら **Q** キーを押します。

2. 検索ボックスに「**詳細度**」と入力します。 表示された結果から **[MSBuild の詳細度を変更する]** を選択します。

   ![Visual Studio 2019 の検索ボックス](media/vs-2019/quick-launch-verbosity.png)

   **[オプション]** ダイアログ ボックスが開き、 **[ビルド/実行]** オプションのページが表示されます。

::: moniker-end

3. **[MSBuild プロジェクト ビルドの出力の詳細]** で **[標準]** を選択し、 **[OK]** をクリックします。

4. **ソリューション エクスプローラー** で **[ConsoleApp1]** プロジェクトを右クリックし、コンテキスト メニューで **[リビルド]** を選択して、プロジェクトをもう一度ビルドします。

   今度は、 **[出力]** ウィンドウには、どの場所のどのファイルがコピーされたかなど、ビルド プロセスに関するより詳細なログが表示されます。

   ![Visual Studio の詳細なビルド出力](media/build-output-verbose.png)

## <a name="send-feedback-menu"></a>[フィードバックの送信] メニュー

Visual Studio の使用中に問題が発生した場合、または製品の改善案をお持ちの場合は、Visual Studio ウィンドウ上部の **[フィードバックの送信]** メニューを使用してください。

::: moniker range="vs-2017"

![Visual Studio 2017 の [フィードバックの送信] メニュー](media/quickstart-IDE-send-feedback.png)

::: moniker-end

::: moniker range=">=vs-2019"

![Visual Studio 2019 の [フィードバックの送信] メニュー](media/vs-2019/send-feedback-menu.png)

::: moniker-end

## <a name="next-steps"></a>次の手順

ユーザー インターフェイスに慣れるため、Visual Studio の機能をいくつか確認しました。 下記に従って、さらに試してみてください。

> [!div class="nextstepaction"]
> [コード エディターについて学習する](../get-started/tutorial-editor.md)

> [!div class="nextstepaction"]
> [プロジェクトとソリューションについて学習する](../get-started/tutorial-projects-solutions.md)

## <a name="see-also"></a>関連項目

- [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
- [Visual Studio のその他の機能](../ide/advanced-feature-overview.md)
- [テーマとフォントの色を変更する](../ide/quickstart-personalize-the-ide.md)
