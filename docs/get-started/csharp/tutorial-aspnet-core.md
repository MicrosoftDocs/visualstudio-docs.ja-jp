---
title: 'チュートリアル: C# と ASP.NET Core の概要'
titleSuffix: ''
description: Visual Studio を使用して C# で ASP.NET Core Web アプリを作成する方法について段階的に説明します。
ms.custom: vs-acquisition, get-started
ms.date: 06/12/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: j-martens
ms.author: jmartens
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 25840b820a92925c3d7434d0c76b0138b533b2dc
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388114"
---
# <a name="tutorial-get-started-with-c-and-aspnet-core-in-visual-studio"></a>チュートリアル: Visual Studio での C# および ASP.NET Core の概要

Visual Studio を使用した ASP.NET Core での C# 開発に関するこのチュートリアルでは、C# ASP.NET Core Web アプリを作成し、それを変更し、IDE の一部の機能を検討した後で、アプリを実行します。

## <a name="prerequisites"></a>前提条件

1. Visual Studio のインストール
   ::: moniker range="vs-2017"
   
   Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。
   
   ::: moniker-end
   
   ::: moniker range="vs-2019"
   
   Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。
   
   ::: moniker-end

   ::: moniker range="vs-2022"

   Visual Studio 2022 プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

   ::: moniker-end

1. Visual Studio の更新 - Visual Studio を既にインストールしている場合は、最新のリリースを実行していることを確認します。 インストールを更新する方法の詳細については、「[Visual Studio を最新リリースに更新する](../../install/update-visual-studio.md)」ページを参照してください。

1. テーマを選択する (省略可能) - このチュートリアルには、ダーク テーマを使用しているスクリーンショットが含まれます。 方法については、「[Visual Studio IDE とエディターのカスタマイズ](../../ide/quickstart-personalize-the-ide.md)」ページをご覧ください。

## <a name="create-a-project"></a>プロジェクトを作成する

まず、ASP.NET Core プロジェクトを作成します。 このプロジェクトの種類には、完全な機能を備えた Web サイトのために必要となるすべてのテンプレート ファイルが付属していますので、何も追加する必要はありません。

::: moniker range="vs-2017"

1. Visual Studio 2017 を開きます。

2. 上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual C#]** 、 **[Web]** の順に展開し、 **[.NET Core]** を選択します。 中央のウィンドウで、 **[ASP.NET Core Web アプリケーション]** を選択ます。 次に、ファイルに *MyCoreApp* という名前を付け、 **[OK]** を選択します。

   ![Visual Studio IDE の [新しいプロジェクト] ダイアログ ボックスに示されている ASP.NET Core Web アプリケーション プロジェクト テンプレート](media/csharp-aspnet-choose-template-name-razor-mycoreapp-file.png)

### <a name="add-a-workload-optional"></a>ワークロードを追加する (省略可能)

**ASP.NET Core Web アプリケーション** プロジェクト テンプレートが表示されない場合は、**ASP.NET と Web 開発** ワークロードを追加して取得できます。 コンピューターにインストールされている Visual Studio 2017 の更新プログラムに応じて、次の 2 つの方法のうちのいずれかでこのワークロードを追加することができます。

#### <a name="option-1-use-the-new-project-dialog-box"></a>オプション 1:[新しいプロジェクト] ダイアログ ボックスを使用する

1. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual Studio インストーラーを開く]** リンクを選択します。 (ディスプレイの設定によっては、表示するためにスクロールする必要があります。)

   ![[新しいプロジェクト] ダイアログ ボックスで [Visual Studio インストーラーを開く] リンクを選択する](../media/open-visual-studio-installer-mycoreapp.png)

1. Visual Studio インストーラーが起動します。 **[ASP.NET と Web 開発]** ワークロードを選択してから **[変更]** を選択します。

   ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../media/tutorial-aspnet-workload.png)

   (新しいワークロードのインストールを続ける前に、Visual Studio を終了することが必要な場合があります。)

#### <a name="option-2-use-the-tools-menu-bar"></a>オプション 2:[ツール] メニュー バーを使用する

1. **[新しいプロジェクト]** ダイアログ ボックスを取り消します。 次に、上部のメニュー バーで、 **[ツール]**  >  **[ツールと機能を取得]** の順に選択します。

