---
title: 'チュートリアル: Visual Basic 入門'
description: Visual Studio で Visual Basic コンソール アプリを作成する方法の詳細な手順を説明します。
ms.custom: vs-acquisition,  get-started
ms.date: 02/10/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: vb
author: j-martens
ms.author: jmartens
manager: jmartens
dev_langs:
- vb
ms.workload:
- multiple
ms.openlocfilehash: 8d34fef6251da95b6c3ac99430b87d853d4b5ba7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390712"
---
# <a name="tutorial-get-started-with-visual-basic-in-visual-studio"></a>チュートリアル: Visual Studio の Visual Basic の概要

この Visual Basic (VB) に関するチュートリアルでは、Visual Studio を使用して、いくつかの異なるコンソール アプリを作成して実行しながら、[Visual Studio の統合開発環境 (IDE)](visual-studio-ide.md) の一部の機能を検討します。

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

3. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、**[Visual Basic]** を展開し、**[.NET Core]** を選択します。 中央のウィンドウで、 **[Console App (.NET Core)]** を選択します。 プロジェクトに *WhatIsYourName* という名前を付けます。

   ![Visual Studio IDE の [新しいプロジェクト] ダイアログ ボックスに示されているコンソール アプリ (.NET Core) プロジェクト テンプレート](media/new-project-vb-dotnetcore-whatisyourname-console-app.png)

### <a name="add-a-workload-optional"></a>ワークロードを追加する (省略可能)

**コンソール アプリ (.NET Core)** プロジェクト テンプレートが表示されない場合は、 **.NET Core クロスプラットフォームの開発** ワークロードを追加して取得できます。 コンピューターにインストールされている Visual Studio 2017 の更新プログラムに応じて、次の 2 つの方法のうちのいずれかでこのワークロードを追加することができます。

#### <a name="option-1-use-the-new-project-dialog-box"></a>オプション 1:[新しいプロジェクト] ダイアログ ボックスを使用する

1. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、**[Visual Studio インストーラーを開く]** リンクをクリックします。

   ![[新しいプロジェクト] ダイアログ ボックスで [Visual Studio インストーラーを開く] リンクをクリックする](../media/vs-open-visual-studio-installer-generic.png)

1. Visual Studio インストーラーが起動します。 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。

   ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../media/tutorial-aspnet-workload.png)

#### <a name="option-2-use-the-tools-menu-bar"></a>オプション 2:[ツール] メニュー バーを使用する

1. **[新しいプロジェクト]** ダイアログ ボックスを取り消し、上部のメニュー バーから **[ツール]** > **[ツールと機能を取得]** の順に選択します。

1. Visual Studio インストーラーが起動します。 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> このチュートリアルの一部のスクリーン ショットではダーク テーマが使用されています。 ダーク テーマを使用していないが、使用したい場合は、その方法について「[Visual Studio IDE とエディターのカスタマイズ](../../ide/quickstart-personalize-the-ide.md)」ページを参照してください。

