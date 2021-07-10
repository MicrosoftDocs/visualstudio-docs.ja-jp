---
title: 最初の Node.js アプリを作成する
ms.custom:
- vs-acquisition
- SEO-VS-2020
description: このクイック スタートでは、Visual Studio で Node.js アプリを作成します
ms.date: 03/25/2021
ms.technology: vs-javascript
ms.topic: quickstart
ms.devlang: javascript
ms.assetid: b0e4ebed-1a01-41ef-aad1-4d8465ce5322
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 0c44bfcfe1e7f07f83ca2b7dbb8b0604f5efe5f1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386164"
---
# <a name="quickstart-create-your-first-nodejs-app-with-visual-studio"></a>クイックスタート: Visual Studio を使用して最初の Node.js アプリを作成する

ここでは 5 分から 10 分で Visual Studio 統合開発環境 (IDE) の概要を示し、単純な Node.js Web アプリを作成します。

## <a name="prerequisites"></a>前提条件

始める前に、Visual Studio をインストールし、Node.js 環境を設定します。

### <a name="install-visual-studio"></a>Visual Studio のインストール

::: moniker range=">=vs-2019"
Visual Studio 2019 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2017 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。
::: moniker-end

### <a name="set-up-your-nodejs-environment"></a>Node.js 環境を設定する

Visual Studio は、Node.js 開発に一般的なツールのインストールなど、環境の設定に役立ちます。

1. Visual Studio で **[ツール]**  >  **[ツールと機能を取得]** に移動します。

1. Visual Studio インストーラーで **[Node.js 開発]** ワークロードを選択し、 **[変更]** を選択し、ワークロードをダウンロードしてインストールします。

    ![Visual Studio インストーラーの Node.js ワークロード](../ide/media/quickstart-nodejs-workload.png)

1. [Node.js ランタイム](https://nodejs.org/en/download/)の LTS バージョンをインストールします。 外部のフレームワークとライブラリとの互換性を最大限に高めるために、LTS バージョンをお勧めします。

    Node.js は 32 ビットと 64 ビットのアーキテクチャ用に構築されていますが、Node.js インストーラーは、インストールされたバージョンのうち一度に 1 つのみをサポートします。

1. インストールされたランタイムが Visual Studio によって検出されない場合 (通常はされます)、インストールされたランタイムを参照するようにプロジェクトを構成します。

   1. [プロジェクトを作成](#create-your-app-project)した後、プロジェクト ノードを右クリックします。

   1. **[プロパティ]** を選択し、 **[node.exe のパス]** を設定します。 Node.js のグローバル インストールを使用するか、または Node.js プロジェクトごとにローカル インタープリターへのパスを指定することができます。

## <a name="create-your-app-project"></a>アプリのプロジェクトを作成する

1. [Node.js ランタイム](https://nodejs.org/en/download/)の LTS バージョンをまだインストールしていない場合はインストールします。 詳細については、[前提条件](#prerequisites)を参照してください。

1. Visual Studio を開きます。

1. 新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"

    1. **Esc** キーを押してスタート ウィンドウを閉じます。

    1. **Ctrl + Q** キーを押して検索ボックスを開き、「**Node.js**」と入力します。

    1. **[空の Node.js Web アプリケーション (JavaScript)]** を選択します。 ダイアログで **[作成]** を選択します。

    ::: moniker-end

    ::: moniker range="vs-2017"
    1. 上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

    1. **[新しいプロジェクト]** ダイアログの左側のペインで、 **[JavaScript]** を展開して、 **[Node.js]** を選択します。

    1. 中央のペインで、 **[空白の Node.js Web アプリケーション]** を選択し、 **[OK]** を選択します。

    ::: moniker-end
    
    **[空白の Node.js Web アプリケーション]** プロジェクト テンプレートが表示されない場合は、**Node.js 開発** ワークロードを追加する必要があります。 詳細な手順については、「[必須コンポーネント](#prerequisites)」を参照してください。

    Visual Studio によってプロジェクトが作成され、開かれます。 プロジェクトの *server.js* ファイルが左のエディターで開かれます。

## <a name="explore-the-ide"></a>IDE を探索する

1. 右側のペインにある **ソリューション エクスプローラー** を確認します。

   ![ソリューション エクスプローラー](../ide/media/quickstart-nodejs-solution-explorer.png)

   - 太字で強調表示されているのが作成したプロジェクトです。プロジェクトを設定したときに指定した名前が使われています。 ディスク上では、このプロジェクトは、プロジェクト フォルダーの *.njsproj* ファイルに該当します。

   - 最上位レベルにあるのは、ソリューションです。既定では、名前はプロジェクトと同じです。 ディスク上の *.sln* ファイルで表されるソリューションは、1 つ以上の関連プロジェクトのコンテナーです。

   - **npm** ノードには、インストールされている npm パッケージが表示されます。 npm ノードを右クリックし、ダイアログを使用して npm パッケージを検索し、インストールすることができます。

1. コマンド プロンプトから npm パッケージまたは Node.js コマンドをインストールする場合は、プロジェクト ノードを右クリックし、 **[ここでコマンド プロンプトを開く]** を選択します。

   ![Node.js のコマンド プロンプト](../ide/media/quickstart-nodejs-command-prompt.png)

1. ソース コードへのナビゲーションをテストする場合は、開いている *server.js* ファイルから **http.createServer** を選択して **F12** キーを押すか、コンテキスト (右クリック) メニューから **[定義に移動]** を選択します。 このコマンドで *http.d.ts* の `createServer` 関数の定義が示されます。

   ![[定義に移動] コンテキスト メニュー](../ide/media/quickstart-nodejs-gotodefinition.png)

1. *server.js* に戻り、次のコード行を見つけます: `res.end('Hello World\n');`。 このコードを次のように修正します。

    `res.end('Hello World\n' + res.connection.`

    「**connection.** 」と入力すると、IntelliSense によってコード入力をオートコンプリートするオプションが表示されます。

   ![IntelliSense のオートコンプリート](../ide/media/quickstart-nodejs-intellisense.png)

1. **localPort** を選択し、「 **);** 」と入力してステートメントを完成させます。

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-app"></a>アプリを実行する

1. **Ctrl + F5** キーを押し (または **[デバッグ]**  >  **[デバッグなしで開始]** を選択し)、アプリを実行します。 
 
   アプリがブラウザーで開きます。

1. ブラウザーで "Hello World" のメッセージとローカルのポート番号が表示されることを確認します。

おめでとうございます。 Visual Studio を使用してシンプルな Node.js アプリを作成しました。 詳細を確認するには、目次の「**チュートリアル**」セクションに進んでください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリを Linux App Service にデプロイする](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [Node.js と Express のチュートリアル](../javascript/tutorial-nodejs.md)

> [!div class="nextstepaction"]
> [Node.js と React のチュートリアル](../javascript/tutorial-nodejs-with-react-and-jsx.md)
