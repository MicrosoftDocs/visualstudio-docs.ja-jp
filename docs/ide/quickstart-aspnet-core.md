---
title: C# に ASP.NET Core Web アプリを作成する
description: Visual Studio で C# および ASP.NET Core を使用して Hello World の Web アプリを作成する方法について、段階的に説明します。
ms.date: 02/01/2019
ms.custom: mvc,seodec18
ms.topic: quickstart
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 60f7c7bd7d0a3073f75d4ece7012601ded8eb059
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55957787"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-aspnet-core-web-app"></a>クイック スタート: Visual Studio を使用して初めての ASP.NET Core Web アプリを作成する

Visual Studio の使用方法を紹介する、この 5 - 10 分のクイック スタートでは、ASP.NET プロジェクト テンプレートと C# プログラミング言語を使って、シンプルな "Hello World" Web アプリを作成します。

## <a name="before-you-begin"></a>始める前に

### <a name="install-visual-studio"></a>Visual Studio のインストール

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) ページに移動し、無料試用版をインストールしてください。

### <a name="choose-your-theme-optional"></a>テーマを選択する (省略可能)

このクイック スタート チュートリアルには、ダーク テーマを使用しているスクリーン ショットが含まれます。 ダーク テーマを使用していないが、使用したい場合は、その方法について「[Visual Studio IDE とエディターのカスタマイズ](quickstart-personalize-the-ide.md)」ページを参照してください。

## <a name="create-a-project"></a>プロジェクトを作成する

最初に、ASP.NET Core Web アプリケーション プロジェクトを作成します。 このプロジェクト タイプには、Web アプリを作成するためのすべてのテンプレート ファイルが付属しているので、何も追加する必要はありません。

1. Visual Studio 2017 を開きます。

1. 上部のメニュー バーで、**[ファイル]** > **[新規作成]** > **[プロジェクト]** の順に選択します。

1. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで **[Visual C#]** を展開し、**[.NET Core]** を選択します。 中央のウィンドウで、**[ASP.NET Core Web アプリケーション]** を選択ます。 <br/><br/>次に、ファイル名を「`HelloWorld`」にして、**[OK]** を選択します。

   ![C# 用の新しい ASP.NET Core Web アプリケーション プロジェクトを作成する](../ide/media/csharp-aspnet-choose-template-name-file.png)

   > [!NOTE]
   > **.NET Core** プロジェクト テンプレートのカテゴリが表示されない場合は、左側のウィンドウで **[Visual Studio インストーラーを開く]** リンクを選択します。 (ディスプレイの設定によっては、表示するためにスクロールする必要があります。)
   >
   > ![[新しいプロジェクト] ダイアログ ボックスから Visual Studio インストーラーを開く](../ide/media/open-visual-studio-installer.png)
   >
   > Visual Studio インストーラーが起動します。 **[ASP.NET と Web 開発]** ワークロードを選択してから **[変更]** を選択します。
   >
   > ![VS インストーラーの ASP.NET ワークロード](../ide/media/quickstart-aspnet-workload.png)
   >
   > (新しいワークロードのインストールを続ける前に、Visual Studio を終了することが必要な場合があります。)

1. **[新しい ASP.NET Core Web アプリケーション]** ダイアログ ボックスで、上部のドロップダウン メニューから **[ASP.NET Core 2.1]** を選択します。 次に、**[Web アプリケーション]** を選択し、**[OK]** を選択します。

   ![[新しい ASP.NET Core Web アプリケーション] ダイアログ ボックス](../ide/media/aspnet-core-2dot1.png)

   > [!NOTE]
   > **[ASP.NET Core 2.1]** 以降が表示されない場合は、最新リリースの Visual Studio を実行していることを確認します。 インストールを更新する方法の詳細については、「[Visual Studio 2017 を最新リリースに更新する](../install/update-visual-studio.md)」ページを参照してください。

すぐに、Visual Studio でプロジェクト ファイルが開きます。

## <a name="create-and-run-the-app"></a>アプリの作成と実行

1. **ソリューション エクスプローラー**で、**Pages** フォルダーを展開し、**About.cshtml** を選択します。

   ![ソリューション エクスプローラーから About.cshtml ファイルを選択する](../ide/media/csharp-aspnet-about-page-html-file.png)

   このファイルは、Web アプリの **About** という名前のページに対応します。これは Web ブラウザーで実行されます。

   ![Web アプリの About ページ](../ide/media/csharp-aspnet-about-page.png)

   エディターに、**About** ページの "additional information" 領域の HTML コードが表示されます。

   ![Visual Studio エディターに表示された "additional information" 領域の HTML コード](../ide/media/csharp-aspnet-about-cshtml-page.png)

1. "additional information" というテキストを「**Hello World!**」に変更します。

   ![Visual Studio エディターに表示される既定の "additional information" 領域の HTML コードを変更する](../ide/media/csharp-aspnet-about-cshtml-page-hello-world.png)

1. **ソリューション エクスプローラー**で、**About.cshtml** を展開し、**About.cshtml.cs** を選択します。 (このファイルも、Web ブラウザーの **About** ページに対応しています。)

   ![ソリューション エクスプローラーから About.cshtml ファイルを選択する](../ide/media/csharp-aspnet-about-page-code-file.png)

   エディターに、**About** ページの "application description" 領域のテキストを含む C# コードが表示されます。

   ![Visual Studio エディターに表示されたアプリケーション説明領域の C# コード](../ide/media/csharp-aspnet-about-cshtml-cs-code.png)

1. "application description" というメッセージ テキストを「**What's my message?**」に変更します。

   ![Visual Studio エディターでアプリケーション説明領域の既定のメッセージ テキストを変更する](../ide/media/csharp-aspnet-about-cshtml-cs-message.png)

1. **IIS Express** を選択するか、**Ctrl**+**F5** キーを押してアプリを実行し、Web ブラウザーで開きます。

   ![Visual Studio の [IIS Express] ボタンを選択する](../ide/media/csharp-aspnet-helloworld-iisbutton.png)

   > [!NOTE]
   > **"Web サーバー 'IIS Express' に接続できませんでした"** というエラー メッセージ、または SSL 証明書に関するエラー メッセージが表示された場合は、Visual Studio を閉じます。 次に、右クリック コンテキスト メニューから **[管理者として実行]** オプションを使用して Visual Studio を開きます。 その後、アプリケーションをもう一度実行します。

1. Web ブラウザーで、**About** ページに更新されたテキストが含まれていることを確認します。

   ![加えた変更が含まれる更新後の About ページを表示する](../ide/media/csharp-aspnet-about-page-hello-world.png)

1. Web ブラウザーを閉じます。

### <a name="review-your-work"></a>作業内容の確認

次のアニメーションを見て、前のセクションで完了した作業を確認します。

  ![Visual Studio で単純な C# ASP.NET Core Web アプリを作成して実行する方法を示すアニメーション .gif ファイルを表示](../ide/media/csharp-aspnet-animated-hello-world.gif)

このクイック スタートは完了しました。 C#、ASP.NET Core、Visual Studio IDE (統合開発環境) について少しはご理解いただけたかと思います。

## <a name="next-steps"></a>次の手順

詳細については、引き続き以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [Visual Studio での C# および ASP.NET の概要](../get-started/csharp/tutorial-aspnet-core.md)

## <a name="see-also"></a>関連項目

[Visual Studio を使用して Azure App Service に Web アプリを発行する](../deployment/quickstart-deploy-to-azure.md)
