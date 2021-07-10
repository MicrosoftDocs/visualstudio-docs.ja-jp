---
title: Visual Basic を使用して Windows フォーム アプリを作成する
description: Visual Studio で Visual Basic を使用して Windows フォーム アプリを作成する方法の詳細な手順を説明します。
ms.date: 09/27/2019
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.devlang: vb
author: j-martens
ms.author: jmartens
manager: jmartens
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 4d3c1aac5bb06ba29b1c70c39db900e704b2f3ec
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308325"
---
# <a name="create-a-windows-forms-app-in-visual-studio-with-visual-basic"></a>Visual Studio で Visual Basic を使用して Windows フォーム アプリを作成する

ここでは、Visual Studio 統合開発環境 (IDE) の概要を示し、Windows ベースのユーザー インターフェイス (UI) を備えた簡単な Visual Basic アプリケーションを作成します。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

> [!NOTE]
> このチュートリアルの一部のスクリーン ショットではダーク テーマが使用されています。 ダーク テーマを使用していないが、使用したい場合は、その方法について「[Visual Studio IDE とエディターのカスタマイズ](../ide/quickstart-personalize-the-ide.md)」ページを参照してください。

::: moniker-end

::: moniker range="vs-2022"

Visual Studio をまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

> [!NOTE]
> このチュートリアルの一部のスクリーン ショットではダーク テーマが使用されています。 ダーク テーマを使用していないが、使用したい場合は、その方法について「[Visual Studio IDE とエディターのカスタマイズ](../ide/quickstart-personalize-the-ide.md)」ページを参照してください。

::: moniker-end

## <a name="create-a-project"></a>プロジェクトを作成する

まず、Visual Basic アプリケーション プロジェクトを作成します。 このプロジェクトの種類には、必要とするすべてのテンプレート ファイルが付属していますので、何も追加する必要はありません。

::: moniker range="vs-2017"

1. Visual Studio 2017 を開きます。

1. 上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

