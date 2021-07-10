---
title: 'チュートリアル: C# 開発者の編集'
description: この 10 分間の Visual Studio のコード エディターの紹介では、C# でコードを記述、コード内を移動、およびコードを理解する簡単な方法をいくつか説明します。
ms.custom: vs-acquisition, get-started
ms.date: 11/20/2018
ms.technology: vs-ide-general
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 2a6b01e9c26ea816e05a1d2186d904bdb080f098
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390256"
---
# <a name="learn-to-use-the-code-editor-with-c"></a>C でコード エディターを使用する方法を学習する\#

この 10 分間の Visual Studio のコード エディターの紹介では、ファイルにコードを追加した上で、Visual Studio でコードを記述、コード内を移動、および C# コードを理解する簡単な方法をいくつか説明します。

::: moniker range="vs-2017"

> [!TIP]
> Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2022"

Visual Studio 2022 プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

この記事では、既に C# を使い慣れていることを前提としています。 使い慣れていない場合は、最初に [Visual Studio での C# と ASP.NET Core の概要](tutorial-aspnet-core.md)などのチュートリアルに関するページを参照することをお勧めします。

> [!TIP]
> この記事に従うには、Visual Studio に対して C# 設定が選択されていることを確認します。 統合開発環境 (IDE) の設定の選択については、「[Select environment settings (環境設定を選択する)](visual-studio-ide.md#select-environment-settings)」 を参照してください。

## <a name="create-a-new-code-file"></a>新しいコード ファイルを作成する

新しいファイルを作成し、何らかのコードをそのファイルに追加することから始めます。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。 スタート ウィンドウで **Esc** キーを押すか、または **[コードなしで続行]** をクリックして、開発環境を開きます。

::: moniker-end

2. メニュー バーの **[ファイル]** メニューから、 **[新規作成]**  >  **[ファイル]** を選択するか、**Ctrl**+**N** キーを押します。

