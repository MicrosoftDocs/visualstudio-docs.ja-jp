---
title: Node.js と Express のアプリを作成する
description: このチュートリアルでは、Visual Studio の Express Web アプリケーション フレームワークを使用し、簡単な Node.js アプリケーションを作成する方法について説明します。
ms.date: 03/25/2021
ms.custom: vs-acquisition
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: d4ea086d20f5a1000067343ac7571a9a8f8309db
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386814"
---
# <a name="tutorial-create-a-nodejs-and-express-app-in-visual-studio"></a>チュートリアル:Visual Studio で Node.js と Express のアプリを作成する

このチュートリアルでは、Node.js と Express を使用して Visual Studio を開発します。単純な Node.js Web アプリを作成し、いくつかのコードを追加し、IDE の一部の機能を試し、アプリを実行します。 

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2022"

Visual Studio 2022 プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

このチュートリアルでは、以下の内容を学習します。
> [!div class="checklist"]
> * Node.js プロジェクトを作成する
> * 何らかのコードを追加する
> * IntelliSense を使用してコードを編集する
> * アプリを実行する
> * デバッガーでブレークポイントに達する

## <a name="before-you-begin"></a>開始する前に

以下の簡単な FAQ で、主要な概念をいくつか紹介します。

### <a name="what-is-nodejs"></a>Node.js とは何か

Node.js はサーバー側の JavaScript ランタイム環境であり、サーバー側の JavaScript を実行します。

### <a name="what-is-npm"></a>npm とは何か

npm は Node.js の既定のパッケージ マネージャーです。 このパッケージ マネージャーはライブラリのインストール、更新、アンインストールを簡易化するように設計されており、プログラマーはこれを利用することで Node.js ライブラリのソース コードを簡単に公開し、共有できます。

### <a name="what-is-express"></a>Express とは何か

Express は Web アプリケーション フレームワークであり、Node.js が Web アプリケーションをビルドする際、サーバー フレームワークとして利用されます。 Express では、Pug (以前の Jade) など、UI を作成するためのさまざまなフロントエンド フレームワークを選択できます。 このチュートリアルで Pug を使用します。

## <a name="prerequisites"></a>前提条件

* Visual Studio および Node.js 開発ワークロードをインストールしている必要があります。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end

    Visual Studio は既にあり、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動すると、Visual Studio インストーラーが開きます。 **[Node.js 開発]** ワークロードを選択し、 **[変更]** を選択します。

    ![VS インストーラーの Node.js ワークロード](../ide/media/quickstart-nodejs-workload.png)

