---
title: Visual Basic 開発者向けの概要
description: Visual Basic 開発者として、Visual Studio を使用してコードの編集、デバッグ、およびビルドを行い、アプリを発行する方法について説明します。
ms.date: 03/02/2021
ms.technology: vs-ide-general
ms.custom:
- vs-acquisition
- get-started
- SEO-VS-2020
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 486201d61f6bd2d149c9aea66efee1814ce667e7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386632"
---
# <a name="welcome-to-the-visual-studio-ide--visual-basic"></a>Visual Studio IDE へようこそ | Visual Basic

Visual Studio *統合開発環境* は、コードの編集、デバッグ、ビルドを行ってから、アプリを発行するために使用できるクリエイティブなランチパッドです。 統合開発環境 (IDE) は、ソフトウェア開発の多くの側面で使用できる機能を豊富に備えたプログラムです。 大部分の IDE が備える標準的なエディターおよびデバッガーに加えて、Visual Studio ではコンパイラ、コード補完ツール、グラフィック デザイナーなど、ソフトウェア開発プロセスを容易にする多くの機能を用意しています。

::: moniker range="vs-2017"

![Visual Studio IDE](../media/visual-studio-ide.png)

::: moniker-end

::: moniker range=">=vs-2019"

[![The Visual Studio 2019 IDE](media/vs-2019/ide-overview.png)](media/vs-2019/ide-overview.png#lightbox)

::: moniker-end

これはプロジェクトを開いている Visual Studio の画像です。使用頻度が高いツール ウィンドウがいくつか開いています。

- [ソリューション エクスプローラー](../../ide/solutions-and-projects-in-visual-studio.md) (右上) では、コード ファイルを表示、移動、および管理できます。 **ソリューション エクスプローラー** では、ファイルを [ソリューションやプロジェクト](tutorial-projects-solutions.md)にまとめ、コードを整理できます。

- 大部分の時間を費やすことになる[エディター ウィンドウ](../../ide/writing-code-in-the-code-and-text-editor.md) (中央) にはファイルの内容が表示されます。 ここでは、コードを編集したり、ボタンやテキスト ボックスを持つウィンドウなどのユーザー インターフェイスをデザインすることができます。

- [[出力]](../../ide/reference/output-window.md) ウィンドウ (下中央) には、デバッグ メッセージ、エラー メッセージ、コンパイラの警告、公開状態メッセージなど、Visual Studio の通知が出力されます。 メッセージ ソースごとに独自のタブがあります。

- [チーム エクスプローラー](/azure/devops/user-guide/work-team-explorer?view=vsts&preserve-view=true) (右下) では、[Git](https://git-scm.com/) や [Team Foundation バージョン管理 (TFVC)](/azure/devops/repos/tfvc/overview?view=vsts&preserve-view=true) などのバージョン管理テクノロジを使用して、作業項目を追跡し、コードを他のユーザーと共有できます。

## <a name="editions"></a>エディション

Visual Studio は Windows と Mac で利用できます。 [Visual Studio for Mac](/visualstudio/mac/) は Visual Studio 2017 と同じ機能を多く備え、クロスプラットフォーム アプリとモバイル アプリの開発用に最適化されています。 この記事では、Windows バージョンの Visual Studio 2017 について説明します。

Visual Studio 2017 には 3 つのエディションがあります。Community、Professional、Enterprise です。 各エディションでサポートされている機能については、「[Visual Studio 2017 IDE の比較](https://visualstudio.microsoft.com/vs/compare/)」を参照してください。

## <a name="popular-productivity-features"></a>よく使われる生産性機能

ソフトウェアを開発する際に、生産性を高めるために Visual Studio でよく使われる機能のいくつかを以下に示します。

- 波線と[クイック アクション](../../ide/quick-actions.md)

   波線は波打った下線で、コード入力時にエラーや潜在的な問題を警告します。 このような視覚的な手がかりを利用することにより、ビルド中またはプロフラム実行時にエラーが検出されるのを待たなくても問題をすぐに修正することができます。 波線の上に移動すると、エラーに関する追加情報が表示されます。 電球とエラーを修正する方法 (クイック アクションとして知られている) が左余白に表示される場合もあります。

   ::: moniker range="vs-2017"

   ![Visual Studio での波線](media/squiggles-error.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio での波線](media/vs-2019/squiggles-error.png)

   ::: moniker-end

- [リファクタリング](../../ide/refactoring-in-visual-studio.md)

   リファクタリングには、変数の名前をインテリジェントに変更する、1 つまたは複数のコード行を新しいメソッドに抽出する、メソッド パラメーターを並べ替える、などの操作が含まれます。

   ::: moniker range="vs-2017"

   ![Visual Studio のリファクタリング メニュー](media/refactoring-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio のリファクタリング メニュー](media/vs-2019/refactorings-menu.png)

   ::: moniker-end

- [IntelliSense](../../ide/using-intellisense.md)

   IntelliSense は、コードに関する情報をエディターに直接表示したり、場合によっては、ちょっとしたコードを自動的に作成したりする機能のセットを表す用語です。 エディター内のインラインに基本ドキュメントがあるようなもので、これによって、他の場所で型情報を検索する手間が省けます。 IntelliSense 機能は言語によって異なります。 詳細については、「[C# の IntelliSense](../../ide/visual-csharp-intellisense.md)」、「[Visual C++ の IntelliSense](../../ide/visual-cpp-intellisense.md)」、「[JavaScript IntelliSense](../../ide/javascript-intellisense.md)」、および [Visual Basic IntelliSense](../../ide/visual-basic-specific-intellisense.md) に関するページを参照してください。 次の図は、IntelliSense によって型のメンバー リストがどのように表示されるかを示したものです。

   ::: moniker range="vs-2017"

   ![Visual Studio のメンバーの一覧](media/intellisense-list-members.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio のメンバーの一覧](media/vs-2019/intellisense-list-members.png)

   ::: moniker-end

- 検索ボックス

   Visual Studio には非常に多くのメニュー、オプション、およびプロパティがあるため、手に負えないもののように思える場合があるかもしれません。 検索ボックスは、Visual Studio 内で必要な情報を迅速に見つけるのに役立ちます。 探しているものを表す名前の入力を開始すると、Visual Studio に結果がリストされ、目的の場所に正確に移動できます。 Visual Studio に機能を追加する必要がある場合 (追加のプログラミング言語に対してサポートを追加するなど)、検索ボックスの結果として、ワークロードまたは個々のコンポーネントをインストールするための Visual Studio インストーラーが開かれます。

   > [!TIP]
   > 検索ボックスのショートカットとしては、**Ctrl**+**Q** キーを押します。

   ::: moniker range="vs-2017"

   ![Visual Studio 2017 でのクイック起動検索ボックス](../media/quick-launch-nuget.png)

   詳細については、[クイック起動](../../ide/reference/quick-launch-environment-options-dialog-box.md)に関するページを参照してください。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 の検索ボックス](media/vs-2019/quick-launch.png)

   ::: moniker-end

- [Live Share](/visualstudio/liveshare/)

   アプリの種類やプログラミング言語に関係なく、リアルタイムで他のユーザーと共同で編集やデバッグを行います。 プロジェクトをすぐに安全に共有し、必要に応じて、デバッグ セッション、ターミナルのインスタンス、localhost の Web アプリ、音声通話などを共有することができます。

- [呼び出し階層](../../ide/reference/call-hierarchy.md)

   **[呼び出し階層]** ウィンドウには、選択したメソッドを呼び出すメソッドが表示されます。 この情報は、メソッドの変更や削除について考えるとき、またはバグの追跡を試みるときに有用です。

   ::: moniker range="vs-2017"

   ![Visual Studio での [呼び出し階層] ウィンドウ](media/call-hierarchy.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio での [呼び出し階層] ウィンドウ](media/vs-2019/call-hierarchy.png)

   ::: moniker-end

- [CodeLens](../../ide/find-code-changes-and-other-history-with-codelens.md)

   CodeLens を使用すると、コードへの参照、コードへの変更、リンクされたバグ、作業項目、コード レビュー、単体テストをすべて、エディターから離れずに楽に検索できます。

   ::: moniker range="vs-2017"

   ![Visual Studio の CodeLens](media/codelens.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio の CodeLens](media/vs-2019/codelens.png)

   ::: moniker-end

- [定義に移動](../../ide/go-to-and-peek-definition.md)

   [定義に移動] 機能では、関数または型が定義されている場所に直接移動できます。

   ::: moniker range="vs-2017"

   ![Visual Studio 2017 での [定義に移動]](media/go-to-definition-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 での [定義に移動]](media/vs-2019/go-to-definition-menu.png)

   ::: moniker-end

- [定義をここに表示](../../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)

   **[ピークの定義]** ウィンドウには、実際に個々のファイルを開かなくても、メソッドまたは型の定義が表示されます。

   ::: moniker range="vs-2017"

   ![Visual Studio の [定義のピーク]](media/peek-definition.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio の [定義のピーク]](media/vs-2019/peek-definition.png)

   ::: moniker-end

## <a name="install-the-visual-studio-ide"></a>Visual Studio IDE のインストール

このセクションでは、簡単なプロジェクトを作成し、Visual Studio でできることをいくつか試してみます。 配色テーマを変更し、コーディング支援として [IntelliSense](../../ide/using-intellisense.md) を使用し、アプリをデバッグしてプログラムの実行中に変数の値を確認します。

::: moniker range="vs-2017"

まず、[Visual Studio をダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)してシステムにインストールします。 モジュラー インストーラーでは、*ワークロード* (好みのプログラミング言語やプラットフォームで必要な機能のグループ) を選択してインストールできます。 [プログラムの作成](#create-a-program)手順に従う場合は、インストール時に必ず、**[.NET Core クロスプラットフォームの開発]** ワークロードを選択します。

::: moniker-end

::: moniker range=">=vs-2019"

まず、[Visual Studio をダウンロード](https://visualstudio.microsoft.com/downloads)してシステムにインストールします。 モジュラー インストーラーでは、*ワークロード* (好みのプログラミング言語やプラットフォームで必要な機能のグループ) を選択してインストールできます。 [プログラムの作成](#create-a-program)手順に従う場合は、インストール時に必ず、**[.NET Core クロスプラットフォームの開発]** ワークロードを選択します。

::: moniker-end

![Visual Studio インストーラーの [.NET Core クロスプラットフォームの開発] ワークロード](../media/dotnet-core-cross-platform-workload.png)

Visual Studio を初めて開くときは、Microsoft アカウントや、職場または学校アカウントを使用して、[サインイン](../../ide/signing-in-to-visual-studio.md)することもできます。

## <a name="customize-visual-studio"></a>Visual Studio をカスタマイズする

既定の配色テーマの変更など、Visual Studio ユーザー インターフェイスをカスタマイズできます。

### <a name="change-the-color-theme"></a>[配色テーマ] を変更する

**濃色** テーマに変更するには:

::: moniker range="vs-2017"

1. Visual Studio を開きます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。 スタート ウィンドウで、 **[コードなしで続行]** を選択します。


    :::image type="content" source="media/vs-2019/continue-without-code.png" alt-text="[コードなしで続行] リンクが強調表示されている Visual Studio 2019 のスタート ウィンドウのスクリーンショット。":::

   IDE が開きます。

::: moniker-end

2. メニュー バーから **[ツール]**  >  **[オプション]** の順に選択して、 **[オプション]** ダイアログを開きます。

3. **[環境]**  >  **[全般]** オプションのページで、 **[配色テーマ]** の選択内容を **[濃色]** に変更して **[OK]** をクリックします。

   ![Visual Studio で配色テーマを濃色に変更する](media/change-color-theme.png)

   IDE 全体の配色テーマが **濃色** に変更されます。

   ::: moniker range="vs-2017"

   ![ダーク テーマでの Visual Studio](../../ide/media/quickstart-personalize-dark-theme.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![ダーク テーマでの Visual Studio](media/vs-2019/dark-theme.png)

   ::: moniker-end

### <a name="select-environment-settings"></a>環境設定を選択する

次に、Visual Basic 開発者に合わせた環境設定を使用するように Visual Studio を構成します。

1. メニュー バーで、 **[ツール]**  >  **[設定のインポートとエクスポート]** の順にクリックします。

2. **設定のインポートとエクスポート ウィザード** の最初のページで **[すべての設定をリセット]** を選択し、 **[次へ]** をクリックします。

3. **[現在の設定の保存]** ページで、現在の設定を保存する、または保存しないオプションを選択し、 **[次へ]** をクリックします (設定をカスタマイズしていない場合は、 **[No, just reset settings, overwriting my current settings]\(いいえ、設定をリセットして現在の設定を上書きするだけです\)** を選択します)。

4. **[設定の既定のコレクションの選択]** ページで、 **[Visual Basic]** を選択し、 **[完了]** をクリックします。

5. **[リセットの完了]** ページで **[閉じる]** をクリックします。

IDE の他のカスタマイズ方法については、「[Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)」をご覧ください。

## <a name="create-a-program"></a>プログラムを作成する

簡単なプログラムを作成してみましょう。

::: moniker range="vs-2017"

1. Visual Studio メニュー バーで、**[ファイル]** > **[新しいプロジェクト]** を選択します。

   ![メニュー バーで [ファイル]、[新しいプロジェクト] の順に選択します。](media/file-new-project-menu.png)

   **[新しいプロジェクト]** ダイアログ ボックスには複数のプロジェクト "*テンプレート*" が表示されます。 テンプレートには、特定のプロジェクト タイプに必要な基本的なファイルと設定が含まれています。

1. **[Visual Basic]** で **[.NET Core]** カテゴリを選択し、**[Console App (.NET Core)]\(コンソール アプリ (.NET Core)\)** テンプレートを選択します。 **[名前]** テキスト ボックスに「**HelloWorld**」と入力し、**[OK]** ボタンを選びます。

   ![.NET Core アプリ テンプレート](media/overview-npd.png)

   > [!NOTE]
   > **[.NET Core]** カテゴリが表示されない場合は、**[.NET Core クロスプラットフォームの開発]** ワークロードをインストールする必要があります。 これを実行するには、**[新しいプロジェクト]** ダイアログ ボックスの左下側の **[Visual Studio インストーラーを開く]** リンクをクリックします。 Visual Studio インストーラーが開いたら、**[.NET Core クロスプラットフォームの開発]** ワークロードまで下にスクロールして選択してから **[変更]** を選択します。

   Visual Studio によってプロジェクトが作成されます。 これは、リテラル文字列 "Hello World!" を表示する <xref:System.Console.WriteLine?displayProperty=nameWithType> メソッドを呼び出す単純な "Hello World" アプリケーションです。 コンソール (プログラムの出力) ウィンドウでに表示されます。

   すぐに次のようなグラフが表示されます。

   ![Visual Studio IDE](media/overview-ide-console-app.png)

   アプリの Visual Basic コードは、領域の大部分を占めるエディター ウィンドウに表示されます。 キーワードや型など、コードの異なる部分を示すようにテキストが自動的に色分けされているのに注目してください。 また、コードの縦の小さな点線は互いに一致する括弧を示し、行番号は後でコードの場所を探すのに役立ちます。 小さな四角で囲まれたマイナス記号を選択するとコード ブロックが折りたたまれ、折りたたまれている場合は展開できます。 このコードのアウトライン機能を使用すると、必要のないコードを非表示にして画面を整理できます。 プロジェクト ファイルは右側の **ソリューション エクスプローラー** と呼ばれるウィンドウに一覧表示されます。

   ![赤色のボックスを持つ Visual Studio IDE](media/overview-ide-console-app-red-boxes.png)

   他にもメニューやツール ウィンドウが用意されていますが、今は次に進みましょう。

1. アプリを起動します。 そのためには、メニュー バーの **[デバッグ]** メニューから **[デバッグなしで開始]** を選択します。 あるいは、**Ctrl**+**F5 キー** を押します。

   ![[デバッグ]、[デバッグなしで開始] メニューを選択](../media/overview-start-without-debugging.png)

   Visual Studio でアプリがビルドされ、コンソール ウィンドウが開き、メッセージ **Hello World!** が表示されます。 これで実行中のアプリができました。

   ![コンソール ウィンドウ](../media/overview-console-window.png)

1. コンソール ウィンドウを閉じるには、キーボードで任意のキーを押します。

1. 何らかの追加コードをアプリに追加しましょう。 `Console.WriteLine("Hello World!")` という行の前に次の Visual Basic コードを追加します。

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   このコードはコンソール ウィンドウに **What is your name?** と表示し、ユーザーがテキストを入力して **Enter** キーを押すまで待機します。

1. `Console.WriteLine("Hello World!")` という行を次のコードに変更します。

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. **Ctrl**+**F5** キーを押してプログラムを再び実行します。

   Visual Studio によってアプリが再度ビルドされ、コンソール ウィンドウが開き、名前を入力するように求められます。

1. コンソール ウィンドウに名前を入力し、**Enter** キーを押します。

   ![コンソール ウィンドウの入力](../media/overview-console-input.png)

1. 任意のキーを押してコンソール ウィンドウを閉じ、プログラムの実行を停止します。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio のメニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選びます。 (または、**Ctrl** + **Shift** + **N** キーを押します。)

    :::image type="content" source="media/vs-2019/file-new-project.png" alt-text="Visual Studio 2019 メニュー バーから [ファイル] > [新規作成] > [プロジェクト] の順に選択するスクリーンショット。":::

   **[新しいプロジェクトの作成]** ウィンドウが開き、いくつかのプロジェクト "*テンプレート*" が表示されます。 テンプレートには、特定のプロジェクトの種類に必要な基本的なファイルと設定が含まれています。

1. 必要なテンプレートを検索するには、検索ボックスに「**.net core コンソール**」と入力します。 使用可能なテンプレートの一覧が、入力したキーワードに基づいて自動的にフィルター処理されます。 **[すべての言語]** ドロップダウン リストから **[Visual Basic]** を選択し、 **[すべてのプラットフォーム]** リストから **[Windows]** を選択し、 **[すべてのプロジェクトの種類]** リストから **[コンソール]** を選択することで、テンプレートの結果をさらにフィルター処理できます。

   **[コンソール アプリケーション]** テンプレートを選択し、 **[次へ]** をクリックします。

    :::image type="content" source="media/vs-2019/create-new-project.png" alt-text="Visual Studio 2019 の [新しいプロジェクトの作成] ウィンドウのスクリーンショット。ここで必要なテンプレートを選択します。":::

1. **[新しいプロジェクトの構成]** ウィンドウで、 **[プロジェクト名]** ボックスに「**HelloWorld**」と入力し、必要に応じてプロジェクト ファイルのディレクトリの場所 (既定の場所は `C:\Users\<name>\source\repos`) を変更した後、 **[次へ]** をクリックします。

    :::image type="content" source="media/vs-2019/configure-new-project.png" alt-text="Visual Studio 2019 の [新しいプロジェクトの構成] ウィンドウのスクリーンショット。ここでプロジェクトの名前を入力します。":::

1. **[追加情報]** ウィンドウで、 **[ターゲット フレームワーク]** ドロップダウン メニューに **[.NET Core 3.1]** が表示されていることを確認し、 **[作成]** をクリックします。

    :::image type="content" source="media/vs-2019/create-project-additional-info.png" alt-text="Visual Studio 2019 の [追加情報] ウィンドウのスクリーンショット。ここで必要な .NET Core フレームワークのバージョンを選択します。":::

   Visual Studio によってプロジェクトが作成されます。 これは、リテラル文字列 "Hello World!" を表示する <xref:System.Console.WriteLine?displayProperty=nameWithType> メソッドを呼び出す単純な "Hello World" アプリケーションです。 コンソール (プログラムの出力) ウィンドウでに表示されます。

   すぐに次のようなグラフが表示されます。

   ![Visual Studio IDE](media/overview-ide-console-app.png)

   アプリの Visual Basic コードは、領域の大部分を占めるエディター ウィンドウに表示されます。 キーワードや型など、コードの異なる部分を示すようにテキストが自動的に色分けされているのに注目してください。 また、コードの縦の小さな点線は互いに一致する括弧を示し、行番号は後でコードの場所を探すのに役立ちます。 小さな四角で囲まれたマイナス記号を選択するとコード ブロックが折りたたまれ、折りたたまれている場合は展開できます。 このコードのアウトライン機能を使用すると、必要のないコードを非表示にして画面を整理できます。 プロジェクト ファイルは右側の **ソリューション エクスプローラー** と呼ばれるウィンドウに一覧表示されます。

   ![赤色のボックスを持つ Visual Studio IDE](media/overview-ide-console-app-red-boxes.png)

   他にもメニューやツール ウィンドウが用意されていますが、今は次に進みましょう。

1. アプリを起動します。 そのためには、メニュー バーの **[デバッグ]** メニューから **[デバッグなしで開始]** を選択します。 あるいは、**Ctrl**+**F5 キー** を押します。

   ![[デバッグ]、[デバッグなしで開始] メニューを選択](media/vs-2019/start-without-debugging.png)

   Visual Studio でアプリがビルドされ、コンソール ウィンドウが開き、メッセージ **Hello World!** が表示されます。 これで実行中のアプリができました。

   ![Hello World メッセージを表示しているコンソール ウィンドウのスクリーンショット。](../media/vs-2019/overview-console-window.png)

1. コンソール ウィンドウを閉じるには、キーボードで任意のキーを押します。

1. 何らかの追加コードをアプリに追加しましょう。 `Console.WriteLine("Hello World!")` という行の前に次の Visual Basic コードを追加します。

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   このコードはコンソール ウィンドウに **What is your name?** と表示し、ユーザーがテキストを入力して **Enter** キーを押すまで待機します。

1. `Console.WriteLine("Hello World!")` という行を次のコードに変更します。

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. **Ctrl**+**F5** キーを押してプログラムを再び実行します。

   Visual Studio によってアプリが再度ビルドされ、コンソール ウィンドウが開き、名前を入力するように求められます。

1. コンソール ウィンドウに名前を入力し、**Enter** キーを押します。

   ![What is your name の質問とアプリの応答が表示されているコンソール ウィンドウのスクリーンショット。](../media/vs-2019/overview-console-input.png)

1. 任意のキーを押してコンソール ウィンドウを閉じ、プログラムの実行を停止します。

::: moniker-end

## <a name="use-refactoring-and-intellisense"></a>リファクタリングと IntelliSense の使用

[リファクタリング](../../ide/refactoring-in-visual-studio.md)と [IntelliSense](../../ide/using-intellisense.md) がより効率的なコーディングに役立ついくつかの方法を見てみましょう。

最初に、変数 `name` の名前を変更します。

1. 変数 `name` をダブルクリックして選択します。

2. 変数の新しい名前として「**username**」と入力します。

   変数の周りに灰色のボックスが表示され、余白に電球が表示されることに注意してください。

3. 電球アイコンを選択して、使用可能な[クイック アクション](../../ide/quick-actions.md)を表示します。 **['name' から 'username' へ名前を変更]** を選択します。

   ![Visual Studio での名前変更アクション](media/rename-quick-action.png)

   プロジェクト全体で変数の名前が変更され、この場合は 2 か所だけです。

4. 次は IntelliSense を試してみましょう。 `Console.WriteLine("Hello &quot; + username + &quot;!")` という行の下に、次のコード フラグメントを入力します。

    ```vb
   Dim now = Date.
   ```

   ボックスに <xref:System.DateTime> クラスのメンバーが表示されます。 さらに、現在選択されているメンバーの説明が独立したボックスに表示されます。

   ![Visual Studio での IntelliSense リスト メンバー](media/intellisense-list-members.png)

5. クラスのプロパティである **Now** という名前のメンバーを選択します。それをダブルクリックするか、上下の矢印キーを使用して選択した後 **Tab** キーを押します。

6. その下に、次のコード行を入力するか貼り付けます。

   ```vb
   Dim dayOfYear = now.DayOfYear
   Console.Write("Day of year: ")
   Console.WriteLine(dayOfYear)
   ```

   > [!TIP]
   > <xref:System.Console.Write%2A?displayProperty=nameWithType> は <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> と少し異なり、出力の後に行終端記号を追加しません。 つまり、次に出力に送信されるテキストは、同じ書き出されます。 コードでこれらのメソッドをポイントすると、その説明が表示されます。

7. 次に、もう一度リファクタリングを使ってコードを少し簡単にします。 `Dim now = Date.Now` の行で変数 `now` をクリックします。

   その行の余白に小さいドライバー アイコンが表示されることに注意してください。

8. ドライバー アイコンをクリックして、Visual Studio で使用可能な推奨事項を確認します。 この場合は、コードの全体の動作を変更することなくコードの行を削除する[インラインの一時変数](../../ide/reference/inline-temporary-variable.md)リファクタリングが表示されています。

   ![Visual Studio でのインラインの一時変数リファクタリング](media/inline-temporary-variable-refactoring.png)

9. **[インラインの一時変数]** をクリックしてコードをリファクタリングします。

::: moniker range="vs-2017"

10. **Ctrl**+**F5** キーを押してプログラムを再び実行です。 出力は次のようになります。

    ![プログラムの出力が表示されたコンソール ウィンドウ](../media/overview-console-final.png)

::: moniker-end

::: moniker range=">=vs-2019"

10. **Ctrl**+**F5** キーを押してプログラムを再び実行です。 出力は次のようになります。

    ![プログラムの出力が表示されたコンソール ウィンドウ](../media/vs-2019/overview-console-final.png)

::: moniker-end

## <a name="debug-code&quot;></a>コードのデバッグ

コードを記述するときは、実行してバグの存在を確認するために実際にテストする必要があります。 Visual Studio のデバッグ システムを使用すると、一度に 1 つのステートメントずつ、コードを実行して必要に応じて変数を検査できます。 特定の行でコードの実行を停止する &quot;*ブレークポイント*&quot; を設定できます。 コードが実行されたときに変数の値がどのように変わるかなどを確認できます。

ブレークポイントを設定して、プログラムが &quot;実行中&quot; の `username` 変数の値を見てみましょう。

1. `Console.WriteLine(&quot;Hello &quot; + username + &quot;!")` というコード行を探します。 この行にブレークポイントを設定するには、つまりこの行でプログラムの実行を一時停止するには、エディターの左端の余白をクリックします。 コード行の任意の場所をクリックしてから、**F9** キーを押してもかまいません。

   余白の左端に赤い円が表示され、コードが赤で強調表示されます。

   ![Visual Studio でのコード行のブレークポイント](media/breakpoint.png)

1. **[デバッグ]**  >  **[デバッグの開始]** を選択するか、**F5** キーを押して、デバッグを開始します。

1. コンソール ウィンドウが表示されて名前を要求されたら、入力して **Enter** キーを押します。

   Visual Studio コード エディターにフォーカスが戻り、ブレークポイントを設定したコード行が黄色で強調表示されます。 これは、プログラムが実行する次のコード行を示します。

1. `username` 変数をポイントすると、その値が表示されます。 または、`username` を右クリックして **[ウォッチを追加]** を選択し、変数を **[ウォッチ]** ウィンドウに追加して、そこで値を確認することもできます。

   ![Visual Studio でのデバッグ中の変数の値](media/debugging-variable-value.png)

1. プログラムを最後まで実行するには、**F5** キーを再び押します。

Visual Studio でのデバッグの詳細については、[デバッガーの機能ツアー](../../debugger/debugger-feature-tour.md)に関するページをご覧ください。

## <a name="next-steps"></a>次の手順

以下の入力記事のいずれかに従って、Visual Studio をさらに詳しく調べます。

> [!div class="nextstepaction"]
> [コード エディターの使用方法について学習する](tutorial-editor.md)

> [!div class="nextstepaction"]
> [プロジェクトとソリューションについて学習する](tutorial-projects-solutions.md)

## <a name="see-also"></a>関連項目

- [Visual Studio のその他の機能](../../ide/advanced-feature-overview.md)を確認します
- [visualstudio.microsoft.com](https://visualstudio.microsoft.com/vs/) にアクセスします
- [Visual Studio ブログ](https://devblogs.microsoft.com/visualstudio/)を参照します
