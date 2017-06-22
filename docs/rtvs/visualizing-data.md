---
title: "R Tools for Visual Studio でデータを視覚化する | Microsoft Docs"
ms.custom: 
ms.date: 5/1/2017
ms.prod: visual-studio-dev15
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-r
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 1
author: kraigb
ms.author: kraigb
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 7a873df77756e5a957d327049566c8e0db1f3a8a
ms.openlocfilehash: cd9e0afac5c9a0975197cb65001f8f2698242b85
ms.contentlocale: ja-jp
ms.lasthandoff: 05/12/2017

---


# <a name="creating-visual-data-plots-with-r"></a>R でデータを視覚化する

データ サイエンティストのワークフローにおいて、プロットは重要な部分を担います。 R Tools for Visual Studio (RTVS) では、あらゆるプロット行為は 1 つまたは複数のプロット ウィンドウを中心に行われます。プロット ウィンドウはこの重要な行為の生産性を上げるように設計されています。

![ヒーローのイメージをプロットする](media/plotting-hero-image.png)

このトピックの内容

- [プロット ウィンドウ](#the-plot-window)
- [複数のプロット ウィンドウ](#multiple-plot-windows)
- [プロット履歴](#plot-history)
- [プロット ウィンドウをプログラムで操作する](#programmatically-manipulating-plot-windows)

次の動画 (2 分 02 秒) は RTVS によるプロットを簡単に説明しています。

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZTbKmz5RSgY" frameborder="0" allowfullscreen></iframe>

## <a name="the-plot-window"></a>プロット ウィンドウ

プロット ウィンドウには一連のプロットが入ります。各プロットは `plot` コマンドで生成されます。 たとえば、`plot(1:100)` を使用すると、プロット ウィンドウがない場合に新しく作成されます。

![1 ～ 100 の線形プロット](media/plotting-1-to-100.png)

技術的には、R `plot` コマンドがその出力を R グラフィックス デバイスにレンダリングし、プロット ウィンドウが R グラフィックス デバイスのコンテンツをレンダリングします。そのため、各プロット ウィンドウにデバイス番号が与えられます。

プロット ウィンドウは Visual Studio プロジェクトに依存せず、プロジェクトを読み込んだり、閉じたりしても、プロット ウィンドウは開いている状態を維持します。

プロットの生成には "アクティブな" プロット ウィンドウが使用されます。前のプロットはプロット履歴に保存されます (「[プロット履歴](#plot-history)」参照)。 たとえば、`plot(100:1)` を入力すると、上記のプロットが下向きの線に入れ替えられます。

他のすべての Visual Studio ウィンドウと同様に、 プロット ウィンドウのレイアウトはカスタマイズできます (「[Visual Studio のウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」参照)。 プロット ウィンドウは Visual Studio フレーム内のさまざまな場所にドッキングできます。このとき、そのフレームの中でサイズが変更されます。あるいは、フレームから完全に引き出し、フレームに関係なくサイズを変更できます。 

プロット ウィンドウのサイズを変更すると必ずプロットが再レンダリングされ、最良の画質が与えられます。 サイズ変更は通常、次のセクションで説明するコマンドを利用し、プロットをファイルまたはクリップボードにエクスポートする前に行います。

## <a name="plot-window-commands"></a>プロット ウィンドウ コマンド

プロット ウィンドウのツールバーには適用できるコマンドが表示されます。コマンドの大半は、**[R Tools]、[プロット]** メニューの順に選択しても表示できます。

| ボタン | コマンド | 説明 | 
| --- | --- | --- |
| ![新しいプロット ウィンドウ ボタン](media/plotting-toolbar-01-new-plot-window.png) | 新しいプロット ウィンドウ | 個別のプロット ウィンドウとその履歴を作成します。 「[複数のプロット ウィンドウ](#multiple-plot-windows)」を参照してください。 |
| ![プロット ウィンドウをアクティブにするボタン](media/plotting-toolbar-02-activate-plot-window.png) | プロット ウィンドウをアクティブにする | 後続の `plot` ウィンドウが現在のプロット ウィンドウにレンダリングされるように、現在のプロット ウィンドウをアクティブ ウィンドウとして設定します。 「[複数のプロット ウィンドウ](#multiple-plot-windows)」を参照してください。 「[複数のプロット ウィンドウ](#multiple-plot-windows)」を参照してください。 |
| ![プロット履歴ウィンドウ ボタン](media/plotting-toolbar-03-plot-history.png) | プロット履歴ウィンドウ | 履歴にあるすべてのプロットをサムネイルとして表示した状態でウィンドウを開きます。 「[プロット履歴](#plot-history)」を参照してください。 |
| ![プロット履歴ボタン](media/plotting-toolbar-04-plot-history-arrows.png) | 前/次のプロット |  履歴の前のプロット/次のプロットに移動します。 Ctrl + Alt + F11 (前) と Ctrl + Alt + F12 (次) でも移動できます。 「[プロット履歴](#plot-history)」を参照してください。 |
| ![イメージとして保存ボタン](media/plotting-toolbar-05-save-as-image.png)| イメージとして保存 | ファイル名の入力を求め、現在のプロット (ウィンドウ コンテンツ、ウィンドウ サイズ) をイメージ ファイルに保存します。 利用できる形式は `.png`、`.jpg`、`.bmp`、`.tif` です。 |
| ![PDF として保存ボタン](media/plotting-toolbar-06-save-as-pdf.png)| PDF として保存 | 現在のウィンドウ サイズで現在のプロットを PDF ファイルに保存します。 PDF が拡大または縮小されると、プロットは再レンダリングされます。 |
| ![ビットマップとしてコピー ボタン](media/plotting-toolbar-07-copy-as-bitmap.png)| ビットマップとしてコピー | 現在のウィンドウ サイズでプロットをラスター ビットマップとしてクリップボードにコピーします。 | 
| ![メタファイルとしてコピー ボタン](media/plotting-toolbar-08-copy-as-metafile.png)| メタファイルとしてコピー | プロットを [Windows メタファイル](https://en.wikipedia.org/wiki/Windows_Metafile) としてクリップボードにコピーします (Wikipedia)。 | 
| ![プロットの削除ボタン](media/plotting-toolbar-09-remove-plot.png)| プロットの削除 | 履歴から現在のプロットを削除します。 |
| ![すべてのプロットをクリア ボタン](media/plotting-toolbar-10-clear-all-plots.png) | すべてのプロットをクリア | 履歴からプロットをすべて削除します (確認が求められます)。 |

## <a name="multiple-plot-windows"></a>複数のプロット ウィンドウ

データ サイエンティストは多くの場合、さまざまなデータセットのさまざまなプロットを操作します。そのため、RTVS は、非依存のプロット ウィンドウを任意の数だけ作成し、Visual Studio フレームの内外に自由に配置できるようになっています。 (ウィンドウのドッキングとサイズ変更に関する全般情報については、「[Visual Studio のウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」を参照してください。)

新しいプロット ウィンドウはツールバーのボタンか、**[R Tools]、[プロット]、[新しいプロット ウィンドウ]** で作成できます。 新しいプロット ウィンドウは*アクティブ* ウィンドウとなり、新しいプロットがレンダリングされます。 アクティブ ウィンドウを変更するには、アクティブにするウィンドウに切り替え、[プロット ウィンドウをアクティブにする] ツールバー ボタンか、**[R Tools]、[プロット]、[プロット ウィンドウをアクティブにする]** を選択します。

プロットも非依存オブジェクトです。つまり、プロット ウィンドウ間でコピーしたり、移動したりできます。マウスでドラッグ アンド ドロップするか、右クリック コンテキストや **[編集]** メニューの **[コピー]**、**[切り取り]**、**[貼り付け]** コマンドを使用します。

 ドラッグ アンド ドロップの既定の動作はコピーです。移動するには、Shift キーを押しながらドラッグ アンド ドロップします。

## <a name="plot-history"></a>プロット履歴

プロット コマンドは各ウィンドウのプロット履歴に保存されます。セッション内のすべてのプロットが保存されます。 履歴内を移動するには、プロット ウィンドウ ツールバーの矢印ボタンを使用するか、Ctrl + Alt + F11 と Ctrl + Alt + F12 を使用します。 ツールバーのボタンか、**[R Tools]、[プロット]** メニュー コマンドを使用し、単一プロットを削除したり、ウィンドウからすべてのプロットを消去したりできます。

プロットのコレクション全体を表示するには、ツールバーのボタンか、**[R Tools]、[プロット]、[プロット履歴ウィンドウ]** を使用してプロット履歴ウィンドウを開きます。
そのウィンドウに表示されていたプロットのサムネイルが一覧表示されます。プロット ウィンドウ (またはデバイス) 別に分類されます。 ツールバーのズーム ボタンを使用すると、サムネイルのサイズが変更されます。

![プロット履歴ウィンドウ](media/plotting-plot-history-window.png)

プロットを関連ウィンドウで開くには、そのプロットをダブルクリックして選択し、**[プロットの表示]** ツールバー ボタンを選択するか、右クリックして **[プロットの表示]** を選択します。 個々のプロットを選択し、右クリック コンテキストか **[編集]** メニューからコピー、切り取り、削除することもできます。

すべてのウィンドウにわたり、プロット履歴の有効期間はインタラクティブ R セッションの有効期間によって決まります。 R セッションをリセットするか、Visual Studio を終了して再起動すると、プロット履歴がリセットされます。

## <a name="programmatically-manipulating-plot-windows"></a>プロット ウィンドウをプログラムで操作する

R コードからプロット ウィンドウをプログラムで操作できます。デバイス番号を利用し、特定のプロット ウィンドウを特定します。 

- `dev.list()`: 現在の R セッション内のグラフィックス デバイスをすべて一覧表示します。
- `dev.new()`: 新しいグラフィックス デバイス (新しいプロット ウィンドウ) を作成します。
- `dev.set(<device number>)`: アクティブなグラフィックス デバイスを設定します。
- `dev.off()`: アクティブなデバイスを削除します。