* Node.js ランタイムをインストールしている必要があります。

    インストールされていない場合は、[Node.js](https://nodejs.org/en/download/) Web サイトから LTS バージョンをインストールして、外部のフレームワークおよびライブラリとの最善の互換性を確保することをお勧めします。 Node.js は、32 ビットおよび 64 ビット アーキテクチャ用にビルドされています。 Visual Studio の Node.js ツールは Node.js ワークロードに含まれており、両方のバージョンをサポートしています。 必要なのは 1 つだけであり、Node.js インストーラーでは、一度に 1 つのインストールのみをサポートしています。
    
    一般に、Visual Studio はインストール済みの Node.js ランタイムを自動的に検出します。 インストール済みのランタイムが検出されない場合は、プロパティ ページ上のインストール済みのランタイムを参照するようにプロジェクトを構成することができます (プロジェクトを作成した後、プロジェクト ノードを右クリックして、 **[プロパティ]** を選択し、 **[Node.exe のパス]** を設定します)。 Node.js のグローバル インストールを使用するか、または Node.js プロジェクトごとにローカル インタープリターへのパスを指定することが可能です。 

    このチュートリアルは、Node.js 8.10.0 でテストされました。

## <a name="create-a-new-nodejs-project"></a>Node.js プロジェクトを新規作成する

Visual Studio では、*プロジェクト* の 1 つのアプリケーションに対してファイルが管理されます。 プロジェクトには、ソース コード、リソース、構成ファイルが含まれています。

このチュートリアルでは、Node.js と Express アプリのコードを含む簡単なプロジェクトから開始します。

1. Visual Studio を開きます。

1. 新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**Node.js**」と入力してから、 **[新しい基本の Azure Node.js Express 4 アプリケーション プロジェクトの作成]** (JavaScript) を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[JavaScript]** を展開して、 **[Node.js]** を選択します。 真ん中のウィンドウで **[基本の Azure Node.js Express 4 アプリケーション]** を選択し、 **[OK]** を選択します。
    ::: moniker-end
    **[基本の Azure Node.js Express 4 アプリケーション]** プロジェクト テンプレートが表示されない場合は、**Node.js 開発** ワークロードを追加する必要があります。 手順について詳しくは、「[必須コンポーネント](#prerequisites)」をご覧ください。

    Visual Studio は新しいソリューションを作成し、右のウィンドウでプロジェクトを開きます。 *app.js* プロジェクト ファイルがエディター (左のウィンドウ) で開きます。

    ![プロジェクト構造](../javascript/media/tutorial-project-structure.png)

    (1) **[新しいプロジェクト]** ダイアログ ボックスに指定した名前が使用され、**太字** で強調表示されているのがあなたのプロジェクトです。 ファイル システムでは、このプロジェクトは、プロジェクト フォルダーの *.njsproj* ファイルに該当します。 プロジェクトを右クリックし、 **[プロパティ]** を選択することで、プロジェクトに関連付けられたプロパティと環境変数を設定することができます。 プロジェクト ファイルでは Node.js プロジェクト ソースへのカスタム変更が行われないため、他の開発ツールを使用してラウンド トリップを行うことができます。

    (2) 最上位レベルにあるのは、ソリューションです。既定では、名前はプロジェクトと同じです。 ディスク上の *.sln* ファイルで表されるソリューションは、1 つ以上の関連プロジェクトのコンテナーです。

    (3) npm ノードには、インストールされているすべての npm パッケージが表示されます。 npm ノードを右クリックすれば、ダイアログ ボックスを利用して npm パッケージを検索し、インストールできます。または、*package.json* の設定と npm ノードの右クリック オプションを利用してパッケージをインストールし、更新できます。

    (4) *package.json* は、ノーカルでインストールされているパッケージのパッケージ依存関係とパッケージ バージョンを管理する目的で npm によって使用されるファイルです。 詳細については、[npm パッケージの管理](../javascript/npm-package-management.md)に関するページを参照してください。

    (5) プロジェクト ノードの下に、*app.js* などのプロジェクト ファイルが表示されます。 *app.js* はプロジェクト スタートアップ ファイルであり、そのため、**太字** で表示されます。 プロジェクトでファイルを右クリックし、 **[Node.js スタートアップ スクリプトとして設定]** を選択することで、スタートアップ ファイルを設定できます。

1. **npm** ノードを開き、必要なすべての npm パッケージが存在するかどうかを確認します。

    不足しているパッケージ (感嘆符のアイコン) がある場合は、**npm** ノードを右クリックして、 **[npm パッケージのインストール]** を選択します。

## <a name="add-some-code"></a>何らかのコードを追加する

このアプリケーションでは、フロントエンド JavaScript フレームワークに Pug を使用します。 Pug は、HTML にコンパイルされる簡単なマークアップ コードを使用します。 (Pug は *app.js* にビュー エンジンとして設定されています。 *app.js* でビュー エンジンを設定するコードは `app.set('view engine', 'pug');` です。)

1. ソリューション エクスプローラー (右のウィンドウ) で、[views] フォルダーを開き、*index.pug* を開きます。

1. 内容を次のマークアップで置換します。

    ```js
    extends layout

    block content
      h1= title
      p Welcome to #{title}
      script.
        var f1 = function() { document.getElementById('myImage').src='#{data.item1}' }
      script.
        var f2 = function() { document.getElementById('myImage').src='#{data.item2}' }
      script.
        var f3 = function() { document.getElementById('myImage').src='#{data.item3}' }

      button(onclick='f1()') One!
      button(onclick='f2()') Two!
      button(onclick='f3()') Three!
      p
      a: img(id='myImage' height='200' width='200' src='')
    ```

    上記のコードは、タイトルとようこそメッセージを含む HTML ページを動的に生成するために使用されます。 また、このページには、ボタンをクリックするたびに変化するイメージを表示するコードも含まれています。

1. ルート フォルダーに *index.js* を開きます。

1. `router.get` の呼び出しの前に次のコードを追加します。

    ```js
    var getData = function () {
        var data = {
            'item1': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-76.jpg',
            'item2': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-77.jpg',
            'item3': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-78.jpg'
        }
        return data;
    }
    ````

    このコードは、動的に生成された HTML ページに渡すデータ オブジェクトを作成します。

1. `router.get` 関数呼び出しを次のコードで置換します。

    ```js
    router.get('/', function (req, res) {
        res.render('index', { title: 'Express', "data" });
    });
    ```

    上記のコードは、Express ルーター オブジェクトを使って現在のページを設定し、ページにタイトルとデータ オブジェクトを渡してページをレンダリングします。 *index.js* が実行されるときに読み込まれるページとして *index.pug* ファイルがここで指定されます。 *index.js* は *app.js* コードで既定のルートとして構成されます (画像はこのページにありません)。

    Visual Studio のいくつかの機能を示すため、`res.render` を含むコード行に意図的なエラーが組み込まれています。 このエラーはアプリを実行する前に修正する必要があります。これは次のセクションで行います。

## <a name="use-intellisense"></a>IntelliSense を使用する

IntelliSense は、コードの記述を支援する Visual Studio ツールです。

1. *index.js* で、`res.render` を含むコードの行に移動します。

1. `data` 文字列の後にカーソルを置き、「`: get`」と入力します。コードの前半で定義されている `getData` 関数が IntelliSense によって表示されます。 [`getData`] を選択します。

    ![IntelliSense を使用する](../javascript/media/tutorial-nodejs-intellisense.png)

1. かっこを追加して、関数呼び出し `getData()`にします。

1. `"data"` の前のコンマ (`,`) を削除します。式で緑の構文が強調表示されます。 構文の強調表示にカーソルを合わせます。

    ![構文エラーの表示](../javascript/media/tutorial-nodejs-syntax-checking.png)

    このメッセージの最後の行から、JavaScript インタープリターはコンマ (`,`) を要求していることがわかります。

1. 下のペインで、 **[エラー一覧]** タブをクリックし、報告された問題の種類に対して **[ビルド + IntelliSense]** を選択します。

    ファイル名と行番号と共に警告と説明が表示されます。

    ![エラー一覧の表示](../javascript/media/tutorial-nodejs-error-list.png)

1. コードを修正します。`"data"` の前にコンマ (`,`) を追加してください。

    修正後、コード行は `res.render('index', { title: 'Express', "data": getData() });` のようになります。

## <a name="set-a-breakpoint"></a>ブレークポイントの設定

次に、Visual Studio デバッガーがアタッチされた状態でアプリを実行します。 これを行う前に、ブレークポイントを設定する必要があります。

1. *index.js* で、次のコード行の前にある左の余白をクリックし、ブレークポイントを設定します。

    `res.render('index', { title: 'Express', "data": getData() });`

    ブレークポイントは、信頼できるデバッグの最も基本的で重要な機能です。 ブレークポイントは、Visual Studio が実行コードを中断する場所を示します。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。

    ![ブレークポイントの設定](../javascript/media/tutorial-nodejs-set-breakpoint.png)

## <a name="run-the-application"></a>アプリケーションの実行

1. デバッグ ツールバーで、**Web サーバー (Google Chrome)** や **Web サーバー (Microsoft Edge)** などのデバッグ ターゲットを選択します。

    ::: moniker range=">=vs-2019"
    ![デバッグ ターゲットを選択する](../javascript/media/vs-2019/tutorial-nodejs-deploy-target.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![デバッグ ターゲットを選択する](../javascript/media/tutorial-nodejs-deploy-target.png)
    ::: moniker-end

    Chrome をコンピューターで使用できるのにオプションには表示されない場合は、デバッグ ターゲットのドロップダウン リストから **[Browse With]\(ブラウザー\)** を選択し、Chrome を既定のブラウザーに選択します ( **[Set as Default]\(既定値として設定\)** を選択)。

1. **F5** キー ( **[デバッグ]**  >  **[デバッグの開始]** ) を押してアプリケーションを実行します。

    設定したブレークポイントのところでデバッガーが一時停止します。 ここで、アプリの状態を確認できます。

1. `getData` の上にカーソルを合わせ、データヒントでそのプロパティを確認する

    ![変数の検査](../javascript/media/tutorial-nodejs-inspect-variables.png)

1. **F5** キー ( **[デバッグ]**  >  **[続行]** ) を押して続行します。

    アプリがブラウザーで開きます。

    ブラウザー ウィンドウで、タイトルとして "Express" を、最初の段落で "Welcome to Express" を確認できます。

1. ボタンをクリックすると、さまざま画像が表示されます。

    ![ブラウザーで実行しているアプリ](../javascript/media/tutorial-nodejs-running-in-browser.png)

1. Web ブラウザーを閉じます。

## <a name="optional-publish-to-azure-app-service"></a>(省略可能) Azure App Service に発行する

1. ソリューション エクスプローラーで、プロジェクトを右クリックして、 **[発行]** を選択します。

   ![Azure App Service に発行する](../javascript/media/tutorial-nodejs-publish-to-azure.png)

1. **[Microsoft Azure App Service]** を選択します。

    **[App Service]** ダイアログ サービスで、Azure アカウントにサインインし、既存の Azure サブスクリプションに接続できます。

1. 残りの手順に従い、サブスクリプションを選択し、リソース グループを選択または作成し、App Service プランを選択または作成し、Azure に公開するように求められたらその手順に従います。 詳しい手順については、「[Publish to Azure website using web deploy](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy)」 (Web 配置を使用して Azure Web サイトに発行する) を参照してください。

1. **[出力]** ウィンドウには、Azure へのデプロイの進捗状況が表示されます。

    デプロイに成功すると、Azure App Service で実行されているアプリがブラウザーで開きます。 ボタンをクリックすると、画像が表示されます。

   ![Azure App Service で実行されているアプリ](../javascript/media/tutorial-nodejs-running-in-azure.png)

これでこのチュートリアルは完了です。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリを Linux App Service にデプロイする](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [AngularJS Language Service 拡張機能](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)