1. 左側のウィンドウの **[新しいプロジェクト]** ダイアログ ボックスで、**[Visual Basic]** を展開し、**[Windows デスクトップ]** を選択します。 中央のウィンドウで、 **[Windows フォーム アプリケーション (.NET Framework)]** を選択します。 ファイルに `HelloWorld` という名前を付けます。

     **[Windows フォーム アプリケーション (.NET Framework)]** プロジェクト テンプレートが表示されない場合は、 **[新しいプロジェクト]** ダイアログ ボックスを取り消し、上部のメニュー バーで **[ツール]**  >  **[ツールと機能を取得]** を選択します。 Visual Studio インストーラーが起動します。 **.NET デスクトップ開発** ワークロードを選択し、 **[変更]** を選択します。

     ![Visual Studio インストーラーの .NET Core ワークロード](../ide/media/install-dot-net-desktop-env.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   ![[新しいプロジェクトの作成] ウィンドウを表示する](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. **[新しいプロジェクトの作成]** ウィンドウで、Visual Basic 用の **[Windows フォーム アプリケーション (.NET Framework)]** テンプレートを選択します。

   (必要に応じて、検索を絞り込んで目的のテンプレートにすばやくアクセスすることができます。 たとえば、検索ボックスに「*Windows フォーム アプリ*」と入力します。 次に、言語のリストから **[Visual Basic]** を選択して、プラットフォームのリストから **[Windows]** を選択します。)  

   ![Windows フォーム アプリ (.NET Framework) 用の Visual Basic テンプレートを選択する](../get-started/visual-basic/media/vs-2019/vb-create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > **[Windows フォーム アプリ (.NET Framework)]** テンプレートが表示されない場合は、 **[新しいプロジェクトの作成]** ウィンドウからそれをインストールすることができます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。
   >
   > ![[新しいプロジェクトの作成] ウィンドウに表示された [お探しの情報が見つかりませんでしたか?] での [さらにツールと機能をインストールする] リンク](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 次に、Visual Studio インストーラーで、 **[.NET デスクトップの開発]** ワークロードを選択します。
   >
   > ![Visual Studio インストーラーの .NET Core ワークロード](../ide/media/install-dot-net-desktop-env.png)
   >
   > その後、Visual Studio インストーラー内の **[変更]** ボタンをクリックします。 作業内容を保存するよう求められることがあります。その場合は、そのようにします。 次に、 **[続行]** を選択してワークロードをインストールします。 その後、この「[プロジェクトを作成する](#create-a-project)」プロシージャの手順 2 に戻ります。

1. **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*HelloWorld*」とタイプまたは入力します。 次に、 **[作成]** を選択します。

   ![[新しいプロジェクトの構成] ウィンドウで、ご自分のプロジェクトに 'HelloWorld' という名前を付けます。](../get-started/visual-basic/media/vs-2019/vb-name-your-winform-project-helloworld.png)

   Visual Studio によってその新しいプロジェクトが開かれます。

::: moniker-end

## <a name="create-the-application"></a>アプリケーションを作成する

Visual Basic プロジェクト テンプレートを選択し、ファイルに名前を付けると、Visual Studio によって目的のフォームが開かれます。 フォームは、Windows ユーザー インターフェイスです。 このフォームにコントロールを追加して "Hello World" アプリケーションを作成し、このアプリを実行します。

### <a name="add-a-button-to-the-form"></a>フォームにボタンを追加する

1. **[ツールボックス]** をクリックして、ツールボックスのスライド アウト ウィンドウを開きます

     ![[ツールボックス] をクリックして [ツールボックス] ウィンドウを開く](../ide/media/vb-toolbox-toolwindow.png)

     (**ツールボックス** のスライド アウト オプションが表示されない場合は、メニュー バーから開くことができます。 これを行うには、 **[表示]**  >  **[ツールボックス]** を選択します。 または、**Ctrl**+**Alt**+**X** キーを押します)。

1. **[ピン設定]** アイコンをクリックして、 **[ツールボックス]** ウィンドウをドッキングします。

     ![[ツールボックス] ウィンドウを IDE にピン留めする [ピン設定] アイコンをクリックします。](../ide/media/vb-pin-the-toolbox-window.png)

1. **[ボタン]** コントロールをクリックし、フォームまでドラッグします。

     ![フォームにボタンを追加する](../ide/media/vb-add-a-button-to-form1.png)

1. **[プロパティ]** ウィンドウの **[外観]** セクション (または **[フォント]** セクション) で、`Click this` と入力し、**Enter** キーを押します。

     ![フォーム上のボタンにテキストを追加する](../ide/media/vb-button-control-text.png)

     ( **[プロパティ]** ウィンドウが表示されない場合は、メニュー バーから開くことができます。 そのためには、 **[表示]**  >  **[プロパティ ウィンドウ]** をクリックします。 または **F4** キーを押します)。

1. **[プロパティ]** ウィンドウの **[デザイン]** セクションで、名前を **Button1** から `btnClickThis` に変更し、**Enter** キーを押します。

     ![フォーム上のボタンに関数を追加する](../ide/media/vb-button-control-function.png)

   > [!NOTE]
   > **[プロパティ]** ウィンドウで一覧をアルファベット順にした場合、代わりに、 **(DataBindings)** セクションに **Button1** が表示されます。

### <a name="add-a-label-to-the-form"></a>フォームにラベルを追加する

アクションを作成するボタン コントロールが追加されましたので、次にテキストが送信されるラベル コントロールを追加してみましょう。

1. **[ツールボックス]** ウィンドウから **[ラベル]** コントロールを選択し、そのラベルをフォームにドラッグし、 **[Click this]** ボタンの下にドロップします。

1. **[プロパティ]** ウィンドウの **[デザイン]** セクションまたは **(DataBindings)** セクションで、**Label1** の名前を `lblHelloWorld` に変更し、**Enter** キーを押します。

### <a name="add-code-to-the-form"></a>フォームにコードを追加する

1. **[Form1.vb [Design]]** ウィンドウで、**[Click this]** ボタンをダブルクリックして、**[Form1.vb]** ウィンドウを開きます 

      (あるいは、**[ソリューション エクスプローラー]** で **[Form1.vb]** を展開し、**[Form1]** をクリックします)。

1. 次のスクリーンショットに示すように、**Form1.vb** ウィンドウで、**Private Sub** 行と **End Sub** 行の間に `lblHelloWorld.Text = "Hello World!"` と入力します。

     ![フォームにコードを追加する](../ide/media/vb-add-code-to-the-form.png)

## <a name="run-the-application"></a>アプリケーションの実行

1. **[開始]** ボタンをクリックしてアプリケーションを実行します。

     ![[開始] をクリックして、アプリをデバッグして実行する](../ide/media/vb-click-start-hello-world.png)

   いくつかの処理が行われます。 Visual Studio IDE 内では、 **[診断ツール]** ウィンドウが開き、 **[出力]** ウィンドウも開きます。 ただし、IDE の外部では、 **[Form1]** ダイアログ ボックスが表示されます。 このダイアログ ボックスには、 **[Click this]** ボタンと **Label1** というテキストが表示されます。

1. **[Form1]** ダイアログ ボックスの **[Click this]** ボタンをクリックします。 テキスト **Label1** が **Hello World!** に変更されることがわかります。

    ![テキスト Label1 を含む [Form1] ダイアログ ボックス ](../ide/media/vb-form1-dialog-hello-world.png)

1. **[Form1]** ダイアログ ボックスを閉じて、アプリの実行を停止します。

## <a name="next-steps"></a>次の手順

詳細については、引き続き以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [チュートリアル: ピクチャ ビューアーの作成](tutorial-1-create-a-picture-viewer.md)

## <a name="see-also"></a>関連項目

* [その他の Visual Basic のチュートリアル](../get-started/visual-basic/index.yml)
* [C# チュートリアル](../get-started/csharp/index.yml)
* [C++ のチュートリアル](/cpp/get-started/tutorial-console-cpp)