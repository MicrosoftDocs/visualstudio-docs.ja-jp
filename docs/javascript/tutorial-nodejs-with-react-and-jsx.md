---
title: Node.js と React のアプリを作成する
description: Visual Studio のテンプレートから Node.js Web アプリケーション プロジェクトを作成する方法を学習します。
ms.custom: ''
ms.date: 4/21/2020
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 80516adffcb058d6ce28751e7a9f30002ca3a640
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729300"
---
# <a name="tutorial-create-a-nodejs-and-react-app-in-visual-studio"></a>チュートリアル: Visual Studio で Node.js と React のアプリを作成する

Visual Studio では、Node.js プロジェクトを簡単に作成することができ、IntelliSense や、Node.js をサポートする他の組み込み機能を体験できます。 Visual Studio に関するこのチュートリアルでは、Visual Studio のテンプレートから Node.js Web アプリケーション プロジェクトを作成します。 その後、React を使って簡単なアプリを作成します。

このチュートリアルでは、次の作業を行う方法について説明します。
> [!div class="checklist"]
> * Node.js プロジェクトを作成する
> * npm パッケージを追加する
> * アプリに React コードを追加する
> * JSX をトランスパイルする
> * デバッガーをアタッチします。

## <a name="before-you-begin"></a>始める前に

以下の簡単な FAQ で、主要な概念をいくつか紹介します。

### <a name="what-is-nodejs"></a>Node.js とは何か

Node.js はサーバー側の JavaScript ランタイム環境であり、サーバー側の JavaScript を実行します。

### <a name="what-is-npm"></a>npm とは何か

npm は Node.js の既定のパッケージ マネージャーです。 このパッケージ マネージャーはライブラリのインストール、更新、アンインストールを簡易化するように設計されており、プログラマーはこれを利用することで Node.js ライブラリのソース コードを簡単に公開し、共有できます。

### <a name="what-is-react"></a>React とは何か

React は、UI を作成するフロントエンド フレームワークです。

### <a name="what-is-jsx"></a>JSX とは何か

JSX は JavaScript 構文の拡張機能で、通常は UI 要素を記述するために React で使用されます。 JSX コードをブラウザーで実行するには、事前にプレーンな JavaScript にトランスパイルする必要があります。

### <a name="what-is-webpack"></a>webpack とは何か

webpack は、ブラウザーで実行できるように JavaScript ファイルをバンドルします。 他のリソースやアセットを変換またはパッケージ化することもできます。 これは、JSX または TypeScript のコードをプレーンな JavaScript にトランスパイルするため、Babel や TypeScript などのコンパイラを指定するためによく使用されます。

