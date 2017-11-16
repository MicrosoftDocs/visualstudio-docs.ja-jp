---
title: "R Tools for Visual Studio のヘルプ ウィンドウ | Microsoft Docs"
ms.custom: 
ms.date: 06/29/2017
ms.reviewer: 
ms.suite: 
ms.technology: devlang-r
ms.devlang: r
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: ef9c04d4-0d5e-405a-842e-8d47fa0e8781
caps.latest.revision: "1"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.openlocfilehash: cf63def0503e885b1c6ab42584f9f1932b77127f
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="help-in-r-tools-for-visual-studio"></a>R Tools for Visual Studio のヘルプ

R のヘルプは、Visual Studio の対話型ウィンドウに直接統合されています。 `?` コマンド (`?mtcars` など) を使用する場合、R ドキュメントのヘルプが、Visual Studio ウィンドウに表示されます。

![Visual Studio のヘルプ ウィンドウ](media/help-window.png)

> [!Tip]
> ヘルプ ウィンドウは、Visual Studio のその他すべてのウィンドウと同様に、好みに応じて配置およびドッキングすることができます。 「[Visual Studio のウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」を参照してください。
>
> また、**[R Tools] > [オプション]** メニューを選択して、**[R ヘルプ ブラウザー]** プロパティに `External` を設定し、ブラウザーでヘルプの結果を開くことができます。 [オプション](options.md)に関するページを参照してください。

ヘルプを検索するには、`??` に続けて検索用語を指定します。 検索用語にスペースが含まれる場合は、用語を引用符で囲みます。

```R
??"Motor Trend"
```

![ヘルプの検索結果](media/help-search1.png)

また、ヘルプ ウィンドウには、R ドキュメントの詳細な検索を直接実施できる、検索入力フィールドもあります。

![入力フィールドを使用したヘルプの検索結果](media/help-search2.png)

## <a name="integrated-help-lookup"></a>統合ヘルプの参照

開発者は、関数名、データセットなどの要素についてわからないことがあると、多くの場合は R ドキュメントを検索します。 R Tools for Visual Studio (RTVS) では、ヘルプの検索をエディターと対話型ウィンドウに直接統合することで、このプロセスを簡略化しています。

- オート コンプリート操作中に F1 キーを押すと、サブ文字列に一致するヘルプの結果一覧が生成されます。
- 検索用語 (関数など) を右クリックして **[<用語> のヘルプ]** コマンドを選択すると、その関数のヘルプを開きます。 また、任意の選択に対して **[Help on]\(ヘルプの表示\)** を呼び出すこともできます。

    ![コンテキスト メニューを右クリックしてヘルプを呼び出す](media/help-right-click.png)

> [!Tip]
> ブラウザーで統合ヘルプを開くには、**[R Tools] > [オプション]** を選択して、**[F1 Web ブラウザー]** に `External` を設定します。 [オプション](options.md)に関するページを参照してください。

## <a name="integrated-stackoverflow-search"></a>StackOverflow 検索の統合

R ドキュメントでの検索に加えて、開発者はコードを記述するときに StackOverflow を検索することが多いです。 RTVS では、このプロセスも効率化されます。 用語または選択範囲を右クリックし、**[Web で <用語> を検索します]** コマンド (Ctrl + F1 キー) を選択すると、Visual Studio からウィンドウが開き、StackOverflow を対象に検索結果が表示されます。

![Visual Studio の Web 検索結果](media/help-web-search-results.png)

**[R Tools] > [オプション] > [F1 Web 検索文字列]** オプションを使用して、追加されたスコープ文字列 `R site:stackoverflow` を変更できます。

![[F1 Web 検索文字列] オプションを変更する](media/options-dialog.png)

ブラウザーで結果を表示するには、「[R Tools for Visual Studio オプション](options.md)」に従って **[F1 Web ブラウザー]** オプションを変更します。