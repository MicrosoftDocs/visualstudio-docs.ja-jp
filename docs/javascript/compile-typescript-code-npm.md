---
title: npm を使用した TypeScript コードのコンパイルとビルド
description: Node Package Manager (npm) を使用し、Visual Studio プロジェクトに Typescript サポートを追加する方法について説明します。
ms.date: 7/23/2020
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 96e5689c0108231be26ddf7d598227137f7bc1f7
ms.sourcegitcommit: ab5735d64a6ad7aecabf5d6df159888e3246bff5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2021
ms.locfileid: "111433780"
---
# <a name="compile-typescript-code-nodejs"></a>TypeScript コードのコンパイル (Node.js)

TypeScript SDK を使用して、プロジェクトに TypeScript サポートを追加することができます。これは Visual Studio インストーラーで既定で使用できます。または npm を使用します。 プロジェクトが Visual Studio 2019 で開発されている場合は、TypeScript npm パッケージを使用することをお勧めします。これにより、さまざまなプラットフォームや環境の間で移植性が向上します。

ASP.NET Core のプロジェクトでは、代わりに [NuGet パッケージ](../javascript/compile-typescript-code-nuget.md)を使用することをお勧めします。

## <a name="add-typescript-support-using-npm"></a>npm を使用して TypeScript サポートを追加する

[TypeScript npm パッケージ](https://www.npmjs.com/package/typescript)によって、TypeScript サポートを追加できます。 TypeScript 2.1 以降の npm パッケージがプロジェクトにインストールされているときは、対応するバージョンの TypeScript 言語サービスがエディターに読み込まれます。

1. [手順に従って](../ide/quickstart-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json) Node.js 開発ワークロードと Node.js ランタイムをインストールします。

   最も簡単な方法で Visual Studio と統合するために、Node.js TypeScript テンプレートのいずれかを使用してプロジェクトを作成します (空の Node.js Web アプリケーション テンプレートなど)。 それ以外の場合は、Visual Studio に含まれている Node.js JavaScript テンプレートを使用してここに記載されている手順に従うか、[[フォルダーを開く]](../javascript/develop-javascript-code-without-solutions-projects.md) プロジェクトを使用します。

1. プロジェクトにまだ含まれていない場合は、[TypeScript npm パッケージ](https://www.npmjs.com/package/typescript)をインストールします。

   ソリューション エクスプローラー (右側のペイン) から、プロジェクトのルートにある *package.json* を開きます。 一覧表示されるパッケージは、ソリューション エクスプローラーの npm ノードの下にあるパッケージと対応しています。 詳細については、[npm パッケージの管理](../javascript/npm-package-management.md)に関するページを参照してください。

   Node.js プロジェクトの場合は、コマンド ラインまたは IDE を使用して TypeScript npm パッケージをインストールできます。 IDE を使用してインストールするには、ソリューション エクスプローラーで npm ノードを右クリックして **[Install New npm package]\(新しい npm パッケージをインストールする\)** を選択し、「**TypeScript**」を検索して、パッケージをインストールします。

   **[出力]** ウィンドウの **[npm]** オプションをオンにして、パッケージのインストールの進行状況を確認します。 インストールされたパッケージは、ソリューション エクスプローラーの **npm** ノードの下に表示されます。

1. プロジェクトにまだ含まれていない場合は、プロジェクトのルートに *.tsconfig* ファイルを追加します。 ファイルを追加するには、プロジェクト ノードを右クリックし、 **[追加] > [新しい項目]** の順に選択します。 **[TypeScript JSON 構成ファイル]** を選択し、 **[追加]** をクリックします。

   Visual Studio によって *tsconfig.json* ファイルがプロジェクト ルートに追加されます。 このファイルを使用して、TypeScript コンパイラの[オプションを構成](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)することができます。

1. *tsconfig.json* を開き、更新して必要なコンパイラ オプションを設定します。

   シンプルな *tsconfig.json* ファイルの例を次に示します。

   ```json
   {
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "dist"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   この例では、次のように記述されています。
   - *include* によって、TypeScript (*.ts) ファイルを検索する場所をコンパイラに指示します。
   - *outDir* オプションを使用して、TypeScript コンパイラによってトランスパイルされるプレーンな JavaScript ファイルの出力フォルダーを指定します。
   - *sourceMap* オプションによって、コンパイラが *sourceMap* ファイルを生成するかどうかを指定します。

   前述の構成では、TypeScript の構成に関する基本事項のみが説明されています。 他のオプションについては、「[tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)」を参照してください。

## <a name="build-the-application"></a>アプリケーションのビルド

1. TypeScript ( *.ts*) ファイルまたは TypeScript JSX ( *.tsx*) ファイルをプロジェクトに追加してから、TypeScript コードを追加します。 TypeScript のシンプルな例として、次をお使いください。

   ```typescript
   let message: string = 'Hello World';
   console.log(message);
   ```

1. *package.json* に、次のスクリプトを使用して Visual Studio の build コマンドと clean コマンドのサポートを追加します。

   ```json
   "scripts": {
     "build": "tsc --build",
     "clean": "tsc --build --clean"
   },
   ```

   webpack などのサード パーティ製ツールを使用してビルドする必要がある場合は、*package.json* ファイルにコマンド ライン ビルド スクリプトを追加できます。

   ```json
   "scripts": {
      "build": "webpack-cli app.tsx --config webpack-config.js"
   }
   ```

   React での webpack と webpack 構成ファイルの使用例については、[Node.js と React を使用した Web アプリの作成](../javascript/tutorial-nodejs-with-react-and-jsx.md)に関する記事をご覧ください。

   TypeScript での Vue.js の使用例については、[Vue.js アプリケーションの作成](/javascript/create-application-with-vuejs)に関する記事をご覧ください。

1. スタートアップ ページ、Node.js ランタイムへのパス、アプリケーション ポート、またはランタイム引数などのオプションを構成する必要がある場合は、ソリューション エクスプローラーでプロジェクト ノードを右クリックし、 **[プロパティ]** を選択します。

   >[!NOTE]
   > サード パーティ製ツールを構成する場合、 **[ツール]**  >  **[オプション]**  >  **[プロジェクトおよびソリューション]**  >  **[Web パッケージ管理]**  >  **[外部 Web ツール]** で構成したパスは、Node.js プロジェクトで使用されません。 これらの設定は、他のプロジェクトの種類で使用されます。

1. **[ビルド] > [ソリューションのビルド]** の順に選択します。

   アプリは実行時に自動的にビルドされますが、ここではビルド処理中に何が起きるのかを確認します。

   ソース マップを生成した場合は、*outDir* オプションで指定したフォルダーを開くと、生成された \*.js ファイルと生成された \*js.map ファイルが見つかります。

   ソース マップ ファイルは[デバッグ](../javascript/debug-nodejs.md)で必要となります。

### <a name="run-the-application"></a>アプリケーションの実行

アプリをコンパイルした後に実行する手順については、[初めての Node.js アプリの作成](../ide/quickstart-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json#run-the-app)に関するページを参照してください。

## <a name="automate-build-tasks"></a>ビルド タスクの自動化

Visual Studio のタスク ランナー エクスプローラーを使用して、npm や webpack などのサード パーティ製ツールのタスクを自動化することができます。

- [NPM タスク ランナー](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.NPMTaskRunner) - *package.json* で定義されている npm スクリプトのサポートを追加します。 yarn がサポートされています。
- [webpack タスク ランナー](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebPackTaskRunner) - webpack のサポートを追加します。