## <a name="prerequisites"></a>必須コンポーネント

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

    このチュートリアルは、バージョン 12.6.2 でテストされました。

    インストールされていない場合は、[Node.js](https://nodejs.org/en/download/) Web サイトから LTS バージョンをインストールして、外部のフレームワークおよびライブラリとの最善の互換性を確保することをお勧めします。 Node.js は、32 ビットおよび 64 ビット アーキテクチャ用にビルドされています。 Visual Studio の Node.js ツールは Node.js ワークロードに含まれており、両方のバージョンをサポートしています。 必要なのは 1 つだけであり、Node.js インストーラーでは、一度に 1 つのインストールのみをサポートしています。

    一般に、Visual Studio はインストール済みの Node.js ランタイムを自動的に検出します。 インストール済みのランタイムが検出されない場合は、プロパティ ページでインストール済みのランタイムを参照するようにプロジェクトを構成できます (プロジェクトを作成した後、プロジェクト ノードを右クリックして、 **[プロパティ]** を選択し (または **Alt** + **Enter** キーを押し)、 **[Node.exe のパス]** を設定します)。 Node.js のグローバル インストールを使用するか、または Node.js プロジェクトごとにローカル インタープリターへのパスを指定することが可能です。 

## <a name="create-a-project"></a>プロジェクトを作成する

まず、Node.js Web アプリケーション プロジェクトを作成します。

1. Visual Studio を開きます。

1. 新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**Node.js**」と入力してから、 **[空の Node.js Web アプリケーション]** (JavaScript) を選択します (このチュートリアルでは TypeScript コンパイラが使用されますが、手順では **JavaScript** テンプレートから始める必要があります)。
    
    表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[JavaScript]** を展開して、 **[Node.js]** を選択します。 中央のウィンドウで、 **[空白の Node.js Web アプリケーション]** を選択し、名前に「**NodejsWebAppBlank**」と入力してから、 **[OK]** を選択します。
    ::: moniker-end
    **[空白の Node.js Web アプリケーション]** プロジェクト テンプレートが表示されない場合は、**Node.js 開発** ワークロードを追加する必要があります。 手順について詳しくは、「[必須コンポーネント](#prerequisites)」をご覧ください。

    Visual Studio は新しいソリューションを作成し、プロジェクトを開きます。

    ![ソリューション エクスプローラーでの Node.js プロジェクト](../javascript/media/tutorial-nodejs-react-project-structure.png)

    (1) **[新しいプロジェクト]** ダイアログ ボックスに指定した名前が使用され、**太字** で強調表示されているのがあなたのプロジェクトです。 ファイル システムでは、このプロジェクトは、プロジェクト フォルダーの *.njsproj* ファイルに該当します。 プロジェクトを右クリックし、 **[プロパティ]** を選択することで (または **Alt** + **Enter** キーを押して)、プロジェクトに関連付けられたプロパティと環境変数を設定できます。 プロジェクト ファイルでは Node.js プロジェクト ソースへのカスタム変更が行われないため、他の開発ツールを使用してラウンド トリップを行うことができます。

    (2) 最上位レベルにあるのは、ソリューションです。既定では、名前はプロジェクトと同じです。 ディスク上の *.sln* ファイルで表されるソリューションは、1 つ以上の関連プロジェクトのコンテナーです。

    (3) npm ノードには、インストールされているすべての npm パッケージが表示されます。 npm ノードを右クリックすれば、ダイアログ ボックスを利用して npm パッケージを検索し、インストールできます。または、*package.json* の設定と npm ノードの右クリック オプションを利用してパッケージをインストールし、更新できます。

    (4) *package.json* は、ノーカルでインストールされているパッケージのパッケージ依存関係とパッケージ バージョンを管理する目的で npm によって使用されるファイルです。 詳細については、[npm パッケージの管理](../javascript/npm-package-management.md)に関するページを参照してください。

    (5) プロジェクト ノードの下に、*server.js* などのプロジェクト ファイルが表示されます。 *server.js* はプロジェクト スタートアップ ファイルであり、そのため、**太字** で表示されます。 プロジェクトでファイルを右クリックし、 **[Node.js スタートアップ スクリプトとして設定]** を選択することで、スタートアップ ファイルを設定できます。

## <a name="add-npm-packages"></a>npm パッケージを追加する

このアプリを正常に実行するには、複数の npm モジュールが必要です。

* react
* react-dom
* express
* path
* ts-loader
* typescript
* webpack
* webpack-cli

1. ソリューション エクスプローラー (右側のウィンドウ) で、プロジェクトの **npm** ノードを右クリックして、 **[新しい npm パッケージのインストール]** を選びます。

    **[新しい npm パッケージのインストール]** ダイアログ ボックスでは、最新バージョンのパッケージをインストールするか、バージョンを指定してインストールできます。 最新バージョンのパッケージをインストールして予期しないエラーが発生する場合は、後の手順で説明する正確なバージョンのパッケージをインストールしてください。

1. **[新しい npm パッケージのインストール]** ダイアログ ボックスで、react パッケージを探し、 **[パッケージのインストール]** を選択してインストールします。

    ![npm パッケージをインストールする](../javascript/media/tutorial-nodejs-react-install-package.png)

    **[出力]** ウィンドウを選択すると、パッケージ インストールの進捗状況が表示されます ( **[出力元の表示]** フィールドで **[npm]** を選択してください)。 インストールが済むと、**npm** ノードの下にパッケージが表示されます。

    プロジェクトの *package.json* ファイルが、パッケージのバージョンなど、新しいパッケージの情報で更新されます。

1. UI を使って残りのパッケージを 1 つずつ検索して追加する代わりに、次のコードを *package.json* に貼り付けます。 これを行うには、このコードを使用して `dependencies` セクションを追加します。

    ```json
    "dependencies": {
      "express": "~4.17.1",
      "path": "~0.12.7",
      "react": "~16.13.1",
      "react-dom": "~16.13.1",
      "ts-loader": "~7.0.1",
      "typescript": "~3.8.3",
      "webpack": "~4.42.1",
      "webpack-cli": "~3.3.11"
    }
    ```

    ご使用のバージョンの空のテンプレートに `dependencies` セクションが既にある場合は、それを上記の JSON コードに置き換えるだけで済みます。 このファイルの使用の詳細については、「[package.json の構成](../javascript/configure-packages-with-package-json.md)」を参照してください。

1. 変更を保存します。

1. プロジェクトで **npm** ノードを右クリックして、 **[npm パッケージのインストール]** を選択します。

    このコマンドでは、npm インストール コマンドが直接実行されます。

    下のウィンドウで **[出力]** ウィンドウを選択すると、パッケージ インストールの進行状況が表示されます。 インストールには数分かかることがあります。結果がすぐに表示されないことがあります。 出力を確認するには、 **[出力]** ウィンドウの **[出力元の表示]** フィールドで **[Npm]** を選択していることを確認します。 (ウィンドウを開くには、 **[表示]**  >  **[出力]** を選択するか、**Ctrl** + **Alt** + **O** キーを押します。)

    npm モジュールがインストールされると、ソリューション エクスプローラーの表示は次のようになります。

    ![npm パッケージ](../javascript/media/tutorial-nodejs-react-npm-modules-installed.png)

    > [!NOTE]
    > コマンド ラインを使って npm パッケージをインストールした方がよい場合は、プロジェクト ノードを右クリックし、 **[ここでコマンド プロンプトを開く]** を選びます。 Node.js の標準コマンドを使ってパッケージをインストールします。

## <a name="add-project-files"></a>プロジェクト ファイルを追加する

以下の手順では、プロジェクトに 4 つの新しいファイルを追加します。

* *app.tsx*
* *webpack-config.js*
* *index.html*
* *tsconfig.json*

この簡単なアプリでは、プロジェクトのルートに新しいプロジェクト ファイルを追加します (ほとんどのアプリでは、通常、サブフォルダーにファイルを追加し、それに応じて相対パスの参照を調整します)。

1. ソリューション エクスプローラーで、プロジェクト **NodejsWebAppBlank** を右クリックし、 **[追加]**  >  **[新しい項目]** を選択します (または **Ctrl** + **SHIFT** + **A** キーを押します)。

1. **[新しい項目の追加]** ダイアログ ボックスで、 **[TypeScript JSX ファイル]** を選び、名前に「*app.tsx*」と入力して、 **[追加]** または **[OK]** を選択します。

1. 同じ手順を繰り返して *webpack-config.js* を追加します。 TypeScript JSX ファイルの代わりに、 **[JavaScript ファイル]** を選択します。

1. 同じ手順を繰り返して *index.html* をプロジェクトに追加します。 JavaScript ファイルではなく、 **[HTML ファイル]** を選びます。

1. 同じ手順を繰り返して *tsconfig.json* をプロジェクトに追加します。 JavaScript ファイルではなく **[TypeScript JSON 構成ファイル]** を選びます。

## <a name="add-app-code"></a>アプリのコードを追加する

1. *server.js* を開き、既存のコードを次のコードと置き換えます。

    ```javascript
    'use strict';
    var path = require('path');
    var express = require('express');

    var app = express();

    var staticPath = path.join(__dirname, '/');
    app.use(express.static(staticPath));

    // Allows you to set port in the project properties.
    app.set('port', process.env.PORT || 3000);

    var server = app.listen(app.get('port'), function() {
        console.log('listening');
    });
    ```

   上記のコードは、Express を使用し、Web アプリケーション サーバーとして Node.js を起動します。 このコードは、プロジェクトのプロパティで構成されているポート番号にポートを設定します (既定では、ポートはプロパティで 1337 に構成されます)。 プロジェクトのプロパティを開くには、ソリューション エクスプローラーでプロジェクトを右クリックして、 **[プロパティ]** を選びます。

1. *app.tsx* を開き、次のコードを追加します。

    ```javascript
    declare var require: any

    var React = require('react');
    var ReactDOM = require('react-dom');

    export class Hello extends React.Component {
        render() {
            return (
                <h1>Welcome to React!!</h1>
            );
        }
    }

    ReactDOM.render(<Hello />, document.getElementById('root'));
    ```

    上記のコードは、JSX 構文と React を使って、簡単なメッセージを表示します。

1. *index.html* を開き、**body** セクションを次のコードに置き換えます。

    ```html
    <body>
        <div id="root"></div>
        <!-- scripts -->
        <script src="./dist/app-bundle.js"></script>
    </body>
    ```

    この HTML ページは *app-bundle.js* を読み込みます。このファイルには、プレーンな JavaScript にトランスパイルされた JSX と React のコードが含まれます。 現在、*app-bundle.js* ファイルは空です。 次のセクションでは、コードをトランスパイルするためのオプションを構成します。

## <a name="configure-webpack-and-typescript-compiler-options"></a>webpack と TypeScript のコンパイラ オプションを構成する

前の手順では、*webpack-config.js* をプロジェクトに追加しました。 ここでは次に、webpack の構成コードを追加します。 JSX をバンドルしてプレーンな JavaScript にトランスパイルするための入力ファイル (*app.tsx*) と出力ファイル (*app-bundle.js*) を指定する、webpack の簡単な構成を追加します。 トランスパイルについては、TypeScript のコンパイラ オプションもいくつか構成します。 このコードは、webpack と TypeScript コンパイラの概要を説明するための基本的な構成です。

1. ソリューション エクスプローラーで *webpack-config.js* を開き、次のコードを追加します。

    ```json
    module.exports = {
        devtool: 'source-map',
        entry: "./app.tsx",
        mode: "development",
        output: {
            filename: "./app-bundle.js"
        },
        resolve: {
            extensions: ['.Webpack.js', '.web.js', '.ts', '.js', '.jsx', '.tsx']
        },
        module: {
            rules: [
                {
                    test: /\.tsx$/,
                    exclude: /(node_modules|bower_components)/,
                    use: {
                        loader: 'ts-loader'
                    }
                }
            ]
        }
    }
    ```

    webpack 構成コードでは、TypeScript ローダーを使って JSX をトランスパイルするよう webpack に指示されます。

1. *tsconfig.json* を開き、TypeScript コンパイラ オプションを指定する次のコードで既定のコードを置換します。

    ```json
    {
      "compilerOptions": {
        "noImplicitAny": false,
        "module": "commonjs",
        "noEmitOnError": true,
        "removeComments": false,
        "sourceMap": true,
        "target": "es5",
        "jsx": "react"
      },
      "exclude": [
        "node_modules"
      ],
      "files": [
        "app.tsx"
      ]
    }
    ```

    *app.tsx* は、ソース ファイルとして指定されています。

## <a name="transpile-the-jsx"></a>JSX をトランスパイルする

1. ソリューション エクスプローラーで、プロジェクト ノードを右クリックして、 **[ここでコマンド プロンプトを開く]** を選びます。

1. コマンド プロンプトに次のコマンドを入力します。

    `node_modules\.bin\webpack app.tsx --config webpack-config.js`

    コマンド プロンプト ウィンドウに結果が表示されます。

    ![webpack を実行する](../javascript/media/tutorial-nodejs-react-run-webpack-cmd.png)

    上記の出力ではなく何らかのエラーが表示される場合は、それを解決しないとアプリは動きません。 npm パッケージのバージョンがこのチュートリアルで示されているバージョンと異なる場合は、エラーの原因になる可能性があります。 エラーを修正する方法の 1 つは、前の手順で示されている正確なバージョンを使うことです。 また、これらのパッケージ バージョンの中に非推奨となったものがあるためにエラーが発生する場合は、エラーを修正するにはより新しいバージョンをインストールする必要があります。 *package.json* を使用した npm パッケージのバージョン管理に関する詳細は、「[package.json configuration](../javascript/configure-packages-with-package-json.md)」 (package.json の構成) を参照してください。

1. ソリューション エクスプローラーでプロジェクト ノードを右クリックして、 **[追加]**  >  **[既存のフォルダー]** を選択し、*dist* フォルダーを選んで、 **[フォルダーの選択]** を選択します。

    *dist* フォルダーがプロジェクトに追加されます。このフォルダーには、*app-bundle.js* と *app-bundle.js.map* が含まれます。

1. *app-bundle.js* を開き、トランスパイルされた JavaScript コードを表示します。

1. 外部で変更されたファイルを再度読み込むように求めるメッセージが表示される場合は、 **[すべてはい]** を選択します。

    ![変更されたファイルを読み込む](../javascript/media/tutorial-nodejs-react-reload-files.png)

*app.tsx* を変更するたびに、webpack コマンドを再実行する必要があります。 この手順を自動化するには、JSX をトランスパイルするビルド スクリプトを追加します。

## <a name="add-a-build-script-to-transpile-the-jsx"></a>JSX をトランスパイルするビルド スクリプトを追加する

Visual Studio 2019 以降では、ビルド スクリプトが必須です。 (前のセクションで示したように) コマンド ラインで JSX をトランスパイルするのでなく、Visual Studio からビルドするときに JSX をトランスパイルすることができます。

* *package.json* を開き、`dependencies` セクションの後に次のセクションを追加します。

   ```json
   "scripts": {
    "build": "webpack-cli app.tsx --config webpack-config.js"
   }
   ```

## <a name="run-the-app"></a>アプリを実行する

1. **Web サーバー (Google Chrome)** または **Web サーバー (Microsoft Edge)** のいずれかを現在のデバッグ ターゲットとして選択します。

    ::: moniker range=">=vs-2019"
    ![デバッグ ターゲットとして Chrome を選ぶ](../javascript/media/vs-2019/tutorial-nodejs-react-debug-target.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![デバッグ ターゲットとして Chrome を選ぶ](../javascript/media/tutorial-nodejs-react-debug-target.png)
    ::: moniker-end

    Chrome をコンピューターで使用できるのにオプションには表示されない場合は、デバッグ ターゲットのドロップダウン リストから **[Browse With]\(ブラウザー\)** を選択し、Chrome を既定のブラウザーに選択します ( **[Set as Default]\(既定値として設定\)** を選択)。

1. アプリを実行するには、**F5** キーを押すか ( **[デバッグ]**  >  **[デバッグの開始]** )、または緑の矢印ボタンをクリックします。

    Node.js コンソール ウィンドウが開き、デバッガーがリッスンしているポートが示されます。

    Visual Studio は、スタートアップ ファイル *server.js* を起動することにより、アプリを起動します。

    ![ブラウザーで React を実行する](../javascript/media/tutorial-nodejs-react-running-react.png)

1. ブラウザー ウィンドウを閉じます。

1. コンソール ウィンドウを閉じます。

## <a name="set-a-breakpoint-and-run-the-app"></a>ブレークポイントを設定してアプリを実行する

1. *server.js* で、`staticPath` 宣言の左側の余白をクリックして、ブレークポイントを設定します。

    ![server.js に関する Visual Studio のコード ウィンドウのスクリーンショット。 左側の余白の赤い点は、staticPath 宣言にブレークポイントが設定されていることを示します。](../javascript/media/tutorial-nodejs-react-set-breakpoint.png)

    ブレークポイントは、信頼できるデバッグの最も基本的で重要な機能です。 ブレークポイントは、Visual Studio が実行コードを中断する場所を示します。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。

1. アプリを実行するには、**F5** キー ( **[デバッグ]**  >  **[デバッグの開始]** ) を押します。

    設定したブレークポイントでデバッガーが一時停止します (現在のステートメントは黄色でマークされます)。 ここで、 **[ローカル]** ウィンドウや **[ウォッチ]** ウィンドウなどのデバッガー ウィンドウを使って、現在スコープ内にある変数をマウスでポイントすることにより、アプリの状態を調べることができます。

1. アプリを続行するには **F5** キーを押します。

1. Chrome の開発者ツールまたは Microsoft Edge の F12 ツールを使う場合は、**F12** キーを押します。 これらのツールでは、DOM を調べたり、JavaScript コンソールを使ってアプリを操作したりできます。

1. Web ブラウザーとコンソールを閉じます。

## <a name="set-and-hit-a-breakpoint-in-the-client-side-react-code"></a>クライアント側の React コードにブレークポイントを設定してヒットする

前のセクションでは、サーバー側の Node.js コードにデバッガーをアタッチしました。 クライアント側の React コードに Visual Studio からデバッガーをアタッチしてブレークポイントをヒットするには、デバッガーが正しいプロセスを識別できるように手助けする必要があります。 ここではその方法の 1 つを示します。

### <a name="prepare-the-browser-for-debugging"></a>デバッグのためにブラウザーを準備する

::: moniker range=">=vs-2019"
このシナリオでは、現在 IDE 上で **Microsoft Edge Beta** という名前になっている Microsoft Edge (Chromium)、または Chrome のいずれかを使用します。
::: moniker-end
::: moniker range="vs-2017"
このシナリオでは、Chrome を使用します。
::: moniker-end

1. ターゲット ブラウザーのすべてのウィンドウを閉じます。

   そのブラウザーをデバッグを有効にした状態で開くことが、その他のブラウザー インスタンスによって妨げられる可能性があります (ブラウザーの拡張機能が実行され、フル デバッグ モードが阻止されている場合があります。そのため、タスク マネージャーを開き、Chrome の予期しないインスタンスを見つけることが必要な場合があります)。

   ::: moniker range=">=vs-2019"
   Microsoft Edge (Chromium) の場合は、Chrome のすべてのインスタンスもシャットダウンします。 どちらのブラウザーでも Chromium コード ベースが共有されているため、これによって最適な結果が得られます。
   ::: moniker-end

2. デバッグが有効な状態でブラウザーを起動します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 以降では、ブラウザーの起動時に `--remote-debugging-port=9222` フラグを設定することもできます。 **[デバッグ]** ツール バーから **[ブラウザーの選択]** を選択し、 **[追加]** を選択した後、 **[引数]** フィールドにフラグを設定します。 ブラウザーに **Microsoft Edge でのデバッグ** や **Chrome でのデバッグ** などの別のフレンドリ名を使用します。 詳細については、[リリース ノート](/visualstudio/releases/2019/release-notes-v16.2)を参照してください。

    ![ブラウザーをデバッグが有効な状態で開くように設定する](../javascript/media/tutorial-nodejs-react-edge-with-debugging.png)

    別の方法として、Windows の **[スタート]** ボタンから **[ファイル名を指定して実行]** コマンドを開き (右クリックして **[ファイル名を指定して実行]** を選択)、次のコマンドを入力します。

    `msedge --remote-debugging-port=9222`

    または、

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    ::: moniker range="vs-2017"
    Windows の **[スタート]** ボタンから **[ファイル名を指定して実行]** コマンドを開き (右クリックして **[ファイル名を指定して実行]** を選択)、次のコマンドを入力します。

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    これにより、デバッグが有効な状態でブラウザーが起動します。

    アプリはまだ実行されていないため、空のブラウザー ページが表示されます。

### <a name="attach-the-debugger-to-client-side-script"></a>クライアント側スクリプトにデバッガーをアタッチする

1. Visual Studio に切り替えて、ソース コード (*app-bundle.js* または *app.tsx* のいずれか) にブレークポイントを設定します。

    *app-bundle.js* の場合、次の図に示すように、`render()` 関数にブレークポイントを設定します。

    ![app-bundle.js に関する Visual Studio のコード ウィンドウのスクリーンショット。 左側の余白の赤い点は、render 関数にブレークポイントが設定されていることを示します。](../javascript/media/tutorial-nodejs-react-set-breakpoint-client-code.png)

    トランスパイルされた *app-bundle.js* ファイル内で `render()` 関数を見つけるには、**Ctrl**+**F** キーを使用します ( **[編集]**  >  **[検索と置換]**  >  **[クイック検索]** )。

    *app.tsx* では、`render()` 関数の内部で、`return` ステートメントにブレークポイントを設定します。

    ![app.tsx に関する Visual Studio のコード ウィンドウのスクリーンショット。 左側の余白の赤い点は、render 関数の return ステートメントにブレークポイントが設定されていることを示します。](../javascript/media/tutorial-nodejs-react-set-breakpoint-in-tsx-file.png)

2. *.tsx* ファイル (*app-bundle.js* ではなく) にブレークポイントを設定する場合は、*webpack-config.js* を更新する必要があります。 次のコードを

    ```javascript
    output: {
        filename: "./app-bundle.js",
    },
    ```

    を、次のコードで置換します。

    ```javascript
    output: {
        filename: "./app-bundle.js",
        devtoolModuleFilenameTemplate: '[resource-path]'  // removes the webpack:/// prefix
    },
    ```

    これは、Visual Studio でのデバッグを有効にするための開発専用の設定です。 この設定を使用すると、アプリをビルドするときに、ソース マップ ファイル *app-bundle.js* 内で生成された参照をオーバーライドできます。 既定では、ソース マップ ファイル内の webpack 参照には *webpack:///* プレフィックスが含まれています。これにより、Visual Studio でソース ファイル *app.tsx* を検索できなくなります。 具体的には、この変更を行うと、ソース ファイル *app.tsx* への参照が、*webpack:///./app.tsx* から *./app.tsx* に変更され、デバッグが有効になります。

3. Visual Studio でデバッグ ターゲットとして目的のブラウザーを選択し、次に **Ctrl**+**F5** キーを押して ( **[デバッグ]**  >  **[デバッグなしで開始]** )、ブラウザーでアプリを実行します。

    ::: moniker range=">=vs-2019"
    フレンドリ名を使用してブラウザー構成を作成した場合は、それをデバッグ ターゲットとして選択します。
    ::: moniker-end

    アプリがブラウザーの新しいタブで開きます。

4. **[デバッグ]**  >  **[プロセスにアタッチ]** を選択します (または **Ctrl** + **Alt** + **P** キーを押します)。

    > [!TIP]
    > Visual Studio 2017 以降では、これらの手順に従って初めてプロセスにアタッチした後は、 **[デバッグ]**  >  **[プロセスに再アタッチする]** を選択することで (または **Shift** + **Alt** + **P** キーを押して)、同じプロセスに簡単に再アタッチできます。

5. **[プロセスにアタッチ]** ダイアログ ボックスで、アタッチできるブラウザー インスタンスのフィルター処理された一覧を取得します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 では、 **[アタッチ先]** フィールドでターゲット ブラウザー用の適切なデバッガーとして **JavaScript (Chrome)** または **JavaScript (Microsoft Edge - Chromium)** を選び、フィルター ボックスに「**chrome**」または「**edge**」と入力して検索結果をフィルター処理します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 では、 **[アタッチ先]** フィールドで **[WebKit code]\(WebKit コード\)** を選び、フィルター ボックスに「**chrome**」と入力して検索結果をフィルター処理します。
    ::: moniker-end

6. 正しいホスト ポート (この例では localhost) のブラウザー プロセスを選び、 **[アタッチ]** を選択します。

    ポート (1337) も **[タイトル]** フィールドに表示され、適切なブラウザー インスタンスを選択するのに役立ちます。

    ::: moniker range=">=vs-2019"
    Microsoft Edge (Chromium) ブラウザーの場合の例を次に示します。

    ![プロセスにアタッチする](../javascript/media/tutorial-nodejs-react-attach-to-process-edge.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![プロセスにアタッチする](../javascript/media/tutorial-nodejs-react-attach-to-process.png)

    Visual Studio で DOM Explorer と JavaScript コンソールが開けば、デバッガーが正しくアタッチしたことがわかります。 これらのデバッグ ツールは、Chrome の開発者ツールや Microsoft Edge の F12 ツールに似ています。
    ::: moniker-end

    > [!TIP]
    > デバッガーがアタッチされず、「プロセスにアタッチできません。 現在の状態での操作は無効です" というメッセージが表示される場合、ターゲット ブラウザーをデバッグ モードで開始する前に、タスク マネージャーを使用してそのブラウザーのすべてのインスタンスを閉じます。 ブラウザーの拡張機能が実行され、フル デバッグ モードが阻止されている場合があります。

7. ブレークポイントを設定したコードは既に実行しているので、ブラウザーのページを更新してブレークポイントにヒットします。

    デバッガーで一時停止している間に、変数をマウスでポイントし、デバッガー ウィンドウを使って、アプリの状態を確認できます。 コードをステップ実行することにより (**F5**、**F10**、**F11**)、デバッガーを進めることができます。 基本的なデバッグ機能の詳細については、[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)に関するページを参照してください。

    前に実行した手順および使用している環境やブラウザーの状態に応じて、*app-bundle.js* 内またはそれにマップされた *app.tsx* 内で、ブレークポイントにヒットする可能性があります。 どちらの場合も、コードをステップ実行して、変数を確認できます

   * *app.tsx* のコードを中断する必要があるときにできない場合は、前の手順で説明したデバッガーをアタッチするための **[プロセスにアタッチ]** を使用します。 環境が正しく設定されていることを確認してください。

      * ブラウザーをデバッグ モードで実行できるように、Chrome 拡張機能を含むすべてのブラウザー インスタンスを (タスク マネージャーを使用して) 閉じます。 必ずブラウザーをデバッグ モードで起動します。

      * ソース マップ ファイルに *./app.tsx* への参照が含まれており、*webpack:///./app.tsx* が含まれていないことを確認します。そうでないと、Visual Studio デバッガーで *app.tsx* を検索できません。
       または、*app.tsx* 内のコードを中断する必要があるときに、それができない場合は、*app.tsx* で `debugger;` ステートメントを使うか、代わりに Chrome の開発者ツール (または Microsoft Edge の F12 ツール) でブレークポイントを設定してみてください。

   * *app-bundle.js* 内のコードを中断する必要があるときに、それができない場合は、ソース マップ ファイル *app-bundle.js.map* を削除します。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [アプリを Linux App Service にデプロイする](../javascript/publish-nodejs-app-azure.md)
