---
title: ASP.NET Core の概要
description: この記事では、インストールや新しいプロジェクトの作成など、Visual Studio for Mac で ASP.NET の使用を始める方法について説明します。
author: asb3993
ms.author: amburns
ms.date: 07/13/2017
ms.assetid: 6E8B0C90-33D6-4546-8207-CE0787584565
ms.openlocfilehash: 23a76b4d101acb0c917168515a27f2835c322415
ms.sourcegitcommit: 4c0db930d9d5d8b857d3baf2530ae89823799612
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
---
# <a name="getting-started-with-aspnet-core"></a>ASP.NET Core の概要

 Visual Studio for Mac は最新の ASP.NET Core Web 開発プラットフォームをサポートしているため、アプリのサービスを簡単に開発できます。 ASP.NET Core は .NET Core (.NET Framework とランタイムの最新の進化) で実行されます。 ASP.NET Core は、パフォーマンスが高速になるように調整されています。また、インストール サイズが小さくなるように要素が細かく分かれているほか、Windows に加えて Linux と MacOS でも動作するようにイメージが再構成されています。

## <a name="installing-net-core"></a>.NET Core のインストール

.NET Core 1.1 は、Visual Studio for Mac のインストールと共に自動的にインストールされます。

## <a name="creating-an-aspnet-core-app-in-visual-studio-for-mac"></a>Visual Studio for Mac で ASP.NET Core を作成する

Visual Studio for Mac を開きます。 ようこそページで、**[新しいプロジェクト]** を選択します。

![[新しいプロジェクト] ダイアログ](media/asp-net-core-image1.png)

[新しいプロジェクト] ダイアログが表示されます。このダイアログで、アプリケーションを作成するためのテンプレートを選択できます。

ASP.NET Core アプリケーションの作成を開始するためのテンプレートがさまざまなプロジェクトで既に用意されています。 これらの数値は、次のとおりです。

- **.NET Core > ASP.NET Core 空の Web アプリケーション**
- **.NET Core > ASP.NET Core Web アプリ**
- **.NET Core > ASP.NET Core Web API**
- **マルチプラットフォーム > アプリ > 接続型アプリ**

![ASP.NET プロジェクト オプション](media/asp-net-core-image11.png)

**[ASP.NET Core Empty Web Application]\(ASP.NET Core 空の Web アプリケーション\)** を選択し、**[次へ]** を押します。 プロジェクトに名前を付け、**[作成]** を押します。 これで新しい ASP.NET Core アプリが作成されます。下の画像のようになります。

![新しい ASP.NET Core の空のプロジェクト](media/asp-net-core-image4.png)

ASP.NET Core 空の Web アプリケーションでは、Web アプリケーションと共に **Program.cs** と **Startup.cs** という既定のファイルが 2 つ作成されます。ファイルの説明を以下に記します。 また、[依存関係] フォルダーが作成されます。このフォルダーには、ASP.NET Core、.NET Core フレームワーク、プロジェクトをビルドする MSBuild ターゲットなど、プロジェクトの NuGet パッケージ依存関係が含まれます。

![Solution Pad と依存関係](media/asp-net-core-image12.png)

### <a name="programcs"></a>Program.cs

プロジェクトの **Program.cs** ファイルを開き、中を調べます。 `Main` メソッドで 2 つのことが行われていることに注目してください。作成するアプリに入る項目です。