1. Visual Studio を開きます。

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   ![[新しいプロジェクトの作成] ウィンドウを表示する](../../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. **[新しいプロジェクトの作成]** ウィンドウで、言語の一覧から **[Visual Basic]** を選択します。 次に、プラットフォームの一覧から **[Windows]** を選択し、プロジェクトの種類の一覧から **[コンソール]** を選択します。

   言語、プラットフォーム、およびプロジェクトの種類のフィルターを適用してから、 **[コンソール アプリケーション]** テンプレートを選択して、 **[次へ]** を選択します。

   :::image type="content" source="./media/vs-2019/vb-create-new-project-console-net-core.png" alt-text="コンソール アプリケーション用の Visual Basic テンプレートを選択します":::

   > [!NOTE]
   > **[コンソール アプリケーション]** テンプレートが表示されない場合は、 **[新しいプロジェクトの作成]** ウィンドウからそれをインストールすることができます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。
   >
   > ![[新しいプロジェクトの作成] ウィンドウに表示された [お探しの情報が見つかりませんでしたか?] での [さらにツールと機能をインストールする] リンク](../../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > 次に、Visual Studio インストーラーで、 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択します。
   >
   > ![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../../get-started/media/dot-net-core-xplat-dev-workload.png)
   >
   > その後、Visual Studio インストーラー内の **[変更]** ボタンをクリックします。 作業内容を保存するよう求められることがあります。その場合は、そのようにします。 次に、 **[続行]** を選択してワークロードをインストールします。 その後、この「[プロジェクトを作成する](#create-a-project)」プロシージャの手順 2 に戻ります。

1. **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*WhatIsYourName*」と入力またはタイプします。 その後、 **[次へ]** を選択します。

   :::image type="content" source="./media/vs-2019/vb-name-your-project-whatname.png" alt-text="[新しいプロジェクトの構成] ウィンドウで、ご自分のプロジェクトに 'WhatIsYourName' という名前を付けます。":::

1. **[追加情報]** ウィンドウでは、ターゲット フレームワークとして **[.NET Core 3.1]** が既に選択されているはずです。 そうでない場合は **[.NET Core 3.1]** を選択します。 次に、 **[作成]** を選択します。

   :::image type="content" source="./media/vs-2019/vb-target-framework.png" alt-text="[追加情報] ウィンドウで、[.NET Core 3.1] が選択されていることを確認します":::

   Visual Studio によってその新しいプロジェクトが開かれます。

::: moniker-end

## <a name="create-a-what-is-your-name-application"></a>"What Is Your Name" アプリケーションを作成する

名前の入力を求めた後に、日付と時刻と共にそれを表示するアプリを作成してみましょう。 以下にその方法を示します。

 ::: moniker range="vs-2017"

1. *WhatIsYourName* プロジェクトがまだ開いていない場合は、これを開きます。

1. 次の Visual Basic コードを `Sub Main(args As String())` 行と `End Sub` 行の間に入力します。このコードは左かっこのすぐ後に配置します。

     ```vb
     Console.WriteLine(vbCrLf + "What is your name? ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"{vbCrLf}Hello, {name}, on {currentDate:d} at {currentDate:t}")
     Console.Write(vbCrLf + "Press any key to exit... ")
     Console.ReadKey(True)
    ```

    このコードでは、既存の <xref:System.Console.WriteLine%2A>、<xref:System.Console.Write%2A>、および <xref:System.Console.ReadKey%2A> ステートメントを置き換えます。

   ![What Is Your Name コードが表示されているコード ウィンドウ](./media/vs-2019/vb-codewindow-what-name-dark.png)

1. 緑色の **[開始]** ボタンを使用するか、**F5** キーを押して、最初のアプリをビルドして実行します。

1. コンソール ウィンドウが開いたら、自分の名前を入力します。 コンソール ウィンドウは次のスクリーン ショットのようになります。

   ![What Is Your Name、時刻と日付、Press any key to continue メッセージが表示されているコンソール ウィンドウ](media/vb-console-what-name.png)

1. 任意のキーを押して、コンソール ウィンドウを閉じます。

::: moniker-end

::: moniker range=">=vs-2019"

1. *[WhatIsYourName]* プロジェクト内で、次の Visual Basic コードを `Sub Main(args As String())` 行と `End Sub` 行の間に入力します。このコードは左かっこのすぐ後に配置します。

     ```vb
     Console.WriteLine(vbCrLf + "What is your name? ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"{vbCrLf}Hello, {name}, on {currentDate:d} at {currentDate:t}!")
     Console.Write(vbCrLf + "Press any key to exit... ")
     Console.ReadKey(True)
    ```

    このコードでは、既存の <xref:System.Console.WriteLine%2A>、<xref:System.Console.Write%2A>、および <xref:System.Console.ReadKey%2A> ステートメントを置き換えます。

   ![What Is Your Name コードが表示されているコード ウィンドウ](./media/vs-2019/vb-codewindow-what-name-dark.png)

1. 緑色の **[開始]** ボタンを使用するか、**F5** キーを押して、最初のアプリをビルドして実行します。

1. コンソール ウィンドウが開いたら、自分の名前を入力します。 コンソール ウィンドウは次のスクリーン ショットのようになります。

   ![What Is Your Name、時刻と日付、Press any key to continue メッセージが表示されているコンソール ウィンドウ](media/vb-console-what-name.png)

1. 任意のキーを押して、コンソール ウィンドウを閉じます。

 ::: moniker-end

## <a name="create-a-calculate-this-application"></a>"Calculate This" アプリケーションを作成する

::: moniker range="vs-2017"

1. Visual Studio 2017 を開き、上部のメニュー バーから **[ファイル]** > **[新規作成]** > **[プロジェクト]** の順に選択します。

1. **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、**[Visual Basic]** を展開し、**[.NET Core]** を選択します。 中央のウィンドウで、 **[Console App (.NET Core)]** を選択します。 次に、ファイルに *CalculateThis* という名前を付けます。

1. `Module Program` 行と `End Module` 行の間に次のコードを入力します。

   ```vb
   Public num1 As Integer
   Public num2 As Integer
   Public answer As Integer
   Sub Main()
       Console.WriteLine("Type a number and press Enter")
       num1 = Console.ReadLine()
       Console.WriteLine("Type another number to add to it and press Enter")
       num2 = Console.ReadLine()
       answer = num1 + num2
       Console.WriteLine("The answer is " & answer)
       Console.ReadLine()
   End Sub
   ```

   コード ウィンドウは次のスクリーンショットのようになります。

   ![CalculateThis コードが表示されているコード ウィンドウ](media/vb-codewindow-calculate-this.png)

1. **CalculateThis** をクリックしてプログラムを実行します。 コンソール ウィンドウは次のスクリーン ショットのようになります。

    ![実行するアクションに対するプロンプトを含む、CalculateThis アプリが表示されているコンソール ウィンドウ](media/vb-console-calculate-this.png)

::: moniker-end 

::: moniker range=">=vs-2019"

1. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。 

1. **[新しいプロジェクトの作成]** ウィンドウで、言語の一覧から **[Visual Basic]** を選択します。 次に、プラットフォームの一覧から **[Windows]** を選択し、プロジェクトの種類の一覧から **[コンソール]** を選択します。

1. 言語、プラットフォーム、およびプロジェクトの種類のフィルターを適用してから、 **[コンソール アプリケーション]** テンプレートを選択して、 **[次へ]** を選択します。

   次に、**[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*CalculateThis*」とタイプまたは入力します。 その後、 **[次へ]** を選択します。

1. **[追加情報]** ウィンドウでは、ターゲット フレームワークとして **[.NET Core 3.1]** が既に選択されているはずです。 そうでない場合は **[.NET Core 3.1]** を選択します。 次に、 **[作成]** を選択します。

1. `Module Program` 行と `End Module` 行の間に次のコードを入力します。

   ```vb
   Public num1 As Integer
   Public num2 As Integer
   Public answer As Integer
   Sub Main()
       Console.WriteLine("Type a number and press Enter")
       num1 = Console.ReadLine()
       Console.WriteLine("Type another number to add to it and press Enter")
       num2 = Console.ReadLine()
       answer = num1 + num2
       Console.WriteLine("The answer is " & answer)
       Console.ReadLine()
   End Sub
   ```

   コード ウィンドウは次のスクリーンショットのようになります。

   ![CalculateThis コードが表示されているコード ウィンドウ](media/vb-codewindow-calculate-this.png)

1. **CalculateThis** をクリックしてプログラムを実行します。 コンソール ウィンドウは次のスクリーン ショットのようになります。

    ![実行するアクションに対するプロンプトを含む、CalculateThis アプリが表示されているコンソール ウィンドウ](media/vb-console-calculate-this.png)

::: moniker-end

## <a name="quick-answers-faq"></a>FAQ に対する簡単な回答

以下の簡単な FAQ で、主な概念をいくつか示します。

### <a name="what-is-visual-basic"></a>Visual Basic とは何ですか?

Visual Basic は、習得しやすいように設計されたタイプ セーフのプログラミング言語です。 BASIC (つまり、初心者向けの汎用シンボリック命令コード) から派生したものです。

### <a name="what-is-visual-studio"></a>Visual Studio とは何ですか?

Visual Studio は、開発者向け生産性向上ツールの統合開発スイートです。 プログラムやアプリケーションを作成するために使用できるプログラムのようなものと考えてください。

### <a name="what-is-a-console-app"></a>コンソール アプリとは何ですか?

コンソール アプリは、コマンドライン ウィンドウ (別名コンソール) で入力を取得し、出力を表示します。

### <a name="what-is-net-core"></a>.NET Core とは何ですか?

.NET Core は、.NET Framework の次の進化段階です。 .NET Framework ではプログラミング言語間でコードを共有できましたが、.NET Core ではプラットフォーム間でコードを共有する機能が追加されました。 さらに良い点は、オープン ソースであるという点です  (.NET Framework および .NET Core の両方にビルド済みの機能のライブラリと、コードを実行する仮想マシンとして機能する、共通言語ランタイム (CLR) が含まれています)。

## <a name="next-steps"></a>次の手順

これでこのチュートリアルは完了です。 詳細については、以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [Visual Studio で Visual Basic と .NET Core SDK を使用してライブラリを構築する](/dotnet/core/tutorials/vb-library-with-visual-studio)

## <a name="see-also"></a>関連項目

* [Visual Basic 言語のチュートリアル](/dotnet/visual-basic/walkthroughs)
* [Visual Basic の言語リファレンス](/dotnet/visual-basic/language-reference/index)
* [Visual Basic コード ファイルの IntelliSense](../../ide/visual-basic-specific-intellisense.md)
