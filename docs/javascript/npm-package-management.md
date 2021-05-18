---
title: npm パッケージを管理する
description: Visual Studio では、Node.js パッケージ マネージャー (npm) を利用してパッケージを管理できます。
ms.custom: seodec18
ms.date: 02/23/2021
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 2fcf1bd9e9ef5c3ff0663cf12684e6e638d1e5e4
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729287"
---
# <a name="manage-npm-packages-in-visual-studio"></a>Visual Studio で npm パッケージを管理する

npm を利用すると、Node.js アプリケーションで使用するパッケージをインストールしたり、管理したりできます。 Visual Studio では、npm を操作したり、UI から、または直接 npm コマンドを実行したりすることが簡単にできます。 npm に不慣れで詳細が必要な場合、[npm ドキュメント](https://docs.npmjs.com/) ページにお進みください。

Visual Studio と npm の統合は、プロジェクトの種類によって異なります。
* [Node.js](#nodejs-projects)
* [ASP.NET Core](#aspnet-core-projects)
* [フォルダーを開く (Node.js)](../javascript/develop-javascript-code-without-solutions-projects.md)

> [!Important]
> npm では、プロジェクト ルートに *node_modules* フォルダーと *package.json* が必要です。 お使いのアプリのフォルダー構造が異なる場合、Visual Studio を使用して npm パッケージを管理するには、フォルダー構造を変更する必要があります。

## <a name="nodejs-projects"></a>Node.js プロジェクト

Node.js プロジェクトでは、次のタスクを実行できます。
* [ソリューション エクスプローラーからパッケージをインストールする](#npmInstallWindow)
* [ソリューション エクスプローラーからインストール済みのパッケージを管理する](#solutionExplorer)
* [Node.js 対話型ウィンドウで `.npm` コマンドを使用する](#interactive)

これらの機能は連動し、プロジェクト システムやプロジェクトの *package.json* ファイルによって同期します。

### <a name="prerequisites"></a>必須コンポーネント

プロジェクトに npm サポートを追加するには、**Node.js 開発** ワークロードと Node.js ランタイムがインストールされている必要があります。 詳細な手順については、[Node.js プロジェクトの作成](../ide/quickstart-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json)に関するページを参照してください。

> [!NOTE]
> 既存の Node.js プロジェクトの場合は、 **[既存の Node.js コードから]** というソリューション テンプレート、または [Open folder (Node.js)](../javascript/develop-javascript-code-without-solutions-projects.md) プロジェクト タイプを使用して、ご利用のプロジェクトの npm を有効にします。

### <a name="install-packages-from-solution-explorer-nodejs"></a><a name="npmInstallWindow"></a> ソリューション エクスプローラーからパッケージをインストールする (Node.js)

Node.js プロジェクトの場合、npm パッケージをインストールする最も簡単な方法は、npm パッケージ インストール ウィンドウを使用することです。 このウィンドウにアクセスするには、プロジェクトの **npm** ノードを右クリックし、 **[新しい npm パッケージのインストール]** を選択します。

:::image type="content" source="../javascript/media/solution-explorer-install-package.png" alt-text="ソリューション エクスプローラーから新しい npm パッケージをインストールする" border="true":::

このウィンドウでは、パッケージを検索し、オプションを指定し、インストールできます。

![[新しい npm パッケージのインストール] ダイアログのスクリーンショット。 azure 2.2.1-preview パッケージが選択され、そのパッケージの詳細とオプションが表示されています。](../javascript/media/search-package.png)

* **[依存関係の種類]** - **[Standard]** 、 **[Development]** 、 **[Optional]** からパッケージを選択します。 [Standard] の場合、パッケージはランタイム依存となります。[Development] の場合、パッケージは開発中にのみ必須となります。
* **package.json に追加** - 推奨。 この構成可能なオプションは非推奨とされます。
* **[選択したバージョン]** - インストールするパッケージのバージョンを選択します。
* **[他の npm 引数]** - 他の標準 npm 引数を指定します。 たとえば、`@~0.8` のようなバージョン値を入力し、バージョン リストでは利用できない特定のバージョンをインストールできます。

**[出力]** ウィンドウ (このウィンドウを開くには、 **[表示]**  >  **[出力]** を選択するか、**Ctrl**  +  **Alt**  +  **O** キーを押します) の **npm** 出力でインストールの進行状況を確認できます。 これには時間がかかる場合があります。

![npm 出力](../javascript/media/npm-output.png)

> [!TIP]
> 関心があるスコープを検索クエリの前に付加するとスコープ パッケージを検索できます。たとえば、mocha の TypeScript 定義ファイルを探すには「`@types/mocha`」と入力します。 また、TypeScript の型定義をインストールするとき、npm 引数フィールドに `@ts2.6` を追加すると、ターゲットの TypeScript バージョンを指定できます。

### <a name="manage-installed-packages-in-solution-explorer-nodejs"></a><a name="solutionExplorer"></a>ソリューション エクスプローラーでインストール済みのパッケージを管理する (Node.js)

npm パッケージはソリューション エクスプローラーに表示されます。 **npm** ノードの下にあるエントリは、*package.json* ファイルの依存関係を模倣します。

![npm パッケージのインストール状態を示すソリューション エクスプローラーの npm ノードのスクリーンショット。](../javascript/media/solution-explorer-status.png)

### <a name="package-status"></a>パッケージ ステータス

* ![インストール済みのパッケージ](../javascript/media/installed-npm.png) - インストールされ、package.json のリストに入っている
* ![無関係なパッケージ](../javascript/media/extraneous-npm.png) - インストールされているが、package.json のリストで明示されていない
* ![足りないパッケージ](../javascript/media/missing-npm.png) - インストールされていないが、package.json のリストに入っている

::: moniker range=">=vs-2019"
**npm** ノードを右クリックして、次のいずれかのアクションを行います。

* **新しい npm パッケージのインストール**: UI を開いて、新しいパッケージをインストールします。
* **npm パッケージのインストール**: npm インストール コマンドを実行して、*package.json* にリストされているすべてのパッケージをインストールします (`npm install` を実行します)。
* **npm パッケージを更新**: *package.json* に指定されたセマンティック バージョニング (SemVer) 範囲に従って、パッケージを最新バージョンに更新します。 (`npm update --save` を実行します)。 SemVer 範囲は、通常、"~" または "^" を使用して指定します。 詳細については、「[package.json パッケージの構成](../javascript/configure-packages-with-package-json.md)」を参照してください。

パッケージ ノードを右クリックして、次のいずれかのアクションを行います。

* **npm パッケージのインストール**: npm インストール コマンドを実行して、*package.json* にリストされているパッケージ バージョンをインストールします (`npm install` を実行します)。
* **npm パッケージを更新**: *package.json* に指定された SemVer 範囲に従って、パッケージを最新バージョンに更新します。 (`npm update --save` を実行します)。SemVer 範囲は、通常、"~" または "^" を使用して指定します。
* **npm パッケージのアンインストール**: パッケージをアンインストールし、*package.json* からそれを削除します (`npm uninstall --save` を実行します)。
::: moniker-end
::: moniker range="vs-2017"
パッケージ ノードまたは **npm** ノードを右クリックし、次のいずれかのアクションを行います。
* *package.json* のリストに入っている **足りないパッケージをインストールする**
* **npm パッケージ** を最新バージョンに更新する
* **パッケージをアンインストールし**、*package.json* から削除する
::: moniker-end

>[!NOTE]
> npm パッケージでの問題の解決方法については、[トラブルシューティング](#troubleshooting-npm-packages)に関するページを参照してください。

### <a name="use-the-npm-command-in-the-nodejs-interactive-window-nodejs"></a><a name="interactive"></a>Node.js 対話型ウィンドウで .npm コマンドを使用する (Node.js)

Node.js 対話型ウィンドウで `.npm` コマンドを使用して npm コマンドを実行することもできます。 このウィンドウを開くには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[Node.js 対話型ウィンドウを開く]** を選択します (または **Ctrl**  +  **K**、**N** キーを押します)。

このウィンドウで次のようなコマンドを使用してパッケージをインストールできます。

`.npm install azure@4.2.3`

 > [!Tip]
 > 既定では、npm はプロジェクトのホーム ディレクトリで実行されます。 ソリューションにプロジェクトが複数ある場合、プロジェクトの名前かパスを括弧で指定します。
 > `.npm [MyProjectNameOrPath] install azure@4.2.3`

 > [!Tip]
 > プロジェクトに package.json ファイルが含まれない場合、`.npm init -y` を使用し、新しい package.json ファイルを既定のエントリで作成します。

 ## <a name="aspnet-core-projects"></a>ASP.NET Core プロジェクト

ASP.NET Core プロジェクトなどのプロジェクトの場合は、プロジェクトで npm サポートを統合し、npm を使用してパッケージをインストールすることができます。
* [npm サポートをプロジェクトに追加する](#npmAdd)
* [package.json を使用してパッケージをインストールする](#npmInstallPackage)

>[!NOTE]
> ASP.NET Core プロジェクトでは、npm の代わりに[ライブラリ マネージャー](/aspnet/core/client-side/libman/?view=aspnetcore-3.1&preserve-view=true)または yarn を使用して、クライアント側の JavaScript ファイルと CSS ファイルをインストールすることもできます。

### <a name="add-npm-support-to-a-project-aspnet-core"></a><a name="npmAdd"></a> npm サポートをプロジェクトに追加する (ASP.NET Core)

プロジェクトに *package.json* ファイルがまだ含まれていない場合は、*package.json* ファイルをプロジェクトに追加することで、npm サポートを有効にすることができます。

1. Node.js がインストールされていない場合は、[Node.js](https://nodejs.org/en/download/) Web サイトから LTS バージョンをインストールして、外部のフレームワークおよびライブラリとの最善の互換性を確保することをお勧めします。

   npm には Node.js が必要です。

1. *package.json* ファイルを追加するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[追加]**  >  **[新しい項目]** を選択します (または **Ctrl**  +  **SHIFT**  +  **A** キーを押します)。 **[npm 構成ファイル]** を選択し、既定の名前を使用して、 **[追加]** をクリックします。

   ![package.json をプロジェクトに追加する](../javascript/media/npm-add-package-json.png)

   npm 構成ファイルのリストが表示されない場合は、Node.js 開発ツールがインストールされていません。 Visual Studio インストーラーを使用すれば、**Node.js 開発** ワークロードを追加できます。 次に、前の手順を繰り返します。

1. *package.json* の `dependencies` または `devDependencies` セクションに 1 つまたは複数の npm パッケージを含めます。 たとえば、ファイルに次の内容を追加できます。

   ```json
   "devDependencies": {
      "gulp": "4.0.2",
      "@types/jquery": "3.3.33"
   }
   ```

ファイルを保存すると、Visual Studio によってソリューション エクスプローラーの **[依存関係] / [npm]** ノードの下にパッケージが追加されます。 ノードが表示されない場合は、 **[package.json]** を右クリックし、 **[パッケージの復元]** を選択します。

>[!NOTE]
> シナリオによっては、インストールされている npm パッケージの正しい状態がソリューション エクスプローラーに表示されないことがあります。 詳細については、[トラブルシューティングのヒント](#troubleshooting-npm-packages)に関するページをご覧ください。

### <a name="install-packages-using-packagejson-aspnet-core"></a><a name="npmInstallPackage"></a>package.json を使用してパッケージをインストールする (ASP.NET Core)

npm が含まれているプロジェクトでは、`package.json` を使用して npm パッケージを構成できます。 ソリューション エクスプローラーで npm ノードを右クリックし、 **[Open package.json]\(package.json を開く\)** を選択します。

![npm ノードが選択されているソリューション エクスプローラーのスクリーンショット。 右クリックのコンテキスト メニューが開き、[package.json を開く] が選択されています。](../javascript/media/npm-add-package.png)

*package.json* の IntelliSense を使用すると、npm パッケージの特定のバージョンを選択できます。

:::image type="content" source="../javascript/media/npm-add-package-intellisense.png" alt-text="npm パッケージのバージョンを選択する" border="true":::

ファイルを保存すると、Visual Studio によってソリューション エクスプローラーの **[依存関係] / [npm]** ノードの下にパッケージが追加されます。 ノードが表示されない場合は、 **[package.json]** を右クリックし、 **[パッケージの復元]** を選択します。

パッケージをインストールするには数分かかる場合があります。 **[出力]** ウィンドウで **npm** 出力に切り替えて、パッケージのインストールの進捗状況を確認します。

![npm 出力](../javascript/media/npm-output.png)

## <a name="troubleshooting-npm-packages"></a>npm パッケージのトラブルシューティング

* Node.js がインストールされていない場合、npm には Node.js が必要です。[Node.js](https://nodejs.org/en/download/) Web サイトから LTS バージョンをインストールして、外部のフレームワークおよびライブラリとの最善の互換性を確保することをお勧めします。

* Node.js プロジェクトの場合は、npm サポート用に **Node.js 開発** ワークロードがインストールされている必要があります。

* シナリオによっては、[こちら](https://github.com/aspnet/Tooling/issues/479)に説明されている既知の問題が原因で、インストールされている npm パッケージの正しい状態がソリューション エクスプローラーに表示されないことがあります。 たとえば、パッケージのインストール時に、それがインストールされていないと表示される場合があります。 ほとんどの場合、この記事で先に説明したように、*package.json* を削除し、Visual Studio を再起動して、*package.json* ファイルを再度追加することで、ソリューション エクスプローラーを更新できます。 または、パッケージをインストールするとき、npm 出力ウィンドウを使用してインストールの状態を確認できます。

* 一部の ASP.NET Core シナリオでは、ソリューション エクスプローラーの npm ノードはプロジェクトのビルド後に表示されないことがあります。 ノードを再び表示するには、プロジェクト ノードを右クリックし、 **[プロジェクトのアンロード]** を選択します。 次に、プロジェクト ノードを右クリックし、 **[プロジェクトの再読み込み]** を選択します。

* アプリのビルド時または TypeScript コードのトランスパイル時にエラーが表示される場合は、エラーの原因として npm パッケージの非互換性が考えられるので確認してください。 エラー特定するには、この記事で前述したように、パッケージをインストールするときに npm 出力ウィンドウを確認してください。 たとえば、1 つまたは複数の npm パッケージ バージョンが非推奨となっていて、これが原因でエラーが発生する場合、エラーを修正するにはより新しいバージョンをインストールする必要があります。 *package.json* を使用した npm パッケージのバージョン管理に関する詳細は、「[package.json configuration](../javascript/configure-packages-with-package-json.md)」 (package.json の構成) を参照してください。
