---
title: 'クイック スタート: F# で ASP.NET Core Web サービスを作成する'
description: Visual Studio で F# を使用して ASP.NET Core Web サービスを段階的に作成する方法について説明します。
ms.date: 08/24/2018
ms.topic: quickstart
ms.custom: vs-acquisition
author: cartermp
ms.author: phcart
manager: andrehal
dev_langs:
- FSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 298b55120a5e4d0efea1ec5eeeacc2dfa3da274f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386437"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-aspnet-core-web-service-in-f"></a>クイック スタート: F\# で Visual Studio を使用して初めての ASP.NET Core Web サービスを作成する

この 5 - 10 分の Visual Studio での F# の概要では、F# で ASP.NET Core の Web アプリケーションを作成します。

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2022"

Visual Studio 2022 プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

## <a name="create-a-project"></a>プロジェクトを作成する

まず、ASP.NET Core Web API プロジェクトを作成します。 プロジェクトの種類は、機能的な Web サービスを構成するテンプレート ファイルにあらかじめ用意されています。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

2. 上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、左ウィンドウの **[Visual F#]** を展開し、**[Web]** を選択します。 中央のウィンドウで、**[ASP.NET Core Web アプリケーション]** を選択してから **[OK]** を選択します。

     **.NET Core** プロジェクト テンプレートのカテゴリが表示されない場合は、左側のウィンドウで **[Visual Studio インストーラーを開く]** リンクを選択します。 Visual Studio インストーラーが起動します。 **[ASP.NET と Web 開発]** ワークロードを選択してから **[変更]** を選択します。

     ![VS インストーラーの ASP.NET ワークロード](../ide/media/quickstart-aspnet-workload.png)

4. **[新しい ASP.NET Core Web アプリケーション]** ダイアログ ボックスで、上部のドロップダウン メニューから **[ASP.NET Core 2.1]** を選択します。 (リストに **ASP.NET Core 2.1** が表示されない場合は、ダイアログ ボックスの上部付近にある黄色のバーに表示される **[ダウンロード]** リンクに従ってインストールしてください) **[OK]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. **[新しいプロジェクトの作成]** ページで、検索ボックスに「**f# web**」と入力し、**[ASP.NET Core Web アプリケーション]** プロジェクト テンプレートを選択します。 **[次へ]** を選択します。

4. **[新しいプロジェクトの構成]** ページで、名前を入力して、**[作成]** を選択します。

5. **[新しい ASP.NET Core Web アプリケーションを作成する]** ページで、上部のドロップダウン メニューから **[ASP.NET Core 2.1]** を選択し、**[作成]** を選択します。

::: moniker-end

## <a name="explore-the-ide"></a>IDE を探索する

1. **ソリューション エクスプローラー** のツールバーで、**Controllers** フォルダーを展開し、**[ValuesController.fs]** を選択してエディターで開きます。

   ![ソリューション エクスプローラーで Controllers フォルダーが展開されている F# での Web API プロジェクト](../ide/media/hello-world-fs-sln-explorer.png)

2. 次いで、以下のようになるように `Get()` メンバーを変更します。

   ```fsharp
   [<HttpGet>]
   member this.Get() =
       let values = [|"Hello"; "World"; "First F#/ASP.NET Core web API!"|]
       ActionResult<string[]>(values)
   ```

このコードは単純です。 値の F# 配列は、`values` 名にバインドされ、ASP.NET Core MVC フレームワークに `ActionResult` として渡されます。 残りは、ASP.NET Core がユーザーに代わって実行してくれます。

エディターでは次のようになります。

![変更された Get メンバー](../ide/media/hello-world-fs-get-member.png)

## <a name="run-the-application"></a>アプリケーションを実行する

1. **Ctrl**+**F5** キーを押してアプリケーションを実行し、Web ブラウザーで開きます。

2. このページは、`/api/values` ルートに移動されるはずですが、しない場合はご自分のブラウザーに `https://localhost:44396/api/values` と入力します。

これで Web ブラウザーに、前に入力したものと一致する JSON が表示されます。

## <a name="next-steps"></a>次のステップ

このクイック スタートは完了しました。 F#、ASP.NET Core、Visual Studio IDE について少しはご理解いただけたかと思います。 パブリック サーバー上で実行されているアプリを表示するには、次のボタンを選択します。

> [!div class="nextstepaction"]
> [Azure App Service へのアプリの展開](../deployment/quickstart-deploy-to-azure.md)

F# の詳細については、公式の「[F# Guide](/dotnet/fsharp/index)」 (F# ガイド) をご覧ください。