```csharp
public static void Main(string[] args)
{
    var host = new WebHostBuilder()
        .UseKestrel()
        .UseContentRoot(Directory.GetCurrentDirectory())
        .UseIISIntegration()
        .UseStartup<Startup>()
        .Build();

    host.Run();
}
```
ASP.NET Core アプリにより、その main メソッドで Web サーバーが作成されます。[`WebHostBuilder`](https://docs.microsoft.com/aspnet/core/fundamentals/hosting) のインスタンスを介してホストが構成され、起動されます。 このビルダーは、ホストの構成を可能にするメソッドを提供します。 テンプレート アプリで、次の構成が使用されます。

 * `UseKestrel`: Kestrel サーバーがアプリにより使用されることを指定します
 * `UseContentRoot(Directory.GetCurrentDirectory())`: アプリがこのフォルダーから起動されるとき、Web プロジェクトのルート フォルダーをアプリのコンテンツ ルートとして使用します
 * `.UseIISIntegration()`: アプリが IIS と連動しなければならないことを指定します。 IIS と ASP.NET Core を一緒に使用するには、`UseKestrel` と `UseIISIntegration` を指定する必要があります。
 * `.UseStartup<Startup>()`: スタートアップ クラスを指定します。

 ビルド/実行メソッドにより、IWebHost がビルドされます。これはアプリをホストし、入ってくる HTTP 要求の待ち受けをアプリに開始させます。

### <a name="startupcs"></a>Startup.cs

アプリのスタートアップ クラスは `WebHostBuilder` の `UseStartup()` メソッドに指定されます。 このクラスで要求処理パイプラインを指定し、サービスを構成します。

プロジェクトの **Startup.cs** ファイルを開き、中を調べます。

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
    {
        loggerFactory.AddConsole();

        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.Run(async (context) =>
        {
            await context.Response.WriteAsync("Hello World!");
        });
    }
}
```

このスタートアップ クラスは次の規則に常に従う必要があります。

 - 常にパブリックに設定する必要があります
 - `ConfigureServices` と `Configure` という 2 つのパブリック メソッドが含まれている必要があります

`ConfigureServices` メソッドは、アプリで使用されるサービスを定義します。

`Configure` により、[ミドルウェア](https://docs.microsoft.com/aspnet/core/fundamentals/middleware)を利用した要求パイプラインの作成が可能になります。 これは、要求と応答を処理するために ASP.NET アプリケーション パイプライン内で使用されるコンポーネントです。 HTTP パイプラインは、シーケンスで呼び出される、一連の要求デリゲートで構成されます。 各デリゲートは要求をそれ自体で処理するか、次のデリゲートに渡すことができます。

`IApplicationBuilder` で `Run`、`Map`、`Use` メソッドを使用することでデリゲートを構成できますが、`Run` メソッドは次のデリゲートを呼び出すことがありません。常にパイプラインの終わりで使用する必要があります。

事前作成済みテンプレートの `Configure` メソッドは、いくつかのことを行うように作成されています。 最初に、開発中に使用するために、例外処理ページを構成します。 次に、簡単な "Hello World" で要求元の Web ページに応答を送信します。

この簡単な "Hello World" プロジェクトは、コードを追加しなくても実行できるようになりました。 アプリを実行し、それをブラウザーで表示するには、ツールバーの [再生] ボタン (三角形) を押します。

![アプリを実行する](media/asp-net-core-image5.png)

Visual Studio for Mac では、ランダムのポートを利用して Web プロジェクトを起動します。 利用されているポートを調べるには、アプリケーション出力を開きます。これは **[表示]、[パッド]** にあります。 出力は下の画像のようになります。

![アプリケーション出力と待ち受けポート](media/asp-net-core-image6.png)

ブラウザーを開き、`http://localhost:5000/` を入力します。`5000` は、Visual Studio がアプリケーション出力に出力したポートに変更します。 `Hello World!` というテキストが表示されるはずです。

![ブラウザーにテキストが表示される](media/asp-net-core-image7.png)

## <a name="adding-a-controller"></a>コントローラーを追加する

ASP.NET Core アプリはモデル ビュー コントローラー (MVC) デザイン パターンを利用し、アプリの各パーツの責任を論理的に分離します。 MVC の構造は次のとおりです。

- **モデル**: アプリのデータを表すクラス。
- **ビュー**: アプリのユーザー インターフェイス (多くの場合、モデル データ) を表示します。
- **コント ローラー**: ブラウザー要求を処理し、ユーザー入力と繰り返しに応答するクラス。

