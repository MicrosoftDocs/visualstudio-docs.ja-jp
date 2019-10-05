---
title: Docker Compose と ASP.NET Core を使用した複数コンテナーのチュートリアル
author: ghogen
description: Docker Compose を使用して複数のコンテナーを使用する方法について説明します
ms.author: ghogen
ms.date: 02/21/2019
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: ce6e98e2d068cd569247c4c4ea869c4280101d47
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "71126089"
---
# <a name="tutorial-create-a-multi-container-app-with-docker-compose"></a>チュートリアル: Docker Compose を使用して複数コンテナーのアプリを作成する

このチュートリアルでは、Visual Studio でコンテナー ツールを使用しているときに、複数のコンテナーを管理し、それらの間で通信を行う方法について学習します。  複数のコンテナーを管理するには、"*コンテナー オーケストレーション*" が必要であり、Docker Compose、Kubernetes、Service Fabric などのオーケストレーターが必要です。 ここでは、Docker Compose を使用します。 Docker Compose は、開発サイクル中での、ローカルのデバッグとテストに適しています。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure ツール** ワークロード、または **.NET Core クロスプラットフォーム開発**ワークロードがインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
::: moniker-end

::: moniker range=">= vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、および/または **.NET Core クロスプラットフォーム開発**ワークロードがインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
* .NET Core 2.2 を使って開発するための [.NET Core 2.2 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/2.2)
::: moniker-end

## <a name="create-a-web-application-project"></a>Web アプリケーション プロジェクトを作成する

Visual Studio で、**ASP.NET Core Web アプリケーション** プロジェクトを `WebFrontEnd` という名前で作成します。 **[Web アプリケーション]** を選択し、Razor Pages を使用して Web アプリケーションを作成します。 
  
::: moniker range="vs-2017"

**[Docker サポートを有効にする]** を選択しないでください。 Docker サポートは、後で追加します。

![Web プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/docker-tutorial-enable-docker-support.png)

::: moniker-end

::: moniker range="vs-2019"

![Web プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/vs-2019/new-aspnet-core-project1.png)

**[Docker サポートを有効にする]** を選択しないでください。 Docker サポートは、後で追加します。

![Web プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/vs-2019/new-aspnet-core-project.png)

::: moniker-end

## <a name="create-a-web-api-project"></a>Web API プロジェクトを作成する

同じソリューションにプロジェクトを追加し、*MyWebAPI* という名前を付けます。 プロジェクト タイプとして **API** を選択し、 **[HTTPS 用の構成]** チェックボックスをオフにします。 この設計では、同じ Web アプリケーション内のコンテナー間の通信ではなく、クライアントとの通信にのみ SSL を使用します。 `WebFrontEnd` のみが HTTPS を必要とします。

::: moniker range="vs-2017"
   ![Web API プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/docker-tutorial-mywebapi.png)
::: moniker-end
::: moniker range="vs-2019"
   ![Web API プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/vs-2019/web-api-project.png)
::: moniker-end

## <a name="add-code-to-call-the-web-api"></a>コードを追加して Web API を呼び出す

1. `WebFrontEnd` プロジェクトで、*Index.cshtml.cs* ファイルを開き、`OnGet` メソッドを次のコードに置き換えます。

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          request.RequestUri = new Uri("http://mywebapi/api/values/1");
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```

1. *Index.cshtml* ファイルで、`ViewData["Message"]` を表示する行を追加し、ファイルを次のコードのようにします。
    
      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }
    
      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="https://docs.microsoft.com/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. 次に、Web API プロジェクトで、Values コントローラーにコードを追加し、*webfrontend* から追加した呼び出しに対して API によって返されるメッセージをカスタマイズします。
    
      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

1. `WebFrontEnd` プロジェクトで、 **[追加] > [コンテナー オーケストレーター サポート]** の順に選択します。 **[Docker サポート オプション]** ダイアログが表示されます。

1. **[Docker Compose]** を選択します。

1. Linux などのターゲット OS を選択します。

   ![ターゲット OS 選択のスクリーンショット](media/tutorial-multicontainer/docker-tutorial-docker-support-options.PNG)

   Visual Studio では、*docker-compose.yml* ファイルと *.dockerignore* ファイルが、ソリューション内の **docker-compose** ノードで作成されます。そのプロジェクトは、スタートアップ プロジェクトであることを示す太字のフォントで表示されます。

   ![ソリューション エクスプローラーと、追加された docker-compose プロジェクトのスクリーンショット](media/tutorial-multicontainer/multicontainer-solution-explorer.png)

   *docker-compose.yml* は、次のように表示されます。

   ```yaml
   version: '3.4'

    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
   ```

   *.dockerignore* ファイルには、Docker によってコンテナーに含める必要のないファイルの種類と拡張機能が含まれます。 これらのファイルは、開発中のアプリまたはサービスの一部ではなく、一般的に、開発環境やソース管理に関連付けられるものです。

   実行中のコマンドの詳細については、[出力] ウィンドウの **[コンテナー ツール]** セクションを参照してください。  コマンドライン ツールの docker-compose が、ランタイム コンテナーの構成や作成に使用されているのが確認できます。

1. Web API プロジェクトで、プロジェクト ノードを再度右クリックして、 **[追加]**  >  **[コンテナー オーケストレーター サポート]** の順に選択します。 **[Docker Compose]** を選択し、同じターゲット OS を選択します。  

    > [!NOTE]
    > この手順では、Visual Studio によって Dockerfile が作成されます。 既に Docker サポートがあるプロジェクトでこれを行う場合は、既存の Dockerfile を上書きするかどうかを確認するメッセージが表示されます。 保持する Dockerfile に変更を加えた場合は、[いいえ] を選択します。

    Visual Studio によって、docker compose YML ファイルにいくつかの変更が加えられます。 これで、両方のサービスが含まれることになります。

    ```yaml
    version: '3.4'
    
    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
    
      mywebapi:
        image: ${DOCKER_REGISTRY-}mywebapi
        build:
          context: .
          dockerfile: MyWebAPI/Dockerfile
    ```

1. サイトをローカルで実行して (F5 キーまたは Ctrl + F5 キー)、想定どおりに動作することを確認します。 すべてが正しく構成されている場合、"Hello from webfrontend and webapi (with value 1)" というメッセージが表示されます。

   コンテナー オーケストレーションを追加するときに使用する最初のプロジェクトは、実行またはデバッグの際に起動されるように設定されます。 docker-compose プロジェクトの **[プロジェクトのプロパティ]** で、起動アクションを構成できます。  docker-compose プロジェクト ノードで、右クリックしてコンテキスト メニューを開き、 **[プロパティ]** を選択するか、Alt + Enter キーを押します。  次のスクリーンショットは、ここで使用するソリューションに必要なプロパティを示しています。  たとえば、 **[サービス URL]** プロパティをカスタマイズすることで読み込まれるページを変更できます。

   ![docker-compose プロジェクト プロパティのスクリーンショット](media/tutorial-multicontainer/launch-action.png)

   起動すると、このように表示されます。

   ![実行中の Web アプリのスクリーンショット](media/tutorial-multicontainer/webfrontend.png)

## <a name="next-steps"></a>次の手順

[Azure にコンテナー](/azure/containers)をデプロイするためのオプションを確認します。

## <a name="see-also"></a>関連項目
  
[Docker Compose](https://docs.docker.com/compose/)  
[コンテナー ツール](/visualstudio/containers/)
