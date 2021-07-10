---
title: ローカルの Docker コンテナーでアプリをデバッグする | Microsoft Docs
description: 編集と更新を使用して、ローカルの Docker コンテナーで実行されているアプリに変更を加え、デバッグのブレークポイントを設定する方法について説明します。
ms.author: ghogen
author: ghogen
manager: jmartens
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.topic: how-to
ms.workload: multiple
ms.date: 07/25/2019
ms.technology: vs-azure
ms.openlocfilehash: 8fb821acb48dd05aa09723fe5c6c254e7d1ca648
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306385"
---
# <a name="debug-apps-in-a-local-docker-container"></a>ローカルの Docker コンテナーでのアプリのデバッグ

Visual Studio を使用すると、一貫した方法で、Docker コンテナーの開発とアプリケーションの検証をローカルで行うことができます。
Docker がインストールされたローカルの Windows デスクトップ上で実行されている Linux または Windows コンテナーで、アプリの実行とデバッグを行えます。コードを変更するたびに、コンテナーを再起動する必要はありません。

この記事では、Visual Studio を使用してローカルの Docker コンテナーでアプリを起動し、変更を加えた後、ブラウザーを更新してその変更を確認する方法について説明します。 また、この記事では、コンテナー化されたアプリにデバッグ用のブレークポイントを設定する方法についても説明します。 サポートされているプロジェクトの種類には、.NET Framework および .NET Core の Web アプリとコンソール アプリなどがあります。 この記事では、ASP.NET Core Web アプリと .NET Framework コンソール アプリを使用します。

サポートされている種類のプロジェクトが既にある場合は、Visual Studio を使用して Dockerfile を作成し、コンテナー内で実行するようにプロジェクトを構成することができます。 「[Visual Studio のコンテナー ツール](overview.md)」をご覧ください。

## <a name="prerequisites"></a>必須コンポーネント

ローカルの Docker コンテナーでアプリをデバッグするには、次のツールをインストールする必要があります。

::: moniker range="vs-2017"