1. Visual Studio インストーラーが起動します。 **[ASP.NET と Web 開発]** ワークロードを選択してから **[変更]** を選択します。

   (新しいワークロードのインストールを続ける前に、Visual Studio を終了することが必要な場合があります。)

### <a name="add-a-project-template"></a>プロジェクト テンプレートを追加する

1. **[新しい ASP.NET Core Web アプリケーション]** ダイアログ ボックスで、 **[Web アプリケーション]** プロジェクト テンプレートを選択します。

1. 上部のドロップダウン メニューに **[ASP.NET Core 2.1]** が表示されていることを確認します。 次に、 **[OK]** を選択します。

   ![[新しい ASP.NET Core Web アプリケーション] ダイアログ ボックス](media/new-project-csharp-aspnet-razor-web-app.png)

   > [!NOTE]
   > 上部のドロップダウン メニューで **[ASP.NET Core 2.1]** が表示されない場合は、最新リリースの Visual Studio を実行していることを確認します。 インストールを更新する方法の詳細については、「[Visual Studio を最新リリースに更新する](../../install/update-visual-studio.md)」ページを参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   :::image type="content" source="../../get-started/media/vs-2019/create-new-project-dark-theme.png" alt-text="[新しいプロジェクトの作成] ウィンドウを表示する":::

