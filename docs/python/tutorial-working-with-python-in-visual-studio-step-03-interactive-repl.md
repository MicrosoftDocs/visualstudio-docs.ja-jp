---
title: Visual Studio での Python チュートリアル、手順 3、対話型 REPL
titleSuffix: ''
description: Visual Studio での Python 機能の中核となるチュートリアルの手順 3 では、Python の対話型 REPL ウィンドウについて説明します。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: e82073b77231f84452ba51402f407904142bbf8e
ms.sourcegitcommit: 925db7adb9cb554b081c7e727d09680d4863feed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "107941098"
---
# <a name="step-3-use-the-interactive-repl-window"></a>手順 3: 対話型 REPL ウィンドウを使用する

**前の手順:[コードを記述して実行する](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)**

Visual Studio の Python 用 **対話型** ウィンドウによって機能豊富な REPL (読み取り、評価、出力ループ) エクスペリエンスが実現され、通常の編集、ビルド、デバッグのサイクルが大幅に短縮されます。 **対話型** ウィンドウは、Python のコマンド ラインの REPL エクスペリエンスのすべての機能を提供します。 これは、コマンド ラインからでは面倒な、Visual Studio エディターのソース ファイルでのコード交換も容易にします。

> [!NOTE]
> REPL の問題については、確実に `ipython` パッケージと `ipykernel` パッケージをインストールしてください。また、パッケージのインストールのヘルプについては、[Python 環境のパッケージ タブ](./python-environments-window-tab-reference.md#packages-tab)に関する記事を参照してください。

1. **ソリューション エクスプローラー** で、(前の図で示した **Python 3.6 (32-bit)** などのような) プロジェクトの Python 環境を右クリックして、**[対話型ウィンドウを開く]** を選択して **対話型** ウィンドウを開きます。 Visual Studio のメイン メニューで、**[表示]** > **[その他のウィンドウ]** > **[Python Interactive ウィンドウ]** を選択することも可能です。

1. **対話型** ウィンドウが、エディターの下で、標準の Python REPL プロンプト (**>>>**) と共に開きます。 **[環境]** ドロップダウン リストを使用して、操作する特定のインタープリターを選択できます。 **対話型** ウィンドウのサイズを大きくすることもできます。その場合には、2 つのウィンドウ間の区切りをドラッグします。

    ![Python の対話型ウィンドウとサイズ変更のためのそれのドラッグ](media/vs-getting-started-python-11-interactive1b.png)

    > [!Tip]
    > Visual Studio のすべてのウィンドウのサイズは、境界の区切りをドラッグしてサイズ変更できます。 Visual Studio のフレームから個々にウィンドウをドラッグして、フレーム内で自由に再配置することも可能です。 詳細については、「[ウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」をご覧ください。

1. ステートメント (`print("Hello, Visual Studio")` など) や式 (`123/456` など) をいくつか入力して、すぐに表示される結果を確認します。

    ![Python Interactive ウィンドウの即時の結果](media/vs-getting-started-python-12-interactive2.png)

1. 複数行ステートメント (関数の定義など) を記述し始めると、 **[インタラクティブ]** ウィンドウに行の継続を示す Python の **...** プロンプトが表示されます。これは、コマンド ライン REPL とは異なり、自動的にインデントされます。 新しい **...** 行を追加するには、`Shift+Enter` を押します。

    ![ステートメントの継続を示す Python Interactive ウィンドウ](media/vs-getting-started-python-13-interactive3.png)

1. **対話型** ウィンドウでは、入力内容がすべて履歴に残されます。複数行の履歴項目により、コマンドライン REPL の機能が強化されています。 たとえば、関数を行ごとに再作成するのではなく、`f` 関数の定義全体を単一ユニットとして呼び出して、名前を `make_double` に変更することが簡単にできます。

1. Visual Studio では、エディター ウィンドウから **対話型** ウィンドウに、複数のコード行を送信できます。 この機能を使用すると、ソース ファイル内のコードを維持し、その選択された一部を **対話型** ウィンドウに簡単に送信できます。 それから、プログラム全体を実行するのではなく、迅速な REPL 環境でそれらのコード フラグメントを使用して作業できます。 この機能を参照するには、次を使用して *PythonApplication1.py* ファイルの `for` ループをまず置き換えます。

    ```python
    # Create a string with spaces proportional to a cosine of x in degrees
    def make_dot_string(x):
        return ' ' * int(20 * cos(radians(x)) + 20) + 'o'
    ```

1. *.py* ファイルの `import`、`from`、および `make_dot_string` 関数のステートメントを選択します。 選択したテキストを右クリックし、 **[Interactive に送信]** を選択します (または **Ctrl** + **Enter** キーを押します)。 コードの断片がすぐに **対話型** ウィンドウに貼り付けられて、実行されます。 コードでは関数が定義されているため、数回呼び出すことですばやくその関数をテストすることができます。

    ![対話型ウィンドウへのコードの送信とそのテスト](media/vs-getting-started-python-14-interactive4.png)

    > [!Tip]
    > "*選択せずに*" エディターで **Ctrl**+**Enter** キーを押すと、**対話型** ウィンドウで現在のコード行が実行され、次の行にカーソルが自動的に配置されます。 この機能により、繰り返し **Ctrl**+**Enter** キーを押すことで、Python コマンド ラインのみでは不可能なコードのステップ実行を簡単に実行できます。 また、これでは、デバッガーを実行しなくても、また必ずしも最初からプログラムを開始しなくてもコードをステップ実行できます。

1. また、下のスニペットなどの任意のソースから **対話型** ウィンドウへ、コードを複数行コピーしたり貼り付けることも可能です。これは Python のコマンド ラインの REPL から実行するのは困難です。 コードを貼り付けると、**対話型** ウィンドウはそれが入力されたかのようにそのコードを実行します。

    ```python
    for i in range(360):
        s = make_dot_string(i)
        print(s)
    ```

    ![[Interactive に送信] を使用した複数行のコードの貼り付け](media/vs-getting-started-python-15-interactive5.png)

1. ご覧のように、このコードは問題なく動作しますが、その出力はあまりよくはありません。 `for` ループに別のステップ実効値を入れると、より余弦波のようになります。 幸い、`for` ループ全体が単一ユニットとして REPL の履歴にあるため、簡単に関数に戻って変更を加え、再テストすることができます。 まず上向き矢印キーを押して、`for` ループを呼び出します。 次いで、左または右の矢印を押して、コード内を移動します (これを行うまで、上および下矢印は履歴内を循環します)。 移動し、`range` 仕様を `range(0, 360, 12)` に変更します。 次いで (コードの任意の場所で) **Ctrl**+**Enter** キーを押し、ステーメント全体を再実行します。

    ![対話型のウィンドウでの前のステートメントの編集](media/vs-getting-started-python-16-interactive6.png)

1. この手順を繰り返し、最適な値が見つかるまで、別のステップ設定を試します。 たとえば、`range(0, 1800, 12)` のように範囲を長くして波を繰り返すことも可能です。

1. **インタラクティブ** ウィンドウに記述したコードに問題がなければ、それを選択します。 次に、コードを右クリックして **[コードのコピー]** を選択します (**Ctrl** + **Shift** + **C** キー)。 最後に、選択したコードをエディターに貼り付けます。 Visual Studio のこの特殊機能が、任意の出力や `>>>` と `...` のプロンプトを自動的に除外することに注目してください。 たとえば、次の図は、プロンプトと出力を含む選択に対し、**[コードのコピー]** コマンドを使用しているところを示しています。

    ![プロンプトと出力を含む選択での対話型ウィンドウでのコードのコピー コマンド](media/vs-getting-started-python-17-interactive7.png)

    エディターに貼り付けると、コードのみが得られます。

    ```python
    for i in range(0, 1800, 12):
        s = make_dot_string(i)
        print(s)
    ```

    プロンプトと出力などを含め、**対話型** ウィンドウの内容を正確にコピーする場合、標準の **コピー** コマンドを使用します。

1. ここでは、**対話型** ウィンドウの迅速な REPL 環境を使用して、小規模なコードの詳細を処理し、そのコードをプロジェクトのソース ファイルに追加しました。 **Ctrl**+**F5** キー (または **[デバッグ]**  >  **[デバッグなしで開始]** ) を使用してコードを今再実行した場合、期待した正確な結果を得られます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [デバッガーでコードを実行する](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)

## <a name="go-deeper"></a>詳しい説明

- [対話型ウィンドウの使用](python-interactive-repl-in-visual-studio.md)
- [IPython REPL の使用](interactive-repl-ipython.md)