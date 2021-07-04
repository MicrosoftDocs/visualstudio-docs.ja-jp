---
title: Python Interactive ウィンドウ (REPL)
description: Visual Studio で Python コードを迅速に開発するために対話型ウィンドウ (REPL) を使用します。
ms.date: 02/11/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 21115673a41e26b2f1685442d2ed0ad93a147990
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254889"
---
# <a name="work-with-the-python-interactive-window"></a>Python 対話型ウィンドウの使用

Visual Studio では、各 Python 環境に向けて対話型の read-evaluate-print loop (REPL) ウィンドウが用意されています。これにより、コマンド ライン上の *python.exe* で得られる REPL が改善されます。 ( **[表示]**  >  **[その他のウィンドウ]**  >  **[&lt;環境&gt; インタラクティブ]** メニュー コマンドで開いた) **対話型** ウィンドウを使用すると、任意の Python コードを入力し、すぐに結果を確認することができます。 このコーディング方法は、API とライブラリの学習と実習、およびプロジェクトに含める作業コードを対話形式で開発するのに役立ちます。

![Python Interactive ウィンドウ](media/interactive-window.png)

Visual Studio では、複数の Python REPL モードから選ぶことができます。

| REPL | 説明 | 編集 | デバッグ | イメージ |
| --- | --- | --- | --- | --- |
| 標準 | 既定の REPL、Python と直接対話 | 標準的な編集 (複数行など)。 | はい、`$attach` を使用 | いいえ |
| デバッグ | 既定の REPL、デバッグ対象の Python プロセスと対話 | 標準的な編集 | デバッグのみ | いいえ |
| IPython | REPL は IPython のバックエンドと対話 | IPython コマンド、Pylab の利便性 | いいえ | はい、REPL でインライン |
| IPython (Pylab なし) | REPL は IPython のバックエンドと対話 | 標準的な IPython | いいえ | はい、別のウィンドウ |

この記事では、REPL の **標準** モードと **デバッグ** モードについて説明します。 IPython モードについて詳しくは、[IPython REPL の使用](interactive-repl-ipython.md)に関するページをご覧ください。

**Ctrl**+**Enter** などのエディターとのやりとりを含む、例を使用した詳細なチュートリアルについては、チュートリアルの「[手順 3: 対話型 REPL ウィンドウを使用する](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)」を参照してください。

## <a name="open-an-interactive-window"></a>対話型ウィンドウを開く

環境用の **対話型** ウィンドウを開くにはいくつかの方法があります。