1. **[新しいプロジェクトの作成]** ウィンドウで、言語の一覧から **[C#]** を選択します。 次に、プラットフォームの一覧から **[Windows]** を選択し、プロジェクトの種類の一覧から **[Web]** を選択します。

      言語、プラットフォーム、およびプロジェクトの種類のフィルターを適用してから、 **[ASP.NET Core Web アプリ]** テンプレートを選択して、 **[次へ]** を選択します。

   :::image type="content" source="./media/vs-2019/csharp-create-new-project-aspnet-core.png" alt-text="ASP.NET Core Web アプリ用の C# テンプレートを選択する":::

   > [!NOTE]
   > **[ASP.NET Core Web アプリ]** テンプレートが表示されない場合は、 **[新しいプロジェクトの作成]** ウィンドウからそれをインストールすることができます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。
   >
   > ![[新しいプロジェクトの作成] ウィンドウに表示された [お探しの情報が見つかりませんでしたか?] での [さらにツールと機能をインストールする] リンク](../../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 次に、Visual Studio インストーラーで、 **[ASP.NET と Web 開発]** ワークロードを選択します。
   >
   > ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../../get-started/media/aspnet-core-web-dev-workload.png)
   >
   > その後、Visual Studio インストーラー内の **[変更]** ボタンをクリックします。 作業内容を保存するよう求められたら、そのようにします。 次に、 **[続行]** を選択してワークロードをインストールします。 その後、この「[プロジェクトを作成する](#create-a-project)」プロシージャの手順 2 に戻ります。

1. **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*MyCoreApp*」とタイプまたは入力します。 その後、 **[次へ]** を選択します。

   :::image type="content" source="./media/vs-2019/csharp-name-your-aspnet-app.png" alt-text="[新しいプロジェクトの構成] ウィンドウで、ご自分のプロジェクトに 'MyCoreApp' という名前を付けます。":::

1. **[追加情報]** ウィンドウで、上部のドロップダウン メニューに **[.NET Core 3.1]** が表示されていることを確認します。 チェック ボックスをオンにすると、Docker サポートを有効にすることができます。 [認証の変更] ボタンをクリックして、認証サポートを追加することもできます。 ここでは、以下のオプションから選択できます。
    - [なし]: 認証は行われません。
    - [個別のアカウント]: ローカルまたは Azure ベースのデータベースに保管されます。
    - [Microsoft ID プラットフォーム]: このオプションでは、認証用に Active Directory、Azure AD、または Microsoft 365 が使用されます。
    - [Windows]: イントラネット アプリケーションに適しています。
    
    **[Enable Docker]\(Docker を有効にする\)** チェック ボックスはオフのままにし、[認証の種類] に **[なし]** を選択します。 そのうえで **[Create]\(作成\)** を選択します。

   :::image type="content" source="./media/vs-2019/aspnet-core-additional-information.png" alt-text="[追加情報] ウィンドウで、[.NET Core 3.1] が選択されていることを確認し、すべて既定値のままにします":::

   Visual Studio で新しいプロジェクトが開かれます。

::: moniker-end

### <a name="about-your-solution"></a>ソリューションについて

このソリューションは **Razor ページ** デザイン パターンに従っています。 これは [Model-View-Controller (MVC)](/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-2.1&tabs=aspnetcore2x&preserve-view=true) デザイン パターンとは異なり、モデルとコント ローラーのコードが Razor ページ自体の中に含まれるよう効率化されています。

::: moniker range="vs-2017"
## <a name="tour-your-solution"></a>ソリューションのツアーを体験する

 1. プロジェクト テンプレートでは、_MyCoreApp_ という名前の単一の ASP.NET Core プロジェクトを使用してソリューションを作成します。 **ソリューション エクスプローラー** タブを選択してそのコンテンツを表示させます。

    ![MyCoreApp という名前の Visual Studio の Razor Pages ソリューション用 ASP.NET ソリューション エクスプローラー](media/csharp-aspnet-razor-solution-explorer-mycoreapp.png)

 1. **Page** フォルダーを展開した後、 *[About.cshtml]* を展開します。

     ![Visual Studio のソリューション エクスプローラーの About.cshtml ファイル](media/csharp-aspnet-razor-solution-explorer-aboutcshtml.png)

 1. コード エディターで **About.cshtml** ファイルを表示します。

     ![Visual Studio コード エディターの About.cshtml ファイルの最初の 10 行を示すスクリーンショット。](media/csharp-aspnet-razor-aboutcshtml-mycoreapp-code.png)

 1. **About.cshtml.cs** ファイルを選択します。

     ![Visual Studio コード エディターで About.cshtml.cs ファイルを選択する](media/csharp-aspnet-razor-solution-explorer-aboutcshtmlcs.png)

 1. コード エディターで **About.cshtml.cs** ファイルを表示します。

     ![Visual Studio コード エディターの About.cshtml.cs ファイルの最初の 18 行を示すスクリーンショット。 ](media/csharp-aspnet-razor-aboutcshtmlcs-mycoreapp-code.png)

 1. プロジェクトには、Web サイトのルートとなる **wwwroot** フォルダーが含まれます。 その内容を表示するには、フォルダーを展開します。

     ![Visual Studio のソリューション エクスプローラーの wwwroot フォルダー](media/csharp-aspnet-razor-solution-explorer-wwwroot.png)

    &mdash;CSS、イメージ、JavaScript ライブラリなど&mdash;の静的サイト コンテンツを、任意のパスに直接配置することができます。

 1. プロジェクトには、実行時に Web アプリを管理する構成ファイルも含まれます。 既定のアプリケーション [構成](/aspnet/core/fundamentals/configuration)は *appsettings.json* に格納されます。 しかし、*appsettings.Development.json* を使用して、これらの設定をオーバーライドすることができます。 **appsettings.Development.json** ファイルを表示するには、**appsettings.json** ファイルを展開します。

     ![Visual Studio のソリューション エクスプローラーの構成ファイル](media/csharp-aspnet-razor-solution-explorer-appsettingsjson.png)

## <a name="run-debug-and-make-changes"></a>実行、デバッグ、および変更

1. IDE の **[IIS Express]** ボタンを選択して、デバッグ モードでアプリをビルドして実行します (または、**F5** キーを押すか、メニュー バーから **[デバッグ]**  >  **[デバッグの開始]** の順に選択します)。

     ![Visual Studio の [IIS Express] ボタンを選択する](media/csharp-aspnet-razor-iisexpress.png)

     > [!NOTE]
     > "**Web サーバー 'IIS Express' に接続できませんでした**" というエラー メッセージが表示された場合は、Visual Studio を閉じて、右クリックまたはコンテキスト メニューから **[管理者として実行]** オプションを使用して Visual Studio を開きます。 その後、アプリケーションをもう一度実行します。
     >
     > IIS SSL Express の証明書を受け入れるかどうかをたずねるメッセージが表示される場合もあります。 Web ブラウザーでコードを表示するには、 **[はい]** を選択し、フォロー アップ セキュリティ警告メッセージを受信する場合はさらに **[はい]** を選択します。

1. Visual Studio でブラウザー ウィンドウが起動します。 そうすると、メニュー バーに **Home**、**About**、**Contact** ページが表示されます。 (表示されない場合は、"ハンバーガー" メニュー項目を選択して表示させます。)

    ![Web アプリのメニュー バーから "ハンバーガー" メニュー項目を選択する](media/csharp-aspnet-razor-browser-page.png)

1. メニュー バーから **[About]** を選択します。

   ![アプリのブラウザー ウィンドウのメニュー バーで [About] を選択する](media/csharp-aspnet-razor-browser-page-about-menu.png)

   特に、ブラウザーで見た **About** ページには、*About.cshtml* ファイルに設定されているテキストが表示されます。

   ![[バージョン情報] ページでテキストを表示する](media/csharp-aspnet-razor-browser-page-about.png)

1. Visual Studio に戻り、**Shift + F5** を押してデバッグ モードを停止します。 これにより、ブラウザー ウィンドウ内のプロジェクトも閉じられます。

1. Visual Studio で **About.cshtml** を選択します。 次に、「_additional_」という単語を削除して、その代わりに「_file and directory_」という文字列を追加します。

    ![About.cshtml ファイル内のテキストを変更する](media/csharp-aspnet-razor-aboutcshtml-mycoreapp-code-changed.png)

1. **About.cshtml.cs** を選択します。 次に、次のショートカットを使用して、ファイルの上部にある `using` ディレクティブをクリーンアップします。

   灰色表示の `using` ディレクティブのいずれかを選択すると、キャレットのすぐ下、または左余白に[クイック アクション](../../ide/quick-actions.md) (電球) が表示されます。 電球を選択してから、 **[不要な using の削除]** を選択します。

   ![About.cshtml.cs の不要な using を削除する](media/csharp-aspnet-razor-remove-unnecessary-usings.png)

     Visual Studio では、ファイルから不要な `using` ディレクティブが削除されます。

1. 次に、`OnGet()` メソッドの本体を次のコードに変更します。

     ```csharp
     public void OnGet()
     {
         string directory = Environment.CurrentDirectory;
         Message = String.Format("Your directory is {0}.", directory);
     }
    ```

1. **Environment** と **String** の下に波形の下線が 2 本表示されることに注意してください。 波形の下線が表示されるのは、これらの種類がスコープに含まれないためです。

   ![OnGet メソッドで波形の下線でマークされたエラー](media/csharp-aspnet-razor-add-new-on-get-method.png)

    **[エラー一覧]** ツール バーを開くと、そこに同じエラーが一覧表示されます ( **[エラー一覧]** ツール バーが表示されない場合は、上部のメニュー バーで **[表示]**  >  **[エラー一覧]** の順に選択します)。

   ![Visual Studio の [エラー一覧]](media/csharp-aspnet-razor-error-list.png)

1. これを修正しましょう。 コードエディターで、エラーを含むいずれかの行にカーソルを置いた後、左余白のクイック アクション (電球) を選択します。 次に、ドロップダウン メニューから、 **[using System;]** を選択してファイルの先頭にこのディレクティブを追加し、エラーを解決します。

   !["using System;" ディレクティブを追加する](media/csharp-aspnet-razor-add-usings.png)

1. **Ctrl**+**S** を押して変更を保存し、**F5** を押して Web ブラウザーでプロジェクトを開きます。

1. Web サイトの上部で **[About]** を選択し、変更を確認します。

   ![加えた変更が含まれる更新後の About ページを表示する](media/csharp-aspnet-razor-browser-page-about-changed.png)

1. Web ブラウザーを閉じ、**Shift**+**F5** キーを押してデバッグ モードを停止したら、Visual Studio を閉じます。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="tour-your-solution"></a>ソリューションのツアーを体験する

 1. プロジェクト テンプレートでは、_MyCoreApp_ という名前の単一の ASP.NET Core プロジェクトを使用してソリューションを作成します。 **ソリューション エクスプローラー** タブを選択してそのコンテンツを表示させます。

    ![MyCoreApp という名前の Visual Studio の Razor Pages ソリューション用 ASP.NET ソリューション エクスプローラー](media/csharp-aspnet-razor-solution-explorer-mycoreapp.png)

 1. **[Pages]** フォルダーを展開します。

     ![ソリューション エクスプローラーの Pages フォルダー](media/vs-2019/csharp-aspnet-solution-explorer-pages.png)

 1. コード エディターで **Index.cshtml** ファイルを表示します。

     ![Visual Studio コード エディターで Index.cshtml ファイルを表示する](media/vs-2019/csharp-aspnet-index-cshtml.png)

 1. 各 .cshtml ファイルには、関連付けられたコード ファイルがあります。 エディターでコード ファイルを開くには、ソリューション エクスプローラーで **Index.cshtml** ノードを展開して、**Index.cshtml.cs** ファイルを選択します。

     ![Visual Studio コード エディターで Index.cshtml.cs ファイルを選択する](media/vs-2019/csharp-aspnet-choose-index-cshtml.png)

 1. コード エディターで **Index.cshtml.cs** ファイルを表示します。

     ![Visual Studio コード エディターで About.cshtml ファイルを表示する](media/vs-2019/csharp-aspnet-index-cshtml-editing.png)

 1. プロジェクトには、Web サイトのルートとなる **wwwroot** フォルダーが含まれます。 その内容を表示するには、フォルダーを展開します。

     ![Visual Studio のソリューション エクスプローラーの wwwroot フォルダー](media/csharp-aspnet-razor-solution-explorer-wwwroot.png)

    &mdash;CSS、イメージ、JavaScript ライブラリなど&mdash;の静的サイト コンテンツを、任意のパスに直接配置することができます。

 1. プロジェクトには、実行時に Web アプリを管理する構成ファイルも含まれます。 既定のアプリケーション [構成](/aspnet/core/fundamentals/configuration)は *appsettings.json* に格納されます。 しかし、*appsettings.Development.json* を使用して、これらの設定をオーバーライドすることができます。 **appsettings.Development.json** ファイルを表示するには、**appsettings.json** ファイルを展開します。

     ![Visual Studio のソリューション エクスプローラーの構成ファイル](media/csharp-aspnet-razor-solution-explorer-appsettingsjson.png)

## <a name="run-debug-and-make-changes"></a>実行、デバッグ、および変更

1. IDE の **[IIS Express]** ボタンを選択して、デバッグ モードでアプリをビルドして実行します (または、**F5** キーを押すか、メニュー バーから **[デバッグ]**  >  **[デバッグの開始]** の順に選択します)。

     ![Visual Studio の [IIS Express] ボタンを選択する](media/csharp-aspnet-razor-iisexpress.png)

     > [!NOTE]
     > "**Web サーバー 'IIS Express' に接続できませんでした**" というエラー メッセージが表示された場合は、Visual Studio を閉じて、右クリックまたはコンテキスト メニューから **[管理者として実行]** オプションを使用して Visual Studio を開きます。 その後、アプリケーションをもう一度実行します。
     >
     > IIS SSL Express の証明書を受け入れるかどうかをたずねるメッセージが表示される場合もあります。 Web ブラウザーでコードを表示するには、 **[はい]** を選択し、フォロー アップ セキュリティ警告メッセージを受信する場合はさらに **[はい]** を選択します。

1. Visual Studio でブラウザー ウィンドウが起動します。 その後、メニュー バーに **Home** ページと **Privacy** ページが表示されます。

1. メニュー バーから **[Privacy]** を選択します。

   ブラウザーで見た **Privacy** ページには、*Privacy.cshtml* ファイルに設定されているテキストが表示されます。

   ![Privacy ページでテキストを表示する](media/vs-2019/csharp-aspnet-browser-page-privacy.png)

1. Visual Studio に戻り、**Shift + F5** を押してデバッグ モードを停止します。 これにより、ブラウザー ウィンドウ内のプロジェクトも閉じられます。

1. Visual Studio で **Privacy.cshtml** を開いて編集します。 次に、"_サイトのプライバシー ポリシーを詳しく説明するには、このページを使用してください_" の文章を削除して、その場所に "_このページは、@ViewData["TimeStamp"]_ 時点、作成中です" という文章を追加します。

    ![Privacy.cshtml ファイル内のテキストを変更する](media/vs-2019/csharp-aspnet-privacy-cshtml-code-changed.png)

1. それでは、コードを変更してみましょう。 **Privacy.cshtml.cs** を選択します。 次に、次のショートカットを使用して、ファイルの上部にある `using` ディレクティブをクリーンアップします。

   灰色表示の `using` ディレクティブのいずれかを選択すると、キャレットのすぐ下、または左余白に[クイック アクション](../../ide/quick-actions.md) (電球) が表示されます。 電球を選択してから、 **[不要な using の削除]** にマウス ポインターを移動します。

   ![Privacy.cshtml.cs の不要な using を削除する](media/vs-2019/csharp-aspnet-remove-unnecessary-usings.png)

   ここで、 **[変更のプレビュー]** を選択して、変更内容を確認します。

   ![変更のプレビュー](media/vs-2019/csharp-aspnet-preview-changes.png)

   **[適用]** を選択します。 Visual Studio では、ファイルから不要な `using` ディレクティブが削除されます。

1. 次に、`OnGet()` メソッドの本体を次のコードに変更します。

     ```csharp
     public void OnGet()
     {
        string dateTime = DateTime.Now.ToShortDateString();
        ViewData["TimeStamp"] = dateTime;
     }
    ```

1. **DateTime** の下に波形の下線が 2 本表示されることに注意してください。 波形の下線が表示されるのは、これらの種類がスコープに含まれないためです。

   ![OnGet メソッドで波形の下線でマークされたエラー](media/vs-2019/csharp-aspnet-add-new-onget-method.png)

    **[エラー一覧]** ツール バーを開くと、そこに同じエラーが一覧表示されます ( **[エラー一覧]** ツール バーが表示されない場合は、上部のメニュー バーで **[表示]**  >  **[エラー一覧]** の順に選択します)。

   ![Visual Studio の [エラー一覧]](media/vs-2019/csharp-aspnet-error-list.png)

1. これを修正しましょう。 コードエディターで、エラーを含むいずれかの行にカーソルを置いた後、左余白のクイック アクション (電球) を選択します。 次に、ドロップダウン メニューから、 **[using System;]** を選択してファイルの先頭にこのディレクティブを追加し、エラーを解決します。

   !["using System;" ディレクティブを追加する](media/vs-2019/csharp-aspnet-add-usings.png)

1. **F5** キーを押して、Web ブラウザーでプロジェクトを開きます。

1. Web サイトの上部で **[Privacy]** を選択し、変更を確認します。

   ![加えた変更が含まれる、更新後の Privacy ページを表示する](media/vs-2019/csharp-aspnet-browser-page-privacy-changed.png)

1. Web ブラウザーを閉じ、**Shift**+**F5** キーを押してデバッグ モードを停止したら、Visual Studio を閉じます。
::: moniker-end

## <a name="quick-answers-faq"></a>FAQ に対する簡単な回答

以下の簡単な FAQ で、主な概念をいくつか示します。

### <a name="what-is-c"></a>C# とは何ですか?

[C#](https://docs.microsoft.com/dotnet/csharp/tour-of-csharp/) は、堅牢でありながら習得しやすいように設計されたタイプ セーフなオブジェクト指向のプログラミング言語です。

### <a name="what-is-aspnet-core"></a>ASP.NET Core とは何ですか?

ASP.NET Core は、Web アプリやサービスなど、インターネットに接続されているアプリケーションを構築するためのオープンソースのクロスプラットフォーム フレームワークです。 ASP.NET Core アプリは .NET Core または .NET Framework で実行できます。 Windows、Mac、Linux 上で、ASP.NET Core アプリ クロスプラットフォームを開発して実行することができます。 ASP.NET Core は [GitHub](https://github.com/aspnet/home) でオープン ソースとして公開されています。

### <a name="what-is-visual-studio"></a>Visual Studio とは何ですか?

Visual Studio は、開発者向け生産性向上ツールの統合開発スイートです。 プログラムやアプリケーションを作成するために使用できるプログラムのようなものと考えてください。

## <a name="next-steps"></a>次の手順

これでこのチュートリアルは完了です。 C#、ASP.NET Core、Visual Studio IDE について少しはご理解いただけたかと思います。 C# と ASP.NET を使用する Web アプリまたは Web サイトの作成方法の詳細については、以下のチュートリアルに進んで確認してください。

> [!div class="nextstepaction"]
> [ASP.NET Core で Razor ページ Web アプリを作成する](/aspnet/core/tutorials/razor-pages/?view=aspnetcore-2.1&preserve-view=true)

## <a name="see-also"></a>関連項目

[Visual Studio を使用して Azure App Service に Web アプリを発行する](../../deployment/quickstart-deploy-to-azure.md)