* Web 開発ワークロードがインストールされている [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

* Web 開発ワークロードがインストールされている [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)

::: moniker-end

::: moniker range="vs-2022"

* Web 開発ワークロードがインストールされている [Visual Studio 2022 Preview]()

::: moniker-end

ローカルで Docker コンテナーを実行するには、ローカルの Docker クライアントを用意する必要があります。 [Docker for Windows](https://www.docker.com/get-docker) を使用できますが、Hyper-V が使用され、Windows 10 が必須となります。

Docker コンテナーは .NET Framework プロジェクトと .NET Core プロジェクトで利用できます。 2 つの例を見てみましょう。 まず、.NET Core Web アプリを見てみます。 次に、.NET Framework コンソール アプリを見てみます。

## <a name="create-a-web-app"></a>Web アプリの作成

プロジェクトがあり、[概要](overview.md)に関する記事で説明されているように Docker のサポートを追加済みである場合は、このセクションを省略してください。

::: moniker range="vs-2017"
[!INCLUDE [create-aspnet5-app](../azure/includes/create-aspnet5-app.md)]
::: moniker-end
::: moniker range=">= vs-2019"
[!INCLUDE [create-aspnet5-app-2019](../azure/includes/vs-2019/create-aspnet5-app-2019.md)]
::: moniker-end

### <a name="edit-your-code-and-refresh"></a>コードを編集して更新する

変更をすばやく反復する目的で、コンテナーでアプリケーションを起動できます。 次に、変更を続け、IIS Express の場合と同じように変更を表示します。

1. 使用しているコンテナーの種類 (Linux または Windows) が使用されるように Docker が設定されていることを確認します。 タスク バーの Docker アイコンを右クリックして、必要に応じて **[Switch to Linux containers]\(Linux コンテナーに切り替える\)** または **[Switch to Windows containers]\(Windows コンテナーに切り替える\)** を選択します。

1. (.NET Core 3 以降のみ) このセクションで説明しているようにコードを編集して実行中のサイトを更新する処理は、.NET Core 3.0 以降の既定テンプレートでは有効ではありません。 有効にするには、NuGet パッケージ [Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation/) を追加します。 *Startup.cs* で、拡張メソッド `IMvcBuilder.AddRazorRuntimeCompilation` への呼び出しを `ConfigureServices` メソッドのコードに追加します。 これを有効にする必要があるのはデバッグ モードのみなので、コードは次のようになります。

    ```csharp
    public IWebHostEnvironment Env { get; set; }

    public void ConfigureServices(IServiceCollection services)
    {
        IMvcBuilder builder = services.AddRazorPages();

    #if DEBUG
        if (Env.IsDevelopment())
        {
            builder.AddRazorRuntimeCompilation();
        }
    #endif

        // code omitted for brevity
    }
    ```

    次のように、`Startup` メソッドを変更します。

    ```csharp
    public Startup(IConfiguration configuration, IWebHostEnvironment webHostEnvironment)
    {
        Configuration = configuration;
        Env = webHostEnvironment;
    }
    ```

   詳細については、「[ASP.NET Core での Razor ファイルのコンパイル](/aspnet/core/mvc/views/view-compilation?view=aspnetcore-3.1&preserve-view=true)」を参照してください。

1. **[ソリューション構成]** を **[デバッグ]** に設定します。 次に、**Ctrl**+**F5** を押し、Docker イメージをビルドしてローカルで実行します。

    コンテナー イメージがビルドされ、Docker コンテナーで実行されると、Visual Studio では、既定のブラウザーでその Web アプリが起動します。

1. *インデックス* ページに移動します。 このページで変更を行います。
1. Visual Studio に戻り、*Index.cshtml* を開きます。
1. ファイルの最後に次の HTML コンテンツを追加し、変更を保存します。

    ```html
    <h1>Hello from a Docker container!</h1>
    ```

1. 出力ウィンドウで、.NET ビルドが完了して次の行が表示されたら、お使いのブラウザーに戻り、ページを更新します。

   ```output
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down.
   ```

変更が適用されました。

### <a name="debug-with-breakpoints"></a>ブレークポイントを使用してデバッグする

変更にはさらなる調査が必要になることがしばしばあります。 この作業には、Visual Studio のデバッグ機能を利用できます。

1. Visual Studio で *Index.cshtml.cs* を開きます。
2. `OnGet` メソッドの内容を次のコードに置き換えます。

   ```csharp
       ViewData["Message"] = "Your application description page from within a container";
   ```

3. コード行の左側にブレークポイントを設定します。
4. デバッグを開始してブレークポイントまで進めるには、F5 キーを押します。
5. Visual Studio に切り替えるとブレークポイントが表示されます。 値を調べます。

   ![Visual Studio の Index.cshtml.cs のコードの一部を示すスクリーンショット。黄色で強調表示されているコード行の左側にブレークポイントが設定されています。](media/edit-and-refresh/breakpoint.png)

## <a name="create-a-net-framework-console-app"></a>.NET Framework コンソール アプリを作成する

.NET Framework コンソール アプリ プロジェクトを使用するとき、オーケストレーションなしで Docker サポートを追加することはできません。 ただし、Docker プロジェクトを 1 つだけ使用している場合でも、次の手順を使用できます。

1. .NET Framework コンソール アプリ プロジェクトを新規作成する
1. ソリューション エクスプローラーでプロジェクト ノードを右クリックし、 **[追加]** 、 **[Container Orchestration Support]\(コンテナー オーケストレーションのサポート\)** の順に選択します。  ダイアログ ボックスが表示されたら、 **[Docker Compose]** を選択します。 Dockerfile がプロジェクトに追加され、Docker Compose プロジェクトと関連サポート ファイルが追加されます。

### <a name="debug-with-breakpoints"></a>ブレークポイントを使用してデバッグする

1. ソリューション エクスプローラーで、*Program.cs* を開きます。
2. `Main` メソッドの内容を次のコードに置き換えます。

   ```csharp
       System.Console.WriteLine("Hello, world!");
   ```

3. コード行の左側にブレークポイントを設定します。
4. F5 キーを押すと、デバッグが開始され、ブレークポイントまで進みます。
5. Visual Studio に切り替えてブレークポイントを表示し、値を調べます。

   ![Visual Studio の Program.cs のコード ウィンドウのスクリーンショット。黄色で強調表示されているコード行の左側にブレークポイントが設定されています。](media/edit-and-refresh/breakpoint-console.png)

## <a name="container-reuse"></a>コンテナーの再利用

開発サイクル中、Dockerfile を変更したとき、Visual Studio では、コンテナー イメージとコンテナー自体だけが再構築されます。 Dockerfile を変更しない場合、Visual Studio では、以前の実行からのコンテナーが再利用されます。

コンテナーを手動で修正した後、クリーンなコンテナー イメージで再開する場合、Visual Studio で **[ビルド]** の **[クリーン]** コマンドを使用し、その後、通常どおりビルドします。

## <a name="troubleshoot"></a>トラブルシューティング

[Visual Studio Docker 開発で発生する問題を解決する](troubleshooting-docker-errors.md)方法について説明します。

## <a name="next-steps"></a>次の手順

「[Visual Studio でコンテナー化されたアプリをビルドする方法](container-build.md)」を参照して、詳細を確認します。

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Visual Studio、Windows、Azure を使用した Docker の詳細

* [Visual Studio でコンテナーを開発する](./index.yml)方法について説明します。
* Docker コンテナーをビルドし、デプロイする方法については、「[Azure Pipelines 向けの Docker の統合](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker)」を参照してください。
* Windows Server と Nano Server に関する記事の索引が必要であれば、「[Windows コンテナー情報](/virtualization/windowscontainers/)」を参照してください。
* Azure Kubernetes Service の詳細は[こちら](https://azure.microsoft.com/services/kubernetes-service/)をご覧ください。また、[Azure Kubernetes Service ドキュメント](/azure/aks)を確認してください。
