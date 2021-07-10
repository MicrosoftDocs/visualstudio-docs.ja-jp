---
title: TypeScript を使用した ASP.NET Core アプリの作成
description: このチュートリアルでは、ASP.NET Core と TypeScript を使用してアプリを作成します。
ms.date: 03/25/2021
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 0728011c05d47996a313c11a18f31a196ec08e10
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306500"
---
# <a name="tutorial-create-an-aspnet-core-app-with-typescript-in-visual-studio"></a>チュートリアル: Visual Studio での TypeScript を使用した ASP.NET Core アプリの作成

ASP.NET Core と TypeScript を使用した Visual Studio での開発に関するこのチュートリアルでは、単純な Web アプリケーションを作成し、いくつかの TypeScript コードを追加して、アプリを実行します。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2022"

Visual Studio 2022 プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

このチュートリアルでは、次の作業を行う方法について説明します。
> [!div class="checklist"]
> * ASP.NET Core プロジェクトを作成する
> * TypeScript をサポートするための NuGet パッケージを追加する
> * いくつかの TypeScript コードを追加する
> * アプリを実行する
> * npm を使用してサード パーティのライブラリを追加する

## <a name="prerequisites"></a>必須コンポーネント

* Visual Studio をインストールし、ASP.NET Web 開発ワークロードを用意する必要があります。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end

    Visual Studio は既にあり、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動すると、Visual Studio インストーラーが開きます。 **[ASP.NET と Web 開発]** ワークロードを選択してから **[変更]** を選択します。

## <a name="create-a-new-aspnet-core-mvc-project"></a>新しい ASP.NET Core MVC プロジェクトを作成する

Visual Studio では、*プロジェクト* の 1 つのアプリケーションに対してファイルが管理されます。 プロジェクトには、ソース コード、リソース、構成ファイルが含まれています。