MVC の使用方法については、「[Overview of ASP.NET Core MVC](https://docs.microsoft.com/aspnet/core/mvc/overview)」 (ASP.NET Core MVC の概要) ガイドを参照してください。

コントローラーは次のように追加します。

1. プロジェクト名を右クリックし、**[追加]、[新しいファイル]** の順に選択します。 **[全般]、[空のクラス]** を選択し、コントローラー名を入力します。

    ![[新しいファイル] ダイアログ](media/asp-net-core-image8.png)

2. 新しいコントローラーに次のコードを追加します。

    ```csharp
    using System;
    using Microsoft.AspNetCore.Mvc;
    using System.Text.Encodings.Web;

    namespace Hello_ASP
    {
        public class HelloWorldController : Controller
        {
            //
            // GET: /HelloWorld/

            public string Index()
            {
                return "This is my default action...";
            }

        }
    }
    ```

3. **[依存関係]** フォルダーを右クリックし、**[パッケージの追加...]** を選択して `Microsoft.AspNetCore.Mvc` 依存関係をプロジェクトに追加します。

4. 検索ボックスを利用し、`Microsoft.AspNetCore.Mvc` の NuGet ライブラリを参照し、**[パッケージの追加]** を選択します。 インストールには数分かかることがあります。必要な依存関係のためにさまざまなライセンスに同意するように求められることがあります。

    ![Nuget を追加する](media/asp-net-core-image9.png)

5. スタートアップ クラスで `app.Run` lambda を削除し、呼び出すコードを MVC が決定するための URL ルーティング ロジックを次のように設定します。

    ```csharp
    app.UseMvc(routes =>
    {
        routes.MapRoute(
        name: "default",
        template: "{controller=HelloWorld}/{action=Index}/{id?}");
    });
    ```

    `app.Run` lambda は必ず削除してください。これはルーティング ロジックをオーバーライドします。

    MVC は次の形式を利用し、実行するコードを決定します。

    `/[Controller]/[ActionName]/[Parameters]`

    上記のコード スニペットを追加すると、アプリの初期設定を `HelloWorld` コントローラーと `Index` アクション メソッドにすることになります。

6. 下の画像のように、`services.AddMvc();` 呼び出しを `ConfigureServices` メソッドに追加します。

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
    }
    ```

    URL からコントローラーにパラメーター情報を渡すこともできます。

7. 下の画像のように、HelloWorldController に別のメソッドを追加します。

    ```csharp
    public string Xamarin(string name)
    {
        return HtmlEncoder.Default.Encode($"Hello {name}, welcome to Visual Studio for Mac");
    }
    ```

8. この時点でアプリを実行すると、ブラウザーが自動的に開くはずです。

    ![ブラウザーでアプリを実行](media/asp-net-core-image13.png)

9. `http://localhost:xxxx/HelloWorld/Xamarin?name=Amy` にアクセスしてみてください。`xxxx` はポート番号に変更します。次のように表示されるはずです。

    ![引数を指定し、ブラウザーでアプリを実行](media/asp-net-core-image10.png)


## <a name="troubleshooting"></a>トラブルシューティング

Mac OS 10.11 (El Capitan) 以降に .NET Core を手動インストールする場合、次のように行います。

1. .NET Core のインストールを開始する前に、すべての OS が安定した最新版に更新されていることを確認します。 これは App Store アプリケーションで確認できます。[更新プログラム] タブを選択してください。

2. [.NET Core サイト](https://www.microsoft.com/net/core#macos)にある手順を実行してください。

4 つすべての手順を完了し、.NET Core が正しくインストールされていることを確認します。

## <a name="summary"></a>まとめ

このガイドでは、ASP.NET Core の概要を説明しました。 ASP.NET Core とは何か、それを利用する状況、Visual Studio for Mac で使用する場合について説明しました。
ここから先の手順については、次のガイドを参照してください。
- [ASP.NET Core](https://docs.microsoft.com/aspnet/core/?view=aspnetcore-2.1#build-web-ui-and-web-apis-using-aspnet-core-mvc) ドキュメント。
- [Creating Backend Services for Native Mobile Applications](https://docs.microsoft.com/aspnet/core/mobile/native-mobile-backend) (ネイティブ モバイル アプリケーションのバックエンド サービスを作成する)。ここでは、Xamarin.Forms アプリのために ASP.NET Core を利用して REST サービスをビルドする方法について解説しています。
- [ASP.NET Core 実践ラボ](https://github.com/Microsoft/vs4mac-labs/tree/master/Web/Getting-Started)。