3. **[新しいファイル]** ダイアログ ボックスの **[全般]** カテゴリで、 **[Visual C# クラス]** を選択し、 **[開く]** を選択します。

   エディターで新しいファイルが開かれ、C# クラスのスケルトンが表示されます。 (コード エディターによって提供される利点の一部を活用するために、完全な Visual Studio プロジェクトを作成する必要はありません。必要なのはコード ファイルだけです)

   ![Visual Studio での C# コード ファイル](../media/tutorial-editor.png)

## <a name="use-code-snippets"></a>コード スニペットを使用する

Visual Studio で提供されている便利な *コード スニペット* を使用すると、一般的に使用されるコード ブロックを迅速かつ簡単に生成することができます。 [コード スニペット](../../ide/code-snippets.md)は、C#、Visual Basic、C++ など、さまざまなプログラミング言語で使用することができます。 C# `void Main` スニペットをファイルに追加してみましょう。

1. ファイル内の最後の閉じかっこ **}** のちょうど上にカーソルを置き、文字 `svm` を入力します (これは、`static void Main`&mdash; の略ですが、その意味が分からなくても、あまり心配しないでください)。

   ポップアップ ダイアログ ボックスが `svm` コード スニペットに関する情報を伴って表示されます。

   ![Visual Studio でのコード スニペット用の IntelliSense](../media/tutorial-intellisense-snippet.png)

1. **Tab** キーを 2 回押すと、コード スニペットが挿入されます。

   `static void Main()` メソッドの署名がファイルに追加されているのがわかります。 [Main()](/dotnet/csharp/programming-guide/main-and-command-args/) メソッドは、C# アプリケーションのエントリ ポイントです。

利用できるコード スニペットは、プログラミング言語によって異なります。 目的の言語で使用可能なコード スニペットを確認するには、 **[編集]**  >  **[IntelliSense]**  >  **[スニペットの挿入]** の順に選択するか、**Ctrl**+**K**、**Ctrl**+**X** キーを押して、言語のフォルダーを選択します。 C# の場合、リストは次のようになります。

![C# コード スニペットのリスト](../media/tutorial-code-snippet-list.png)

このリストには、[クラス](/dotnet/csharp/programming-guide/classes-and-structs/classes)、[コンストラクター](/dotnet/csharp/programming-guide/classes-and-structs/constructors)、[for](/dotnet/csharp/language-reference/keywords/for) ループ、[if](/dotnet/csharp/language-reference/keywords/if-else) ステートメント、[switch](/dotnet/csharp/language-reference/keywords/switch) ステートメントなどを作成するためのスニペットが含まれています。

## <a name="comment-out-code"></a>コメント アウト コード

ツールバー (Visual Studio のメニュー バーの下にあるボタンの列) は、コード作成時の生産性を高めるのに役立ちます。 たとえば、IntelliSense 補完モードの切り替え (特に、[IntelliSense](../../ide/using-intellisense.md) は、一致するメソッドの一覧を表示するコーディング支援機能)、行のインデントの増減、またはコンパイルしたくないコードをコメント アウトを行うことができます。 このセクションでは、一部のコードをコメント アウトします。

![エディターのツール バー](../media/tutorial-editor-toolbar.png)

1. `Main()` メソッド本体に次のコードを貼り付けます。

    ```csharp
    // _words is a string array that we'll sort alphabetically
    string[] _words = {
        "the",
        "quick",
        "brown",
        "fox",
        "jumps"
    };

    string[] morewords = {
        "over",
        "the",
        "lazy",
        "dog"
    };

    IEnumerable<string> query = from word in _words
                                orderby word.Length
                                select word;
    ```

1. `morewords` 変数は現在使用していませんが、後で使用するかもしれないので、完全に削除したくありません。 そこで、これらの行をコメント アウトしましょう。 終了セミコロンまでの `morewords` の定義全体を選択し、ツールバーの **[選択された行をコメント アウトします。]** ボタンを選択します。 キーボードを使用する場合は、**Ctrl**+**K** キー、**Ctrl**+**C** キーを押します。

   ![コメント アウト ボタン](../media/tutorial-comment-out.png)

   選択した各列の先頭に C# コメント文字 `//` を追加すると、コードがコメント アウトされます。

## <a name="collapse-code-blocks"></a>コード ブロックを折りたたむ

生成された [constructor](/dotnet/csharp/programming-guide/classes-and-structs/constructors) for `Class1` の空のコンストラクターは表示したくありません。コードのビューを整理するために、ビューを折りたたみましょう。 コンストラクターの最初の行の余白にある、内部にマイナス記号が表示された小さな灰色のボックスを選択します。 または、キーボードを使用している場合は、コンストラクター コード内の任意の場所にカーソルを置き、**Ctrl**+**M** キー、**Ctrl**+**M** キーを押します。

![アウトライン折りたたみボタン](../media/tutorial-collapse.png)

コード ブロックが最初の行に折りたたまれ、後続に省略記号 (`...`) が表示されます。 コード ブロックを再度展開するには、現在内部にプラス記号が表示されている同じ灰色のボックスをクリックするか、**Ctrl**+**M** キー、**Ctrl**+**M** キーをもう一度押します。 これは、[アウトライン](../../ide/outlining.md)機能と呼ばれ、長いメソッドまたはクラス全体を折りたたむ場合に特に便利です。

## <a name="view-symbol-definitions"></a>シンボル定義の表示

Visual Studio エディターでは、型やメソッドなどの定義の検査を容易に行うことができます。1 つの方法として、たとえば、シンボルが参照されている任意の場所で **[定義へ移動]** を選択するか **F12** キーを押して、定義を含むファイルに移動します。 作業中のファイルからフォーカスを移動しないより迅速な方法としては、[[定義をここに表示]](../../ide/go-to-and-peek-definition.md#peek-definition) を使用します。 `string` 型の定義を参照してみましょう。

1. `string` が出現している箇所を右クリックし、コンテンツ メニューから **[定義をここに表示]** を選択します。 または、**Alt**+**F12** キーを押します。

   `String` クラスの定義を含むポップアップ ウィンドウが表示されます。 ポップアップ ウィンドウ内をスクロールすることも、参照しているコードから別の種類の定義を参照することもできます。

   ![コード定義ウィンドウ](../media/tutorial-peek-definition.png)

1. 表示された定義ウィンドウを閉じるには、ポップアップ ウィンドウの右上にある、内部に "x" が表示された小さなボックスを選択します。

## <a name="use-intellisense-to-complete-words"></a>IntelliSense を使用した入力補完

コードを記述する場合、[IntelliSense](../../ide/using-intellisense.md) は貴重なリソースです。 このリソースでは、使用可能な型のメンバーに関する情報、またはメソッドの各種オーバーロードのためのパラメーターの詳細を表示できます。 また、IntelliSense を使用すると、単語を区別するために十分な文字を入力した後に入力補完を利用することができます。 プログラムからの出力が表示される標準的な場所であるコンソール ウィンドウに、順序付けされた文字列を出力するコード行を追加してみましょう。

1. `query` 変数の下で、次のコードの入力を開始します。

   ```csharp
   foreach (string str in qu
   ```

   IntelliSense が `query` シンボルに関する **クイック ヒント** を表示しているのがわかります。

   ![Visual Studio での IntelliSense の入力候補](../media/tutorial-intellisense-completion-list.png)

1. IntelliSense の "入力候補" 機能を使用して単語 `query` の残りを挿入するには、**Tab** キーを押します。

1. 次のコードのように、コード ブロックを完成させます。 コード スニペットを使用して再度実行することもできます。それには、`cw` を入力してから、**Tab** キーを 2 回押して、`Console.WriteLine` コードを生成します。

   ```csharp
   foreach (string str in query)
   {
      Console.WriteLine(str);
   }
   ```

## <a name="refactor-a-name"></a>名前のリファクタリング

だれも最初から適切なコードは記述できないものです。変更を必要とする可能性のある要素の 1 つに、変数またはメソッドの名前があります。 Visual Studio の[リファクタリング](../../ide/refactoring-in-visual-studio.md)機能を使用して、`_words` 変数の名前を `words` に変更してみましょう。

1. `_words` 変数の定義にカーソルを置き、右クリックまたはコンテキスト メニューから **[名前の変更]** を選択するか、**Ctrl**+**R** キー、**Ctrl**+**R** キーを押します。

   エディターの右上に **[名前の変更]** ダイアログ ボックスがポップアップ表示されます。

1. 目的の名前 **words** を入力します。 クエリ内の `words` への参照も名前が自動的に変更されることに注意してください。 **Enter** キーを押す前に、 **[名前の変更]** ポップアップ ボックスで **[コメントを含める]** チェック ボックスを選択します。

   ![[名前の変更] ダイアログ ボックス](../media/tutorial-rename.png)

1. **Enter** キーを押します。

   `words` の出現箇所とコード コメント内の `words` への参照箇所の両方で名前が変更されました。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [プロジェクトとソリューションについて学習する](../tutorial-projects-solutions.md)

## <a name="see-also"></a>関連項目

- [コード スニペット](../../ide/code-snippets.md)
- [コード間の移動](../../ide/navigating-code.md)
- [アウトライン](../../ide/outlining.md)
- [[定義へ移動] と [定義をここに表示]](../../ide/go-to-and-peek-definition.md)
- [リファクタリング](../../ide/refactoring-in-visual-studio.md)
- [IntelliSense を使用する](../../ide/using-intellisense.md)
