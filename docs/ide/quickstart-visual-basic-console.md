---
title: Visual Basic を使用して初めてのコンソール アプリを作成する
description: Visual Studio で Visual Basic を使用して、シンプルな Hello World コンソール アプリを作成する方法の詳細な手順を説明します。
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
- vb
ms.workload:
- multiple
ms.openlocfilehash: 658faaf5b044f1c4fed70fa62f205c2fa025f640
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386242"
---
# <a name="quickstart-create-your-first-console-app-in-visual-studio-with-visual-basic"></a>クイックスタート: Visual Studio で Visual Basic を使用して初めてコンソール アプリを作成する

ここでは 5 分から 10 分で Visual Studio 統合開発環境 (IDE) の概要を示し、コンソールで実行される簡単な Visual Basic アプリケーションを作成します。

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

まず、Visual Basic アプリケーション プロジェクトを作成します。 このプロジェクトの種類には、必要となるすべてのテンプレート ファイルが付属していますので、何も追加する必要はありません。

::: moniker range="vs-2017"

1. Visual Studio 2017 を開きます。

2. 上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、**[Visual Basic]** を展開し、**[.NET Core]** を選択します。 中央のウィンドウで、 **[Console App (.NET Core)]** を選択します。 プロジェクトに *HelloWorld* という名前を付けます。

   ![Visual Studio IDE の [新しいプロジェクト] ダイアログ ボックスに示されているコンソール アプリ (.NET Core) プロジェクト テンプレート](../ide/media/new-project-vb-dotnetcore-helloworld-console-app.png)

     **[Console App (.NET Core)]** プロジェクト テンプレートが表示されない場合は、**[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクをクリックします。

   ![[新しいプロジェクト] ダイアログ ボックスで [Visual Studio インストーラーを開く] リンクをクリックする](../ide/media/vb-open-visual-studio-installer-hello-world.png)

     Visual Studio インストーラーが起動します。 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。

     ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../ide/media/dot-net-core-xplat-dev-workload.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> このクイック スタートの一部のスクリーン ショットではダーク テーマが使用されています。 ダーク テーマを使用していないが、使用したい場合は、その方法について「[Visual Studio IDE とエディターのカスタマイズ](quickstart-personalize-the-ide.md)」ページを参照してください。

1. Visual Studio を開きます。

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   ![[新しいプロジェクトの作成] ウィンドウを表示する](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. **[新しいプロジェクトの作成]** ウィンドウで、言語の一覧から **[Visual Basic]** を選択します。 次に、プラットフォームの一覧から **[Windows]** を選択し、プロジェクトの種類の一覧から **[コンソール]** を選択します。

   言語、プラットフォーム、およびプロジェクトの種類のフィルターを適用してから、 **[コンソール アプリケーション]** テンプレートを選択して、 **[次へ]** を選択します。

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-create-new-project-console-net-core.png" alt-text="コンソール アプリケーション用の Visual Basic テンプレートを選択します":::

   > [!NOTE]
   > **[コンソール アプリケーション]** テンプレートが表示されない場合は、 **[新しいプロジェクトの作成]** ウィンドウからそれをインストールすることができます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。
   >
   > ![[新しいプロジェクトの作成] ウィンドウに表示された [お探しの情報が見つかりませんでしたか?] での [さらにツールと機能をインストールする] リンク](../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > 次に、Visual Studio インストーラーで、 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択します。
   >
   > ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../get-started/media/dot-net-core-xplat-dev-workload.png)
   >
   > その後、Visual Studio インストーラー内の **[変更]** ボタンをクリックします。 作業内容を保存するよう求められることがあります。その場合は、そのようにします。 次に、 **[続行]** を選択してワークロードをインストールします。 その後、この「[プロジェクトを作成する](#create-a-project)」プロシージャの手順 2 に戻ります。

1. **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*WhatIsYourName*」と入力またはタイプします。 その後、 **[次へ]** を選択します。

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-name-your-project-whatname.png" alt-text="[新しいプロジェクトの構成] ウィンドウで、ご自分のプロジェクトに 'WhatIsYourName' という名前を付けます。":::

1. **[追加情報]** ウィンドウでは、ターゲット フレームワークとして **[.NET Core 3.1]** が既に選択されているはずです。 そうでない場合は **[.NET Core 3.1]** を選択します。 次に、 **[作成]** を選択します。

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-target-framework.png" alt-text="[追加情報] ウィンドウで、[.NET Core 3.1] が選択されていることを確認します":::

   Visual Studio によってその新しいプロジェクトが開かれます。

::: moniker-end

## <a name="create-the-application"></a>アプリケーションを作成する

Visual Basic プロジェクト テンプレートを選択し、プロジェクトに名前を付けると、簡単な "Hello World" アプリケーションが自動的に作成されます。 <xref:System.Console.WriteLine%2A> メソッドを呼び出し、リテラル文字列 "Hello World!" を コンソール ウィンドウに表示します。

![テンプレートから既定の Hello World コードを表示する](../ide/media/vb-console-helloworld-template.png)

IDE で **[Hello World]** ボタンをクリックした場合、デバッグ モードでプログラムを実行することができます。

  ![[Hello World] ボタンをクリックして、デバッグ モードでプログラムを実行する](../ide/media/vb-console-hello-world-button.png)

プログラムを実行すると、コンソール ウィンドウが一瞬だけ表示され、すぐに閉じられます。 これは、`Main` メソッドの 1 つのステートメントが実行されると、このメソッドは終了し、その結果、アプリケーションも終了するためです。

### <a name="add-some-code&quot;></a>何らかのコードを追加する

アプリケーションを一時停止し、ユーザーに入力を求めるのためのコードを追加してみましょう。

1. <xref:System.Console.WriteLine%2A> メソッドへの呼び出しのすぐ後に、次のコードを追加します。

   ```vb
   Console.Write(&quot;Press any key to continue...")
   Console.ReadKey(true)
   ```

    これにより、キー入力があるまで、プログラムは一時停止状態となります。

2. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** の順に選択します。

   これにより、プログラムが IL (中間言語) にコンパイルされ、それが JIT (just-in-time) コンパイラによってバイナリ コードに変換されます。

## <a name="run-the-application"></a>アプリケーションの実行

1. ツールバーの **[Hello World]** ボタンをクリックします。

   ![[Hello World] ボタンをクリックして、ツールバーからプログラムを実行する](../ide/media/vb-console-hello-world-button.png)

2. 任意のキーを押して、コンソール ウィンドウを閉じます。

   !["Hello World! Press any key to continue" と表示されているコンソール ウィンドウ](../ide/media/vb-console-hello-world-press-any-key.png)

## <a name="next-steps"></a>次のステップ

このクイック スタートは完了しました。 Visual Basic と Visual Studio IDE について少しはご理解いただけたかと思います。 詳細については、引き続き以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [Visual Studio の Visual Basic の概要](../get-started/visual-basic/tutorial-console.md)
