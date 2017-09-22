---
title: "R Tools for Visual Studio の変数エクスプローラー | Microsoft Docs"
ms.custom: 
ms.date: 6/30/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-r
ms.devlang: r
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c669434-40d8-4970-92cc-502a98c8b5ab
caps.latest.revision: 1
author: kraigb
ms.author: kraigb
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 712cc780388acc5e373f71d51fc8f1f42adb5bed
ms.openlocfilehash: 92396808161886cf3b15f7e8e0ab23a0a35e26b9
ms.contentlocale: ja-jp
ms.lasthandoff: 07/12/2017

---

# <a name="variable-explorer"></a>変数エクスプローラー

**変数エクスプローラー** ウィンドウは、**[R Tools] > [ウィンドウ] > [変数エクスプローラー]** (または、 **[R Tools] > [データ サイエンスの設定]** を使用した場合は Ctrl + 8 キー) を使用して開きます。このウィンドウには、現在の R セッションでの特定のスコープにあるすべての変数が表示されます。 たとえば、変数エクスプローラーを開いて[対話型ウィンドウ](interactive-repl.md)に以下の行を入力したとします。

```R
x <- 42
y <- 43
n <- c(1,2,3,5,8,13)
```
 
変数エクスプローラー ウィンドウには次のように表示されます。

![Visual Studio の変数エクスプローラー ウィンドウ](media/variable-explorer-window.png)

より複雑な R データ フレームが定義されているセッションでは、データに移動できます。 たとえば、`cars <- mtcars` の実行後、変数エクスプローラーでさまざまなノードを展開して、データセット内を移動することができます。
 
![変数エクスプローラーの展開ビュー](media/variable-explorer-expanded-results.png)
 
変数を削除するには、右クリックして **[削除]** を選択するか、変数を選択して Del キーを押します。

インクリメンタル検索を使用して、データ フレームで測定項目を検索することもできます。 まず検索対象データ フレームのノードを展開してから、検索ボックスに検索語句を入力します。

## <a name="details-table-view"></a>詳細 (テーブル) ビュー

多くの場合データは表形式であるため、複合データ型を個別のテーブルとして表示できます。そのためには、虫眼鏡アイコンを選択するか、右クリックして **[詳細の表示]** を選択します。 

![変数エクスプローラー](media/variable-explorer-table-view.png)

列見出しをクリックすると、その列を基準にデータが並べ替えられます (クリックするたびに昇順と降順が切り替わります)。 Shift キーを押しながら他の列をクリックすると、それらの列が並べ替えの対象として追加されます。 Shift キーを押さずに 1 つの列をクリックすると、単一の列を基準にした並べ替えに戻ります。

列見出しをクリックする順序によって、並べ替えの実行順序が決まります。 たとえば、Shift キーを押しながら **cyl** 列をクリックし、次に Shift キーを押したまま **mpg** 列を 2 回クリックすると、リストはシリンダー数の昇順に並べ替えられた後、燃費の降順に並べ替えられます。

![2 つの列を基準にしたデータの並べ替えを示すテーブル ビュー。](media/variable-explorer-table-view-sorting.png)

変数エクスプローラーとテーブル ビューは、別の Visual Studio ウィンドウに表示されるため、作業しやすい配置になるように並べて表示できます。 一般的な操作手順については、「[Visual Studio のウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」を参照してください。

## <a name="open-in-excel-or-other-csv-capable-application"></a>Excel (またはその他の CSV に対応したアプリケーション) で開く

さらに処理したり分析したりするには、セッション変数を CSV にエクスポートすると便利なことがよくあります。 エクスポートは、変数エクスプローラーの各ノードの横にある小さい Excel のアイコン (![Excel エクスポート アイコン](media/variable-explorer-excel-icon.png)) を使うか、項目を右クリックして **[CSV アプリで開く]** を選びます。 このアイコンを選択すると、`%userprofile%\Documents\RTVS_CSV_Exports` フォルダーの新規 CSV ファイルにデータが書き込まれ、そのファイルが起動されて、`.csv` の拡張子に関連付けられているアプリケーションで開きます。

## <a name="scopes"></a>スコープ

既定では、変数エクスプローラーはグローバル スコープで開かれます。 ウィンドウ上部のドロップダウンからパッケージを選択することで、パッケージ スコープに切り替えることができます。

![パッケージ スコープが表示された変数エクスプローラー](media/variable-explorer-package-scopes.png)

また、デバッガーのブレークポイントで停止したとき、関数スコープに切り替えることもできます (変数エクスプローラーがデバッグ中のコードの関数スコープに自動的に切り替わることはありません)。

![デバッグ中のデータ フレームが表示された変数エクスプローラー](media/variable-explorer-as-locals-window.png)

デバッガーでコードをステップ実行するときには、変数エクスプローラーが自動的に関数スコープに切り替わり、関数のローカル変数などが表示されます。


## <a name="importing-data-into-variable-explorer"></a>変数エクスプローラーへのデータのインポート

変数エクスプローラー ツール バーの 2 つのコマンド (**[R Tools] > [データ]** メニューから選択することもできます) を使用して、外部 CSV データセットを R セッションにインポートできます。**[データセットを Web URL から R セッションにインポートする]** と **[データセットをテキスト ファイルから R セッションにインポートする]**の 2 つです。 

インポートする CSV ファイルを指定すると、Visual Studio の **[データセットのインポート]** ダイアログ ボックスが表示されます。このダイアログ ボックスで、データ ファイルの解析方法 (つまり、フィールド区切り記号は何か、引用符をどう扱うかなど) を制御するオプションを指定します。 インポートしたデータ フレームのプレビューと元のデータ ファイルを表示することもできます。

![[データセットのインポート] ダイアログ ボックス](media/variable-explorer-import-dataset-dialog.png)

