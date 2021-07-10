---
title: Visual Basic 開発者向けの編集の概要
description: この 10 分間の Visual Studio のコード エディターの紹介では、Visual Basic でコードを記述、コード内を移動、およびコードを理解する簡単な方法をいくつか説明します。
ms.custom:
- vs-acquisition
- seodec18
- get-started
ms.date: 11/20/2018
ms.technology: vs-ide-general
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: fe411074c95db15fde4819ffb07eca39a05e844d
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390165"
---
# <a name="learn-to-use-the-code-editor-with-visual-basic"></a>Visual Basic でコード エディターを使用する方法を学習する

この 10 分間の Visual Studio のコード エディターの紹介では、ファイルにコードを追加した上で、Visual Studio でコードを記述、コード内を移動、および Visual Basic コードを理解する簡単な方法をいくつか説明します。

::: moniker range="vs-2017"

> [!TIP]
> Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

> [!TIP]
> Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2022"

> [!TIP]
> Visual Studio プレビューをまだインストールしていない場合は、[Visual Studio 2022 プレビューのダウンロード](https://visualstudio.microsoft.com/vs/preview/vs2022) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

この記事では、既に Visual Basic を使い慣れていることを前提としています。 使い慣れていない場合は、最初に [Visual Studio の Visual Basic の概要](../../get-started/visual-basic/tutorial-console.md)などのチュートリアルに関するページを参照することをお勧めします。

> [!TIP]
> この記事に従うには、Visual Studio に対して Visual Basic 設定が選択されていることを確認します。 統合開発環境 (IDE) の設定の選択については、「[Select environment settings (環境設定を選択する)](visual-studio-ide.md#select-environment-settings)」 を参照してください。

## <a name="create-a-new-code-file"></a>新しいコード ファイルを作成する

新しいファイルを作成し、何らかのコードをそのファイルに追加することから始めます。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。 スタート ウィンドウで **Esc** キーを押すか、または **[コードなしで続行]** をクリックして、開発環境を開きます。

::: moniker-end

2. メニュー バーの **[ファイル]** メニューから、 **[新しいファイル]** を選択します。

3. **[新しいファイル]** ダイアログ ボックスの **[全般]** カテゴリで、 **[Visual Basic クラス]** を選び、 **[開く]** を選択します。

   エディターで新しいファイルが開かれ、Visual Basic クラスのスケルトンが表示されます (既にお気付きのとおり、構文の強調表示など、コード エディターによって提供されるいくつかの利点を得るために、完全な Visual Studio プロジェクトを作成する必要はありません。 必要なのはコード ファイルだけです)。

   ![Visual Studio での Visual Basic コード ファイル](media/tutorial-editor.png)

## <a name="use-code-snippets"></a>コード スニペットを使用する

Visual Studio で提供されている便利な *コード スニペット* を使用すると、一般的に使用されるコード ブロックを迅速かつ簡単に生成することができます。 [コード スニペット](../../ide/code-snippets.md)は、Visual Basic、C#、C++ など、さまざまなプログラミング言語で使用することができます。 Visual Basic の **Sub** スニペットをファイルに追加してみましょう。

1. `End Class` と示されている行の上にカーソルを置き、「**sub**」と入力します。

   ポップアップ ダイアログ ボックスが表示され、`Sub` キーワードに関する情報と **Sub** コード スニペットの挿入方法が示されます。

   ![Visual Studio でのコード スニペット用の IntelliSense](media/tutorial-intellisense-snippet.png)

1. **Tab** キーを 2 回押すと、コード スニペットが挿入されます。

   Sub プロシージャ `MySub()` のアウトラインがファイルに追加されます。

利用できるコード スニペットは、プログラミング言語によって異なります。 **[編集]**  >  **[IntelliSense]**  >  **[スニペットの挿入]** を選択 (または **Ctrl**+**K**、**Ctrl**+**X** キーを押す) ことで、Visual Basic で使用可能なコード スニペットを確認できます。 Visual Basic の場合、コード スニペットは次のカテゴリで使用できます。

![Visual Basic のコード スニペットのリスト](media/tutorial-code-snippet-list.png)

コンピューター上にファイルが存在するかどうかの判断、テキスト ファイルへの書き込み、レジストリ値の読み取り、SQL クエリの実行、[For Each...Next ステートメント](/dotnet/visual-basic/language-reference/statements/for-each-next-statement)の作成などを行うためのスニペットがあります。

## <a name="comment-out-code"></a>コメント アウト コード

ツールバー (Visual Studio のメニュー バーの下にあるボタンの列) は、コード作成時の生産性を高めるのに役立ちます。 たとえば、IntelliSense 完了モードの切り替え、行のインデントの増減、コンパイルしたくないコードのコメント アウトを行うことができます ([IntelliSense](../../ide/using-intellisense.md) は、特に、一致するメソッドのリストを表示するコーディング支援機能です)。このセクションでは、一部のコードをコメント アウトします。

![エディターのツールバー ボタン](media/tutorial-editor-toolbar.png)

1. `MySub()` プロシージャ本体に次のコードを貼り付けます。

   ```vb
   ' _words is a string array that we'll sort alphabetically
   Dim _words = New String() {
   "the",
   "quick",
   "brown",
   "fox",
   "jumps"
   }

   Dim morewords = New String() {
   "over",
   "the",
   "lazy",
   "dog"
   }

   Dim query = From word In _words
               Order By word.Length
               Select word
   ```

1. ここでは `morewords` 配列は使用していませんが、後で使用するかもしれないので、完全に削除したくありません。 そこで、これらの行をコメント アウトしましょう。 右中かっこまでの `morewords` の定義全体を選択し、ツールバーの **[選択された行をコメント アウトします。]** ボタンを選びます。 キーボードを使用する場合は、**Ctrl**+**K** キー、**Ctrl**+**C** キーを押します。

   ![コメント アウト ボタン](media/tutorial-comment-out.png)

   選択した各行の先頭に Visual Basic コメント文字 `'` を追加すると、コードがコメント アウトされます。

## <a name="collapse-code-blocks"></a>コード ブロックを折りたたむ

コードのセクションを折りたたみ、関心のある部分だけに集中することができます。 実践するために、`_words` 配列を 1 行のコードに折りたたんでみましょう。 `Dim _words = New String() {` と示されている行の余白にある、内部にマイナス記号が表示された小さな灰色のボックスを選択します。 または、キーボードを使用している場合は、配列定義の任意の場所にカーソルを置き、**Ctrl**+**M** キー、**Ctrl**+**M** キーを押します。

![アウトライン折りたたみボタン](media/tutorial-collapse.png)

コード ブロックが最初の行に折りたたまれ、後続に省略記号 (`...`) が表示されます。 コード ブロックを再度展開するには、現在内部にプラス記号が表示されている同じ灰色のボックスをクリックするか、**Ctrl**+**M** キー、**Ctrl**+**M** キーをもう一度押します。 これは、[アウトライン](../../ide/outlining.md)機能と呼ばれ、長いメソッドまたはクラス全体を折りたたむ場合に特に便利です。

## <a name="view-symbol-definitions"></a>シンボル定義の表示

Visual Studio エディターでは、型やメソッドなどの定義の検査を容易に行うことができます。1 つの方法として、たとえば、シンボルが参照されている任意の場所で **[定義へ移動]** を選択して、定義を含むファイルに移動します。 作業中のファイルからフォーカスを移動しないより迅速な方法としては、[[定義をここに表示]](../../ide/go-to-and-peek-definition.md#peek-definition) を使用します。 `String` 型の定義を参照してみましょう。

1. `String` という単語を右クリックし、コンテンツ メニューから **[定義をここに表示]** を選択します。 または、**Alt**+**F12** キーを押します。

   `String` クラスの定義を含むポップアップ ウィンドウが表示されます。 ポップアップ ウィンドウ内をスクロールすることも、参照しているコードから別の種類の定義を参照することもできます。

   ![コード定義ウィンドウ](media/tutorial-peek-definition.png)

1. 表示された定義ウィンドウを閉じるには、ポップアップ ウィンドウの右上にある、内部に "x" が表示された小さなボックスを選択します。

## <a name="use-intellisense-to-complete-words"></a>IntelliSense を使用した入力補完

コードを記述する場合、[IntelliSense](../../ide/using-intellisense.md) は貴重なリソースです。 このリソースでは、使用可能な型のメンバーに関する情報、またはメソッドの各種オーバーロードのためのパラメーターの詳細を表示できます。 また、IntelliSense を使用すると、単語を区別するために十分な文字を入力した後に入力補完を利用することができます。 プログラムからの出力が表示される標準的な場所であるコンソール ウィンドウに、順序付けされた文字列を出力するコード行を追加してみましょう。

1. `query` 変数の下で、次のコードの入力を開始します。

   ```vb
   For Each str In qu
   ```

   IntelliSense が `query` シンボルに関する **クイック ヒント** を表示しているのがわかります。

   ![Visual Studio での IntelliSense の入力候補](media/tutorial-intellisense-completion-list.png)

1. IntelliSense の "入力候補" 機能を使用して単語 `query` の残りを挿入するには、**Tab** キーを押します。

1. 次のコードのように、コード ブロックを完成させます。

   ```vb
   For Each str In query
       Console.WriteLine(str)
   Next
   ```

## <a name="refactor-a-name"></a>名前のリファクタリング

だれも最初から適切なコードは記述できないものです。変更を必要とする可能性のある要素の 1 つに、変数またはメソッドの名前があります。 Visual Studio の[リファクタリング](../../ide/refactoring-in-visual-studio.md)機能を使用して、`_words` 変数の名前を `words` に変更してみましょう。

1. `_words` 変数の定義にカーソルを置き、右クリックまたはコンテキスト メニューから **[名前の変更]** を選択します。

   エディターの右上に **[名前の変更]** ダイアログ ボックスがポップアップ表示されます。

1. `_words` 変数が選択された状態で、**words** の任意の名前を入力します。 クエリ内の `words` への参照も名前が自動的に変更されることに注意してください。 **Enter** キーを押すか、 **[適用]** をクリックする前に、 **[名前の変更]** ポップアップ ボックスで **[コメントを含める]** チェック ボックスをオンにします。

   ![[名前の変更] ダイアログ ボックス](media/tutorial-rename.png)

1. **Enter** キーを押すか、 **[適用]** をクリックします。

   `words` の出現箇所と、コード コメント内の `words` への参照箇所の両方で名前が変更されます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [プロジェクトとソリューションについて学習する](tutorial-projects-solutions.md)

## <a name="see-also"></a>関連項目

- [コード スニペット](../../ide/code-snippets.md)
- [コード間の移動](../../ide/navigating-code.md)
- [アウトライン](../../ide/outlining.md)
- [[定義へ移動] と [定義をここに表示]](../../ide/go-to-and-peek-definition.md)
- [リファクタリング](../../ide/refactoring-in-visual-studio.md)
- [IntelliSense を使用する](../../ide/using-intellisense.md)
