---
title: "R Tools for Visual Studio での R Markdown | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: 
ms.technology: devlang-r
ms.devlang: r
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.workload: data-science
ms.openlocfilehash: 340ab0b55de1bb6c5889bb15560065d71e438ca6
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="creating-r-markdown-documents"></a>R Markdown ドキュメントの作成

[R Markdown](https://rmarkdown.rstudio.com/) は、R の分析を、高品質のドキュメント、レポート、プレゼンテーション、およびダッシュボードに変換するドキュメント形式です。

R Tools for Visual Studio (RTVS) には、R Markdown 項目テンプレート、エディターのサポート (エディター内の R コード用の IntelliSense など)、ファイル生成機能、ライブ プレビューがあります。

## <a name="using-r-markdown"></a>R Markdown の使用

1. Visual Studio を閉じます。
1. (1 回のみ) [pandoc.org](http://pandoc.org/installing.html) の `pandoc` をインストールします。
1. Visual Studio を再起動すると、pandoc のインストールが選択されます。
1. `knitr` および `rmarkdown` パッケージをインストールします。インストールは、[インタラクティブ ウィンドウ](interactive-repl.md)から実行できます。

    ```R
    install.packages("knitr")
    install.packages("rmarkdown")

    ```
1. 新しい R Markdown ファイルを作成します。それには、**[ファイル]、[新規]、[ファイル]** メニュー コマンドの順に移動し、**[R] を選択し、一覧から [R Markdown]** を選択します。 プロジェクトのコンテキストで、ソリューション エクスプローラー内のプロジェクトを右クリックし、**[R Markdown を追加]** を選択します (または、**[追加]、[新しいアイテム]** の順に移動し、一覧から **[R Markdown]** を選択します)。

1. 新しいファイルの既定の内容は次のとおりです。

    ~~~markdown
    ---
    title: "Untitled"
    output: html_document
    ---

    This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and Microsoft Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

    When you click the **R Tools | Publish | Preview** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

    ```{r}
    summary(cars)
    ```

    You can also embed plots, for example:

    ```{r, echo=FALSE}
    plot(cars)
    ```

    Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.

    ~~~

## <a name="previews"></a>プレビュー

Visual Studio 2017 バージョン 15.5 以降では、R Markdown のライブ プレビューを自動的に提供します。 エディターとプレビュー間の自動同期を有効にするには、**[R Tools]、[Markdown]、[自動同期]** の順に選択します (Ctrl + Shift + Y)。 自動同期を使用していない場合は、**[R Tools] > [Markdown] > [R Markdown プレビューのリロード]** を使用してプレビューを更新することができます。

また、エディター内を右クリックし、**[プレビュー]** コマンドのいずれかを選択すると、ファイルを HTML、PDF、Microsoft Word の形式でプレビューすることもできます。 **[R Tools] > [Markdown]** メニューからも同じコマンドが利用できます  (Visual Studio の以前のバージョンでは、これらのコマンドは **[R Tools] > [発行]** メニューにあります)。

![RMarkdown ライブ プレビューおよびその他のプレビュー メニュー コマンド](media/rmarkdown-live-preview.png)