(第 1 の方法) [Python 環境] ウィンドウに切り替え ( **[表示]**  >  **[その他のウィンドウ]**  >  **[Python 環境]** 、または **Ctrl**+**K** > **Ctrl**+ **`** )、選んだ環境の **[対話型ウィンドウを開く]** コマンドまたはボタンを選択します。

![Python 環境ウィンドウの対話型ウィンドウへのリンク](media/interactive-window-opening.png)

(第 2 の方法) **[表示]**  >  **[その他のウィンドウ]** メニューの下の方に、既定の環境の **[Python Interactive ウィンドウ]** コマンドと、**環境** ウィンドウに切り替えるためのコマンドがあります。

![[表示] > [その他のウィンドウ] の対話型ウィンドウ メニュー項目](media/interactive-window-menu.png)

(第 3 の方法) プロジェクトのスタートアップ ファイルで **対話型** ウィンドウを開くことができます。または、スタンドアロン ファイルの場合は、 **[デバッグ]**  >  **[Python Interactive で \<Project | File> を実行する]** メニュー コマンドを選びます (**Shift**+**Alt**+**F5**)。

![[Execute Project in Python Interactive (Python Interactive でプロジェクトを実行する)] メニュー](media/interactive-execute-project.png)

(第 4 の方法) ファイルでコードを選び、後で説明する [ **[Interactive に送信]** コマンド](#send-to-interactive-command)を使用します。

## <a name="interactive-window-options"></a>対話型ウィンドウのオプション

**[ツール]**  >  **[オプション]**  >  **[Python]**  >  **[対話型ウィンドウ]** を使って、**対話型** ウィンドウのさまざまな部分を制御できます ([オプション](python-support-options-and-settings-in-visual-studio.md)に関するページを参照)。

![Python Interactive ウィンドウのオプション](media/options-interactive-windows.png)

## <a name="use-the-interactive-window"></a>対話型ウィンドウの使用

**対話型** ウィンドウを開いた後は、 **\>\>\>** プロンプトで 1 行ずつコードの入力を開始できます。 **対話型** ウィンドウは、入力と同時に各行を実行します。これには、モジュールのインポートや、変数の定義などが含まれます。

![Python Interactive ウィンドウ](media/interactive-window.png)

例外は、上に示すように、`for` ステートメントがコロンで終わる場合など、完全なステートメントにするために追加のコード行が必要な場合です。 このような場合、行プロンプトが **...** に変わり、ブロックの追加行を入力する必要があることを示します (上の図の 4 番目と 5 番目の行を参照)。 空白行で **Enter** キーを押すと、**対話型** ウィンドウはブロックを終了し、インタープリターでブロックを実行します。

> [!Tip]
> **対話型** ウィンドウは、囲むスコープに属しているステートメントを自動的にインデントすることにより、Python の通常のコマンドライン REPL エクスペリエンスを向上させます。 対話型ウィンドウの履歴 (上方向キーで再呼び出しされます) は複数行の項目も提供しますが、コマンドライン REPL は単一行しか提供しません。

<a name="meta-commands"></a> また、**対話型** ウィンドウは複数のメタコマンドもサポートします。 すべてのメタコマンドは `$` で始まり、「`$help`」と入力するとメタコマンドの一覧が表示され、「`$help <command>`」と入力すると特定のコマンドの使用方法の詳細が表示されます。

:::moniker range="<=vs-2017"

| メタコマンド | 説明 |
| --- | --- |
| `$$` | コメントを挿入します。セッションのコードにコメントを追加するのに役立ちます。 |
| `$attach` | Visual Studio のデバッガーを REPL ウィンドウ プロセスにアタッチして、デバッグできるようにします。 |
| `$cls`, `$clear` | エディター ウィンドウの内容を消去し、履歴と実行コンテキストはそのまま維持します。 |
| `$help` | コマンドの一覧または特定のコマンドのヘルプを表示します。 |
| `$load` | ファイルからコマンドを読み込み、完了するまで実行します。 |
| `$mod` | 現在のスコープを指定されたモジュール名に切り替えます。 |
| `$reset` | 実行環境を初期状態にリセットしますが、履歴は保持します。 |
| `$wait` | 少なくとも指定されたミリ秒数だけ待機します。 |

:::moniker-end

:::moniker range=">=vs-2019"

| メタコマンド | 説明 |
| --- | --- |
| `$$` | コメントを挿入します。セッションのコードにコメントを追加するのに役立ちます。 |
| `$cls`, `$clear` | エディター ウィンドウの内容を消去し、履歴と実行コンテキストはそのまま維持します。 |
| `$help` | コマンドの一覧または特定のコマンドのヘルプを表示します。 |
| `$load` | ファイルからコマンドを読み込み、完了するまで実行します。 |
| `$mod` | 現在のスコープを指定されたモジュール名に切り替えます。 |
| `$reset` | 実行環境を初期状態にリセットしますが、履歴は保持します。 |
| `$wait` | 少なくとも指定されたミリ秒数だけ待機します。 |

:::moniker-end

Visual Studio 拡張機能で `IInteractiveWindowCommand` を実装およびエクスポートすることで、コマンドを拡張することもできます ([例](https://github.com/Microsoft/PTVS/blob/master/Python/Product/PythonTools/PythonTools/Repl/InteractiveWindowCommands.cs#L85))。

## <a name="switch-scopes"></a>スコープの切り替え

既定では、プロジェクトの **対話型** ウィンドウのスコープは、コマンド プロンプトから実行した場合のように、プロジェクトのスタートアップ ファイルに設定されます。 スタンドアロン ファイルの場合は、そのファイルがスコープになります。 ただし、**対話型** ウィンドウの上部にあるドロップダウン メニューを使って、REPL セッション中にいつでもスコープを変更できます。

![対話型ウィンドウのスコープ](media/interactive-scopes.png)

「`import importlib`」と入力するなどしてモジュールをインポートすると、そのモジュール内の他のスコープに切り替えるためのオプションがドロップダウン リストに表示されます。 **対話型** ウィンドウのメッセージは新しいスコープも示すため、セッション中にどのようにして特定の状態になったかを追跡できます。

スコープで「`dir()`」と入力すると、関数名、クラス、変数など、そのスコープで有効な識別子が表示されます。 たとえば、`import importlib` に続けて `dir()` を使うと、次にように表示されます。

![importlib スコープ内の対話型ウィンドウ](media/interactive-importlib-scope.png)

## <a name="send-to-interactive-command"></a>対話型コマンドへの送信

**対話型** ウィンドウ内で直接作業するだけでなく、エディターで、コードを選び、右クリックして、 **[Interactive に送信]** を選ぶか、**Ctrl**+**Enter** キーを押します。

![[Interactive に送信] メニュー コマンド](media/interactive-send-to.png)

このコマンドは、開発しながらコードをテストするなど、反復的なまたは革新的なコードの開発に役立ちます。 たとえば、**対話型** ウィンドウにコードの一部を送信し、その出力を表示した後、上方向キーを押してコードをもう一度表示し、変更してから、**Ctrl**+**Enter** キーを押して簡単にテストすることができます (入力の最後に **Enter** キーを押すと入力内容が実行されますが、入力の途中で **Enter** キーを押すと改行が挿入されます)。目的のコードができたら、簡単にプロジェクト ファイルにコピーして戻すことができます。

> [!Tip]
> 既定では、Visual Studio は **>>>** と **...** REPL プロンプトを、**対話型** ウィンドウからエディターにコードを貼り付ける際に削除します。 この動作は、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[Python]**  >  **[詳細設定]** タブで **[貼り付け時に REPL プロンプトを削除する]** オプションを使用して変更できます。 「[Options - Miscellaneous Options](python-support-options-and-settings-in-visual-studio.md#miscellaneous-options)」(オプション ∸ その他のオプション) を参照してください。

<!-- After 15.3 is released, you can also press **Undo** after pasting to restore prompts. Press **Undo** a second time to remove the pasted code entirely. -->

## <a name="work-with-code-cells"></a>コード セルの操作

コード セルはデータ分析で使用できます。また、さまざまなテキスト エディターでサポートされています。

たとえば、コード ファイルをスクラッチ パッドとして使用していると、小さなコードのブロックを一度に送信したい場合がよくあります。 コードを一緒にグループ化するには、`#%%` で始まるコメントを前のセルを終了するセルの先頭に追加して、コードを *コード セル* としてマーク付けします。 コード セルは折りたたむことも展開することもでき、コード セル内で **Ctrl**+**Enter** キーを使用することでセル全体を **対話型** ウィンドウに送信し、次のセルに移動できます。

Visual Studio は `# In[1]:` のようなコメントで始まるコード セルも検出します。これは、Jupyter Notebook を Python ファイルとしてエクスポートするときに取得する形式です。 この検出は、ノートブックを Python ファイルとしてダウンロードし、Visual Studio で開き、**Ctrl**+**Enter** キーを使用して各セルを実行することで、[Azure Notebooks](https://notebooks.azure.com/) からノートブックを簡単に実行できるようにします。

![対話型コード セル](media/interactive-code-cells.png)

## <a name="intellisense-behavior"></a>IntelliSense の動作

コード エディターの IntelliSense がソース コードの分析のみに基づくのとは異なり、**対話型** ウィンドウに含まれる IntelliSense はライブ オブジェクトに基づきます。 これらの提案は **対話型** ウィンドウではより正確です。動的に生成されるコードでは特にそうです。 欠点としては、副作用のある関数 (ログ メッセージなど) は、開発エクスペリエンスに影響を与える可能性があります。

それが問題になる場合は、オプションの「[対話型ウィンドウ オプション](python-support-options-and-settings-in-visual-studio.md#interactive-windows-options)」で説明されているように、 **[ツール]**  >  **[オプション]**  >  **[Python]**  >  **[対話型ウィンドウ]** の **[入力候補モード]** グループにある設定を変更します。
