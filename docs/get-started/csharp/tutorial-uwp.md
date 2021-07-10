---
title: 'チュートリアル: Visual Studio と C# で UWP アプリを作成する'
description: XAML と C# を使用して Visual Studio で UWP アプリを作成する
titleSuffix: ''
ms.custom: vs-acquisition, get-started, SEO-VS-2020
ms.date: 09/20/2019
ms.technology: vs-ide-general
ms.topic: tutorial
ms.devlang: CSharp
author: j-martens
ms.author: jmartens
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 2e89c58e3c0dca2b5d009a592d3f242646339f8f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390295"
---
# <a name="tutorial-create-your-first-universal-windows-platform-application-in-visual-studio-with-xaml-and-c35"></a>チュートリアル: Visual Studio で XAML と C# を使用して最初のユニバーサル Windows プラットフォーム アプリを作成する

ここでは、Visual Studio 統合開発環境 (IDE) の概要を示し、任意の Windows 10 デバイスで実行できる "Hello World" アプリケーションを作成します。 これの実行には、ユニバーサル Windows プラットフォーム (UWP) のプロジェクト テンプレート、Extensible Application Markup Language (XAML) および C# のプログラミング言語を使用します。

::: moniker range="vs-2017"
Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。
::: moniker-end
::: moniker range="vs-2019"
Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。
::: moniker-end

## <a name="create-a-project"></a>プロジェクトを作成する

まず、ユニバーサル Windows プラットフォーム プロジェクトを作成します。 この種類のプロジェクトには、必要となるすべてのテンプレート ファイルが付属していますので、何も追加する必要はありません。

::: moniker range="vs-2017"
1. Visual Studio を開きます。

1. 上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

1. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで **[Visual C#]** を展開し、 **[Windows ユニバーサル]** を選択します。 中央のペインで **[空のアプリ (ユニバーサル Windows)]** を選択します。 次いで、プロジェクトに「*HelloWorld*」という名前を付け、 **[OK]** を選択します。

   > [!NOTE]
   > ソース プロジェクトの場所が **New Technology File System (NTFS)** でフォーマットされたドライブ (オペレーティング システム (OS) ドライブなど) にあることを確認します。 そうしないと、プロジェクトのビルドと実行で問題が発生する可能性があります。 

   ![Visual Studio IDE の [新しいプロジェクト] ダイアログ ボックスに示されている Windows ユニバーサル プロジェクト テンプレート](media/new-project-csharp-uwp-helloworld.png)

   > [!NOTE]
   > **[空のアプリ (ユニバーサル Windows)]** プロジェクト テンプレートが表示されない場合は、 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで **[Visual Studio インストーラーを開く]** リンクをクリックします。<br><br>![[新しいプロジェクト] ダイアログ ボックスで [Visual Studio インストーラーを開く] リンクをクリックする](../../ide/media/vb-open-visual-studio-installer-hello-world.png)<br><br>Visual Studio インストーラーが起動します。 **[ユニバーサル Windows プラットフォーム開発]** ワークロードを選択し、 **[変更]** を選択します。<br><br>![Visual Studio インストーラーの [ユニバーサル Windows プラットフォーム開発] ワークロード](media/uwp-dev-workload.png)

1. **[新しいユニバーサル Windows プラットフォーム プロジェクト]** ダイアログ ボックスで、 **[ターゲット バージョン]** と **[最小バージョン]** の既定の設定をそのまま使用します。

   ![[新しいユニバーサル Windows プラットフォーム プロジェクト] の既定のターゲット バージョンと最小バージョンの設定をそのまま使用します。](media/new-uwp-project-target-minver-dialog.png)
::: moniker-end

::: moniker range=">=vs-2019"
1. Visual Studio を開き、[スタート] ウィンドウで **[新しいプロジェクトの作成]** を選択します。

1. **[新しいプロジェクトの作成]** 画面で、検索ボックスに「*ユニバーサル Windows*」と入力し、 **[空のアプリ (ユニバーサル Windows)]** 用の C# テンプレートを選択して、 **[次へ]** を選択します。

   ![[新しいプロジェクトの作成] 画面のスクリーンショット](media/vs-2019/uwp-create-new-project.png)

   > [!NOTE]
   > **[空のアプリ (ユニバーサル Windows)]** プロジェクト テンプレートが表示されない場合は、 **[さらにツールと機能をインストールする]** リンクをクリックします。<br><br>![[さらにツールと機能をインストールする] リンクをクリックする](media/vs-2019/uwp-not-finding.png)<br><br>Visual Studio インストーラーが起動します。 **[ユニバーサル Windows プラットフォーム開発]** ワークロードを選択し、 **[変更]** を選択します。<br><br>![Visual Studio インストーラーの [ユニバーサル Windows プラットフォーム開発] ワークロード](media/uwp-dev-workload.png)

1. プロジェクトに「_HelloWorld_」という名前を付け、 **[作成]** を選択します。

   ![プロジェクト画面を構成する](media/vs-2019/uwp-configure-your-project.png)

1. **[新しいユニバーサル Windows プラットフォーム プロジェクト]** ダイアログ ボックスで、 **[ターゲット バージョン]** と **[最小バージョン]** の既定の設定をそのまま使用します。

   ![[新しいユニバーサル Windows プラットフォーム プロジェクト] ダイアログ ボックスで、[ターゲット バージョン] と [最小バージョン] の既定の設定をそのまま使用します](media/vs-2019/new-uwp-project-target-minver-dialog.png)
::: moniker-end

   > [!NOTE]
   > UWP アプリを作成するために Visual Studio を初めて使用する場合、 **[設定]** ダイアログ ボックスが表示されます。 **[開発者モード]** 、 **[はい]** の順に選択します。<br><br>
   > ![UWP 設定ダイアログ ボックスで開発者モードを有効にする](media/enable-developer-mode.png)<br><br>Visual Studio では、開発者モード パッケージが追加でインストールされます。 パッケージのインストールが完了したら、 **[設定]** ダイアログ ボックスを閉じます。

## <a name="create-the-application"></a>アプリケーションを作成する

開発を始めるときがきました。 これから、ボタン コントロールを追加し、ボタンにアクションを追加し、"Hello World" アプリを起動してどのように動作するか確認します。

### <a name="add-a-button-to-the-design-canvas"></a>デザイン キャンバスにボタンを追加する

1. **ソリューション エクスプローラー** で、*MainPage.xaml* をダブルクリックして分割ビューを開きます。

   ::: moniker range="vs-2017"
   ![ソリューション エクスプローラーで MainPage.xaml を開く ](media/uwp-solution-explorer-MainPage-xaml.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![ソリューション エクスプローラーで MainPage.xaml を開く](media/vs-2019/uwp-solution-explorer-mainpage-xaml.png)
   ::: moniker-end

   デザイン キャンバスを含む **XAML デザイナー** と、コードを追加または変更できる **XAML エディター** の 2 つのウィンドウがあります。

   ![XAML エディターの XAML デザイナー ウィンドウ](media/uwp-xaml-editor.png)

1. **[ツールボックス]** を選択して、ツールボックスのスライド アウト ウィンドウを開きます。

   ![[ツールボックス] をクリックしてツールボックスのスライド アウト ウィンドウを開く](media/uwp-toolbox.png)

   (**ツールボックス** のオプションが表示されない場合は、メニュー バーから開くことができます。 これを行うには、 **[ビュー]**  >  **[ツールバー]** の順に選択します。 または、**Ctrl**+**Alt**+**X** キーを押します)。

1. **[ピン設定]** アイコンをクリックして、[ツールボックス] ウィンドウをドッキングします。

   ![[ピン設定] アイコンをクリックして [ツールボックス] ウィンドウをドッキングする](media/uwp-toolbox-autohide.png)

1. **[ボタン]** コントロールをクリックし、デザイン キャンバスまでドラッグします。

   ![[ボタン] コントロールをクリックしデザイン キャンバスまでドラッグする](media/uwp-toolbox-add-button-control.png)

   **XAML エディター** でコードを参照すると、そこにもボタンが追加されていることを確認できます。

   ![XAML エディターでボタンを表示する](media/uwp-xaml-control-code-window.png)

### <a name="add-a-label-to-the-button"></a>ボタンにラベルを追加する

1. **XAML エディター** で、ボタンのコンテンツ値を "Button" から "Hello World!" に変更します。

   ![ボタンのコンテンツ値を Hello World に変更する](media/uwp-change-button-text-in-xaml-code-window.png)

1. **XAML デザイナー** のボタンも変更されることに注目してください。

   ![デザイン キャンバスでボタンが Hello World に変更する](media/uwp-button-text-change-in-design-canvas.png)

### <a name="add-an-event-handler"></a>イベント ハンドラーを追加する

「イベント ハンドラー」とは、難しそうに聞こえますが、イベントが発生したときに呼び出されるコードの単なる別名です。 この場合、"Hello World!" ボタンにアクション を追加します。

1. デザイン キャンパスでボタン コントロールをダブルクリックします。

1. 分離コード ページの *MainPage.xaml.cs* でイベント ハンドラー コードを編集します。

   ポイントはここからです。 既定のイベント ハンドラーは次のようになります。

   ![既定の Button_Click イベント ハンドラー ](media/uwp-button-click-code.png)

   これを次のように変更してみます。

   ![新しい非同期の Button_Click イベント ハンドラー ](media/uwp-add-hello-world-async-code.png)

   コピーして貼り付けるコードは次のとおりです。

   ```C#
   private async void Button_Click(object sender, RoutedEventArgs e)
         {
             MediaElement mediaElement = new MediaElement();
             var synth = new Windows.Media.SpeechSynthesis.SpeechSynthesizer();
             Windows.Media.SpeechSynthesis.SpeechSynthesisStream stream = await synth.SynthesizeTextToStreamAsync("Hello, World!");
             mediaElement.SetSource(stream, stream.ContentType);
             mediaElement.Play();
         }
   ```

#### <a name="what-did-we-just-do"></a>行った処理

コードでいくつかの Windows API が使用され、いくつかのテキストを読み上げられる、音声合成オブジェクトが作成されました。 (`SpeechSynthesis` の使用に関する詳細は、「<xref:System.Speech.Synthesis>」をご覧ください)。

## <a name="run-the-application"></a>アプリケーションの実行

::: moniker range="vs-2017"
"Hello World" UWP アプリを、ビルド、配置、および起動して、どのように表示および読み上げがあるか確認してみましょう。 ここではその方法を説明します。

1. 再生ボタン (表示は **[ローカル コンピューター]** ) を使用して、ローカル コンピューターでアプリケーションを起動します。

   ![[ローカル マシン] をクリックし、UWP アプリを起動してデバッグする](media/uwp-start-or-debug.png)

   (または、メニュー バーから **[デバッグ]** > **[デバッグの開始]** を選択するか、F5 キーを押してアプリを開始します)。

1. スプラッシュ スクリーンが消えるとすぐ表示されるアプリを確認します。 アプリは次のように表示されるはずです。

   ![UWP "Hello World" アプリ](media/uwp-hello-world-app.png)

1. **[Hello World]** ボタンをクリックします。

   Windows 10 デバイスにより、"Hello, World!" と文字通り読み上げられます。

1. アプリを閉じるには、ツール バーで **[デバッグの停止]** ボタンをクリックします。 (または、メニュー バーから **[デバッグ]**  >  **[デバッグの停止]** を選択するか、Shift + F5 キーを押します。)

::: moniker-end
::: moniker range=">=vs-2019"
"Hello World" UWP アプリを、ビルド、配置、および起動して、どのように表示および読み上げがあるか確認してみましょう。 ここではその方法を説明します。

1. 再生ボタン (表示は **[ローカル コンピューター]** ) を使用して、ローカル コンピューターでアプリケーションを起動します。

   ![[ローカル マシン] をクリックし、UWP アプリを起動してデバッグする](media/uwp-start-or-debug.png)

   (または、メニュー バーから **[デバッグ]** > **[デバッグの開始]** を選択するか、F5 キーを押してアプリを開始します)。

1. スプラッシュ スクリーンが消えるとすぐ表示されるアプリを確認します。 アプリは次のように表示されるはずです。

   ![UWP "Hello World" アプリ](media/vs-2019/uwp-hello-world-app.png)

1. **[Hello World]** ボタンをクリックします。

   Windows 10 デバイスにより、"Hello, World!" と文字通り読み上げられます。

1. アプリを閉じるには、ツール バーで **[デバッグの停止]** ボタンをクリックします。 (または、メニュー バーから **[デバッグ]**  >  **[デバッグの停止]** を選択するか、Shift + F5 キーを押します。)

::: moniker-end

## <a name="next-steps"></a>次の手順

これでこのチュートリアルは完了です。 これで UWP および Visual Studio IDE の基本を学習できたはずです。 詳細については、引き続き以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [ユーザー インターフェイスを作成する](/windows/uwp/design/basics/xaml-basics-ui)

## <a name="see-also"></a>関連項目

- [UWP の概要](/windows/uwp/get-started/universal-application-platform-guide)
- [UWP アプリのサンプルを入手する](/windows/uwp/get-started/get-uwp-app-samples)
