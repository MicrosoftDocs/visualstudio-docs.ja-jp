---
title: Docker Compose を使用して複数のコンテナーを使用する
author: ghogen
description: Docker Compose を使用して複数のコンテナーを使用する方法について説明します
ms.custom: SEO-VS-2020
ms.author: ghogen
ms.date: 03/15/2021
ms.technology: vs-azure
ms.topic: tutorial
ms.openlocfilehash: 78af96eaa8f340129b2b445dd92419f84cf91ab1
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307818"
---
# <a name="tutorial-create-a-multi-container-app-with-docker-compose"></a>チュートリアル: Docker Compose を使用して複数コンテナーのアプリを作成する

このチュートリアルでは、Visual Studio でコンテナー ツールを使用しているときに、複数のコンテナーを管理し、それらの間で通信を行う方法について学習します。  複数のコンテナーを管理するには、"*コンテナー オーケストレーション*" が必要であり、Docker Compose、Kubernetes、Service Fabric などのオーケストレーターが必要です。 ここでは、Docker Compose を使用します。 Docker Compose は、開発サイクル中での、ローカルのデバッグとテストに適しています。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range="vs-2017"

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure ツール** ワークロード、または **.NET Core クロスプラットフォーム開発** ワークロードがインストールされた [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
::: moniker-end

::: moniker range="vs-2019"

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、および/または **.NET Core クロスプラットフォーム開発** ワークロードがインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
* .NET Core 2.2 を使って開発するための [.NET Core 2.2 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/2.2)
* .NET Core 3.1 を使って開発するための [.NET Core 3 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/3.1)。
::: moniker-end

::: moniker range=">=vs-2022"

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、および/または **.NET Core クロスプラットフォーム開発** ワークロードがインストールされた [Visual Studio 2022 プレビュー](https://visualstudio.microsoft.com/vs/preview/vs2022)
* .NET Core 3.1 を使って開発するための [.NET Core 3 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/3.1)。
* .NET 5 で開発するための [.NET 5 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/5.0)。
::: moniker-end

## <a name="create-a-web-application-project"></a>Web アプリケーション プロジェクトを作成する

Visual Studio で、`WebFrontEnd` という名前の **[ASP.NET Core Web アプリ]** プロジェクトを作成し、Razor Pages を使用した Web アプリケーションを作成します。
  
::: moniker range="vs-2017"

**[Docker サポートを有効にする]** を選択しないでください。 Docker サポートは、後で追加します。

![Web プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/docker-tutorial-enable-docker-support.png)

::: moniker-end

::: moniker range=">=vs-2019"

![ASP.NET Core Web アプリ プロジェクトを作成する](./media/tutorial-multicontainer/vs-2019/create-web-project1.png)

**[Docker サポートを有効にする]** を選択しないでください。 Docker サポートは、後で追加します。

![Web プロジェクトを作成するときの [追加情報] 画面のスクリーンショット。 [Enable Docker Support]\(Docker サポートを有効にする\) オプションは選択されていません。](./media/tutorial-multicontainer/vs-2019/create-web-project-additional-information.png)

::: moniker-end

## <a name="create-a-web-api-project"></a>Web API プロジェクトを作成する

同じソリューションにプロジェクトを追加し、*MyWebAPI* という名前を付けます。 プロジェクト タイプとして **API** を選択し、 **[HTTPS 用の構成]** チェックボックスをオフにします。 この設計では、同じ Web アプリケーション内のコンテナー間の通信ではなく、クライアントとの通信にのみ SSL を使用します。 `WebFrontEnd` のみが HTTPS を必要とし、例のコードでは、そのチェックボックスをオフにしていることを前提としています。 一般に、Visual Studio によって使用される .NET 開発者証明書は外部からコンテナーへの要求に対してのみサポートされ、コンテナーからコンテナーへの要求に対してはサポートされません。

::: moniker range="vs-2017"
   ![Web API プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/docker-tutorial-mywebapi.png)
::: moniker-end
::: moniker range=">=vs-2019"
   ![Web API プロジェクト作成のスクリーンショット](./media/tutorial-multicontainer/vs-2019/create-webapi-project.png)
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
          // request.RequestUri = new Uri("http://mywebapi/WeatherForecast"); // ASP.NET 3 (VS 2019 only)
          request.RequestUri = new Uri("http://mywebapi/api/values/1"); // ASP.NET 2.x
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```
   
    > [!NOTE]
    > 実際のコードでは、各要求の後で `HttpClient` を破棄しないでください。 ベスト プラクティスについては、「[HttpClientFactory を使用して回復力の高い HTTP 要求を実装する](/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)」を参照してください。

   Visual Studio 2019 以降の .NET Core 3.1 では、Web API テンプレートで WeatherForecast API が使用されるため、この行のコメントを解除し、ASP.NET 2.x 用の行をコメント アウトします。

1. *Index.cshtml* ファイルで、`ViewData["Message"]` を表示する行を追加し、ファイルを次のコードのようにします。
    
      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }
    
      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. (ASP.NET 2.x のみ) 次に、Web API プロジェクトで、Values コントローラーにコードを追加し、*webfrontend* から追加した呼び出しに対して API によって返されるメッセージをカスタマイズします。
    
      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

    .NET Core 3.1 では、既に存在する WeatherForecast API を使用できるため、これは必要ありません。 ただし、*Startup.cs* の `Configure` メソッドの <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection*> の呼び出しをコメント アウトする必要があります。このコードでは、Web API を呼び出すために、HTTPS ではなく HTTP が使用されているためです。

    ```csharp
                //app.UseHttpsRedirection();
    ```

1. `WebFrontEnd` プロジェクトで、**[追加] > [コンテナー オーケストレーター サポート]** の順に選択します。 **[Docker サポート オプション]** ダイアログが表示されます。

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

1. サイトをローカルで実行して (F5 キーまたは Ctrl + F5 キー)、想定どおりに動作することを確認します。 .NET Core 2.x バージョンですべてが正しく構成されている場合、"Hello from webfrontend and webapi (with value 1)" というメッセージが表示されます。  .NET Core 3 では、天気予報データが表示されます。

   コンテナー オーケストレーションを追加するときに使用する最初のプロジェクトは、実行またはデバッグの際に起動されるように設定されます。 docker-compose プロジェクトの **[プロジェクトのプロパティ]** で、起動アクションを構成できます。  docker-compose プロジェクト ノードで、右クリックしてコンテキスト メニューを開き、**[プロパティ]** を選択するか、Alt + Enter キーを押します。  次のスクリーンショットは、ここで使用するソリューションに必要なプロパティを示しています。  たとえば、**[サービス URL]** プロパティをカスタマイズすることで読み込まれるページを変更できます。

   ![docker-compose プロジェクト プロパティのスクリーンショット](media/tutorial-multicontainer/launch-action.png)

   起動時に表示されるものを次に示します (.NET Core 2.x バージョン)。

   ![実行中の Web アプリのスクリーンショット](media/tutorial-multicontainer/webfrontend.png)

   .NET 3.1 の Web アプリでは、JSON 形式で気象データが表示されます。

## <a name="next-steps"></a>次のステップ

[Azure にコンテナー](/azure/containers)をデプロイするためのオプションを確認します。

デバッグ セッション中に起動するサービスに対する制御を強化するには、Docker Compose 起動プロファイルを使用し、デバッグ時に実行されるサービスを構成する方法を学習してください。 「[Docker Compose の起動プロファイルを管理する](launch-profiles.md)」を参照してください。

## <a name="see-also"></a>関連項目
  
[Docker Compose](https://docs.docker.com/compose/)  
[コンテナー ツール](./index.yml)