>[!NOTE]
> 空の ASP.NET Core プロジェクトから開始して、TypeScript フロントエンドを追加するには、代わりに [TypeScript を使用した ASP.NET Core](https://www.typescriptlang.org/docs/handbook/asp-net-core.html) に関するページを参照してください。

このチュートリアルでは、ASP.NET Core MVC アプリのコードを含む簡単なプロジェクトから開始します。

1. Visual Studio を開きます。

1. 新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で、スタート ウィンドウの **[新しいプロジェクトの作成]** を選択します。 スタート ウィンドウが開いていない場合は、 **[ファイル]**  >  **[スタート ウィンドウ]** を選択します。 「**Web アプリ**」と入力し、言語として **C#** を選択します。次に、 **[ASP.NET Core Web Application (Model-View-Controller)]\(ASP.NET Core Web アプリケーション (Model-View-Controller)\)** を選択し、 **[次へ]** を選択します。 次の画面で、プロジェクトの名前を指定し、 **[次へ]** を選択します。

    推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで **[Visual C#]** を展開し、 **[.NET Core]** を選択します。 中央のウィンドウで、 **[ASP.NET Core Web アプリケーション - C#]** を選択してから **[OK]** を選択します。

    表示されたダイアログ ボックスで **[Web アプリケーション (モデル ビュー コントローラー)]** を選択し、 **[作成]** (または **[OK]** ) を選択します。

    ![MVC テンプレートを選択する](../javascript/media/aspnet-core-ts-mvc-template.png)
    ::: moniker-end
    **ASP.NET Core Web アプリケーション** プロジェクト テンプレートが表示されない場合は、**ASP.NET と Web 開発** ワークロードを追加する必要があります。 手順について詳しくは、「[必須コンポーネント](#prerequisites)」をご覧ください。

    Visual Studio は新しいソリューションを作成し、右のウィンドウでプロジェクトを開きます。

## <a name="add-some-code"></a>何らかのコードを追加する

1. ソリューション エクスプローラー (右ウィンドウ) で、 プロジェクト ノードを右クリックして **[NuGet パッケージの管理]** を選択します。 **[参照]** タブで **[Microsoft.TypeScript.MSBuild]** を検索し、右側にある **[インストール]** をクリックしてパッケージをインストールします。

   ![NuGet パッケージを追加する](../javascript/media/aspnet-core-ts-nuget.png)

   Visual Studio によってソリューション エクスプローラーの **[依存関係]** ノードの下に NuGet パッケージが追加されます。

1. プロジェクト ノードを右クリックし、 **[追加] > [新しいアイテム]** の順に選択します。 **[TypeScript JSON 構成ファイル]** を選択し、 **[追加]** をクリックします。

   Visual Studio によって *tsconfig.json* ファイルがプロジェクト ルートに追加されます。 このファイルを使用して、TypeScript コンパイラの[オプションを構成](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)することができます。

1. *tsconfig.json* を開き、既定のコードを次のコードに置き換えます。

   ```json
   {
     "compileOnSave": true,
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "wwwroot/js"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   *outDir* オプションでは、TypeScript コンパイラによってトランスパイルされるプラン JavaScript ファイルの出力フォルダーを指定します。

   この構成により、TypeScript の使用に関する基本的な手順が指定されます。 たとえば [gulp や webpack](https://www.typescriptlang.org/docs/handbook/asp-net-core.html) を使用する場合などのその他のシナリオでは、使用するツールと構成設定に応じて、トランスパイルされる JavaScript ファイル用に *wwwroot/js* 以外の別の中間の場所を指定することができます。

1. ソリューション エクスプローラーで、プロジェクト ノードを右クリックして **[追加] > [新しいフォルダー]** の順に選択します。 新しいフォルダーの名前は「*scripts*」とします。

1. *scripts* フォルダーを右クリックし、 **[追加] > [新しいアイテム]** の順に選択します。 **[TypeScript ファイル]** を選択し、ファイル名として「*app.ts*」を入力して、 **[追加]** をクリックします。

   Visual Studio によって *app.ts* ファイルが *scripts* フォルダーに追加されます。

1. *app.ts* を開き、次の TypeScript コードを追加します。

    ```ts
    function TSButton() {
       let name: string = "Fred";
       document.getElementById("ts-example").innerHTML = greeter(user);
    }

    class Student {
       fullName: string;
       constructor(public firstName: string, public middleInitial: string, public lastName: string) {
           this.fullName = firstName + " " + middleInitial + " " + lastName;
       }
    }

    interface Person {
       firstName: string;
       lastName: string;
    }

    function greeter(person: Person) {
       return "Hello, " + person.firstName + " " + person.lastName;
    }

    let user = new Student("Fred", "M.", "Smith");
    ```

    Visual Studio では、TypeScript コードに関して IntelliSense サポートが提供されています。

    これをテストするには、`greeter` 関数から `.lastName` を削除し、「.」と再入力すると、IntelliSense が表示されます。

    ![IntelliSense を表示する](../javascript/media/aspnet-core-ts-intellisense.png)

    `lastName` を選択して、名前をコードにもう一度追加します。

1. *Views/Home* フォルダーを開き、*Index.cshtml* を開きます。

1. ファイルの末尾に次の HTML コードを追加します。

    ```html
    <div id="ts-example">
        <br />
        <button type="button" class="btn btn-primary btn-md" onclick="TSButton()">
            Click Me
        </button>
    </div>
    ```

1. *Views/Shared* フォルダーを開き、 *_Layout.cshtml* を開きます。

1. `@RenderSection("Scripts", required: false)` の呼び出しの前に次のスクリプト参照を追加します。

    ```js
    <script src="~/js/app.js"></script>
    ````

## <a name="build-the-application"></a>アプリケーションのビルド

1. **[ビルド] > [ソリューションのビルド]** の順に選択します。

   アプリは実行時に自動的にビルドされますが、ここではビルド処理中に何が起きるのかを確認します。

1. *wwwroot/js* フォルダーを開くと、2 つの新しいファイルが見つかります。*app.js*、およびソース マップ ファイルの *app.js.map* です。 これらのファイルは TypeScript コンパイラによって生成されます。

   ソース マップ ファイルはデバッグで必要となります。

## <a name="run-the-application"></a>アプリケーションの実行

1. **F5** キー ( **[デバッグ]**  >  **[デバッグの開始]** ) を押してアプリケーションを実行します。

    アプリがブラウザーで開きます。

    ブラウザー ウィンドウに **[ようこそ]** 見出しと **[クリックしてください]** ボタンが表示されます。

    ![TypeScript を使用した ASP.NET Core](../javascript/media/aspnet-core-ts-running-app.png)

1. ボタンをクリックすると、TypeScript ファイルに指定したメッセージが表示されます。

## <a name="debug-the-application"></a>アプリケーションのデバッグ

1. コード エディターの左余白をクリックして、`app.ts` 内の `greeter` 関数にブレークポイントを設定します。

    ![ブレークポイントの設定](../javascript/media/aspnet-core-ts-set-breakpoint.png)

1. **F5** キーを押してアプリケーションを実行します。

   スクリプトのデバッグを有効にするには、メッセージへの応答が必要な場合があります。

   アプリケーションはブレークポイントで一時停止します。 これで、変数を検査し、デバッガーの機能を使用できるようになりました。

## <a name="add-typescript-support-for-a-third-party-library"></a>サード パーティのライブラリ用の TypeScript サポートを追加する

1. [npm パッケージの管理](../javascript/npm-package-management.md#aspnet-core-projects)の指示に従って、プロジェクトに `package.json` ファイルを追加します。 これにより、npm サポートがプロジェクトに追加されます。

   >[!NOTE]
   > ASP.NET Core プロジェクトでは、npm の代わりに[ライブラリ マネージャー](/aspnet/core/client-side/libman/)または yarn を使用して、クライアント側の JavaScript ファイルと CSS ファイルをインストールすることもできます。

1. この例では、jQuery 用の TypeScript 定義ファイルをプロジェクトに追加します。 *package.json* ファイルに次の内容を含めます。

   ```json
   "devDependencies": {
      "@types/jquery": "3.3.33"
   }
   ```

   これにより、jQuery に対する TypeScript サポートが追加されます。 jQuery ライブラリ自体は、既に MVC プロジェクト テンプレートに含まれています (ソリューション エクスプローラーの wwwroot/lib の下を参照)。 別のテンプレートを使用している場合は、jquery npm パッケージも含める必要がある可能性があります。

1. ソリューション エクスプローラーのパッケージがインストールされていない場合は、npm ノードを右クリックし、 **[パッケージの復元]** を選択します。

   >[!NOTE]
   > 場合によっては、ソリューション エクスプローラーで、npm パッケージが *package.json* と同期されていないことが示される可能性があります。これは、[ここ](https://github.com/aspnet/Tooling/issues/479)で説明されている既知の問題のためです。 たとえば、パッケージのインストール時に、それがインストールされていないと表示される場合があります。 ほとんどの場合、この記事で先に説明したように、*package.json* を削除し、Visual Studio を再起動して、*package.json* ファイルを再度追加することで、ソリューション エクスプローラーを更新できます。

1. ソリューション エクスプローラーで、スクリプト フォルダーを右クリックし、 **[追加]**  >  **[新しい項目]** を選択します。

1. **[TypeScript ファイル]** を選択し、「*library.ts*」と入力して、 **[追加]** を選択します。

1. *library.ts* で、次のコードを追加します。

   ```ts
   var jqtest = {
      showMsg: function (): void {
         let v: any = jQuery.fn.jquery.toString();
         let content: any = $("#ts-example-2")[0].innerHTML;
         alert(content.toString() + " " + v + "!!");
         $("#ts-example-2")[0].innerHTML = content + " " + v + "!!";
      }
   };

   jqtest.showMsg();
   ```

   わかりやすくするために、このコードでは jQuery と alert を使用してメッセージを表示します。

   追加された jQuery の TypeScript 型の定義では、次に示すように、jQuery オブジェクトの後に "." を入力すると、jQuery オブジェクトで IntelliSense サポートを取得します。

   ![jQuery の IntelliSense](../javascript/media/aspnet-core-ts-jquery-intellisense.png)

1. _Layout.cshtml で、`library.js` を含めるようにスクリプト参照を更新します。

   ```html
   <script src="~/js/app.js"></script>
   <script src="~/js/library.js"></script>
   ```

1. Index.cshtml で、ファイルの末尾に次の HTML を追加します。

   ```html
   <div>
      <p id="ts-example-2">jQuery version is:</p>
   </div>
   ```

1. **F5** キー ( **[デバッグ]**  >  **[デバッグの開始]** ) を押してアプリケーションを実行します。

    アプリがブラウザーで開きます。

    アラートで **[OK]** をクリックすると、ページが更新され "**jQuery バージョン: 3.3.1!!** " と表示されます。

    ![jquery の例](../javascript/media/aspnet-core-ts-jquery-example.png)

## <a name="next-steps"></a>次の手順

ASP.NET Core で TypeScript を使用する方法の詳細については、こちらを参照してください。 Visual Studio での AngularJS プログラミングに関心がある場合は、Visual Studio の [AngularJS Language Service 拡張機能](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)を使用できます。

> [!div class="nextstepaction"]
> [ASP.NET Core と TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)

> [!div class="nextstepaction"]
> [AngularJS Language Service 拡張機能](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)
