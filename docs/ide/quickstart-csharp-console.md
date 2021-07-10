---
title: 'チュートリアル: Visual Studio で C# コンソール アプリを作成する'
titleSuffix: ''
description: Visual Studio で C# を使用して、シンプルな Hello World コンソール アプリを作成する方法について、ステップ バイ ステップで説明します。
ms.custom: vs-acquisition
ms.date: 03/23/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: quickstart
ms.devlang: vb
author: j-martens
ms.author: jmartens
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: bf7a52b6dbf36c25590292c3272f1e63d07156b9
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387620"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-c-console-app"></a>クイック スタート: Visual Studio を使用して初めての C# コンソール アプリを作成する

ここでは 5 分から 10 分で Visual Studio 統合開発環境 (IDE) の概要を示し、コンソールで実行される簡単な C# アプリを作成します。

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

まず、C# アプリケーション プロジェクトを作成します。 このプロジェクトの種類には、必要となるすべてのテンプレート ファイルが付属していますので、何も追加する必要はありません。

::: moniker range="vs-2017"

1. Visual Studio 2017 を開きます。

2. 上部のメニュー バーから **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

3. 左側のウィンドウの **[新しいプロジェクト]** ダイアログ ボックスで、 **[C#]** を展開し、 **[.NET Core]** を選択します。 中央のウィンドウで、 **[Console App (.NET Core)]** を選択します。 プロジェクトに *HelloWorld* という名前を付けます。

   ![Visual Studio IDE の [新しいプロジェクト] ダイアログ ボックスに示されているコンソール アプリ (.NET Core) プロジェクト テンプレート](../ide/media/new-project-csharp-dotnetcore-helloworld-console-app.png)

     **[Console App (.NET Core)]** プロジェクト テンプレートが表示されない場合は、 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクを選択します。

   ![[新しいプロジェクト] ダイアログ ボックスから [Visual Studio インストーラーを開く] リンクを選択する](../ide/media/csharp-open-visual-studio-installer-hello-world.png)

     Visual Studio インストーラーが起動します。 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。

     ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../ide/media/dot-net-core-xplat-dev-workload.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   ![[新しいプロジェクトの作成] ウィンドウ](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. **[新しいプロジェクトの作成]** ウィンドウで、検索ボックスに「*コンソール*」と入力またはタイプします。 次に、言語のリストから **[C#]** を選択して、プラットフォームのリストから **[Windows]** を選択します。 

   言語およびプラットフォームのフィルターを適用してから、 **[コンソール アプリ (.NET Core)]** テンプレートを選択して、 **[次へ]** を選択します。

   ![コンソール アプリ (.NET Framework) 用の C# テンプレートを選択する](../get-started/csharp/media/vs-2019/csharp-create-new-project-search-console-net-core-filtered.png)

   > [!NOTE]
   > **[コンソール アプリ (.NET Core)]** テンプレートが表示されない場合は、 **[新しいプロジェクトの作成]** ウィンドウからそれをインストールすることができます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。
   >
   > ![[新しいプロジェクトの作成] ウィンドウに表示された [お探しの情報が見つかりませんでしたか?] での [さらにツールと機能をインストールする] リンク](../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > 次に、Visual Studio インストーラーで、 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択します。
   >
   > ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](./media/dot-net-core-xplat-dev-workload.png)
   >
   > その後、Visual Studio インストーラー内の **[変更]** ボタンをクリックします。 作業内容を保存するよう求められることがあります。その場合は、そのようにします。 次に、 **[続行]** を選択してワークロードをインストールします。 その後、この「[プロジェクトを作成する](#create-a-project)」プロシージャの手順 2 に戻ります。

1. **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*HelloWorld*」とタイプまたは入力します。 次に、 **[作成]** を選択します。

   ![[新しいプロジェクトの構成] ウィンドウで、ご自分のプロジェクトに 'HelloWorld' という名前を付けます。](../get-started/csharp/media/vs-2019/csharp-name-your-helloworld-project.png)

   Visual Studio によってその新しいプロジェクトが開かれます。
   
::: moniker-end

## <a name="create-the-application"></a>アプリケーションを作成する

::: moniker range="vs-2017"

C# プロジェクト テンプレートを選択し、プロジェクトに名前を付けると、簡単な "Hello World" アプリケーションが Visual Studio によって自動的に作成されます。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio によって、既定の "Hello World" コードがご利用のコードに含められます。

::: moniker-end

(それを行うために、<xref:System.Console.WriteLine%2A> メソッドが呼び出され、リテラル文字列 "Hello World!" が コンソール ウィンドウに表示されます。)

   ![テンプレートから既定の Hello World コードを表示する](../ide/media/csharp-console-helloworld-template.png)

**F5** キーを押すと、プログラムをデバッグ モードで実行できます。 しかし、コンソール ウィンドウが表示されるのは、閉じる前の一瞬だけです。

(この動作が発生するのは、1 つのステートメントを実行すると `Main` メソッドが終了し、アプリケーションも終了するためです。)

### <a name="add-some-code"></a>何らかのコードを追加する

アプリケーションを一時停止させるコードを追加して、**ENTER** キーを押すまではコンソール ウィンドウが閉じられないようにしましょう。

1. <xref:System.Console.WriteLine%2A> メソッドへの呼び出しのすぐ後に、次のコードを追加します。

   ```csharp
   Console.ReadLine();
   ```

1. コード エディターで次ようになっていることを確認します。

   ![Hello World アプリを一時停止させるコードを追加する](../ide/media/csharp-console-helloworld-add-code.png)

## <a name="run-the-application"></a>アプリケーションの実行

1. ツールバーの **HelloWorld** ボタンを選択して、デバッグ モードでアプリケーションを実行します。 (または、**F5** キーを押します。)

   ![[Hello World] ボタンを選択して、ツールバーからアプリを実行する](../ide/media/csharp-console-hello-world-button.png)

1. コンソール ウィンドウでアプリを確認します。

   ![Hello World! が表示されたコンソール ウィンドウ](../ide/media/csharp-console-hello-world.png)

### <a name="close-the-application"></a>アプリケーションを終了する

1. **ENTER** キーを押して、コンソール ウィンドウを閉じます。

1. Visual Studio の **[出力]** ウィンドウを閉じます。

   ![Visual Studio の [出力] ウィンドウを閉じる](../ide/media/csharp-hello-world-close-output-pane.png)

1. Visual Studio を閉じます。

## <a name="next-steps"></a>次のステップ

このクイック スタートは完了しました。 C# と Visual Studio IDE について、少しはご理解いただけたかと思います。 詳細については、引き続き以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [Visual Studio での C# コンソール アプリの概要](../get-started/csharp/tutorial-console.md)
