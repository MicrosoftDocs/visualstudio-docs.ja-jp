---
title: デバッグを行うときの呼び出し履歴に対するメソッドのマップ
description: デバッグ中に呼び出し履歴を視覚的にトレースするためのコード マップを作成する方法について説明します。 また、コメントをマップに追加してコードの動作を追跡できることについても説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- call stacks, code maps
- Call Stack window, mapping calls
- debugging [Visual Studio], diagramming the call stack
- call stacks, mapping
- Call Stack window, visualizing
- debugging code visually
- debugging [Visual Studio], mapping the call stack
- call stacks, visualizing
- debugging, code maps
- Call Stack window, tracing calls visually
- Call Stack window, show on code map
- debugging [Visual Studio], tracing the call stack visually
- debugging [Visual Studio], visualizing the call stack
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7196cf06e7d6bcde33bc1e4a6c5d0ebfac486576
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99946489"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>Visual Studio でデバッグを行うときの呼び出し履歴に対するメソッドのマップ

デバッグ中に呼び出し履歴を視覚的にトレースするためのコード マップを作成します。 コメントをマップに追加することでバグの発見に重点を置いてコードの動作を追跡できます。

 ![コード マップの呼び出し履歴を使用したデバッグ](../debugger/media/debuggermap_overview.png)

 次が必要です。

 ::: moniker range="vs-2017"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/downloads)

::: moniker-end

- デバッグできるコード (Visual C#、Visual Basic、C++、JavaScript、X++ など)

  参照トピック

- [ビデオ: コード マップ デバッガーの統合を使用して視覚的にデバッグする (Channel 9)](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

- [呼び出し履歴でマップを作成する](#MapStack)

- [コードに関するコメントを追加する](#MakeNotes)

- [次の呼び出し履歴でマップを更新する](#UpdateMap)

- [関連するコードをマップに追加する](#AddRelatedCode)

- [マップを使用してバグを見つける](#FindBugs)

- [Q & A](#QA)

  コード マップを使用するときに使用できるコマンドやアクションの詳細については、「[コード マップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)」を参照してください。

## <a name="map-the-call-stack"></a><a name="MapStack"></a>呼び出し履歴でマップを作成する

1. デバッグを開始します。 (キーボード: **F5** キー)

2. アプリが中断モードになるか、関数にステップ インした後で、 **[コード マップ]** を選択します。 (キーボード: **Ctrl** + **Shift** +  **`** キー)

     ![コード マップを選択して呼び出し履歴のマッピングを開始](../debugger/media/debuggermap_choosecodemap.png)

     現在の呼び出し履歴は新しいコード マップ上にオレンジ色で表示されます。

     ![コード マップの呼び出し履歴を参照](../debugger/media/debuggermap_seeundocallstack.png)

     デバッグを継続している間、マップは自動的に更新されます。 「[次の呼び出し履歴でマップを更新する](#UpdateMap)」を参照してください。

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a>コードに関するコメントを追加する

 コードの動作を追跡するためのコメントを追加します。 コメント内で新しい行を追加するには、**Shift+Return** キーを押します。

 ![コード マップの呼び出し履歴にコメントを追加](../debugger/media/debuggermap_addcomment.png)

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a>次の呼び出し履歴でマップを更新する

 アプリを次のブレークポイントまで実行するか、関数にステップ インします。 マップに新しい呼び出し履歴が追加されます。

 ![次の呼び出し履歴でコード マップを更新](../debugger/media/debuggermap_addclearcallstack.png)

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a>関連するコードをマップに追加する

 マップを作成できたところで、次の作業に進みます。 C# または Visual Basic で作業している場合は、フィールド、プロパティ、およびその他のメソッドなどの項目を追加して、コードの動作を追跡します。

 メソッドのコード定義を表示するには、そのメソッドをダブルクリックするか、そのメソッドのショートカット メニューを使用します。 (キーボード: マップでメソッドを選択して **F12** キーを押す)

 ![コード マップのメソッドのコード定義に移動](../debugger/media/debuggermap_gotocodedefinition.png)

 マップで追跡する項目を追加します。

 ![呼び出し履歴コード マップのメソッドのフィールドを表示](../debugger/media/debuggermap_showfields.png)

> [!NOTE]
> 既定では、マップに項目を追加すると、クラス、名前空間、アセンブリなどの親グループのノードも追加されます。 これは便利ですが、この機能を無効にしてマップをシンプルにしておくこともできます。このためには、マップ ツールバーの **[親を含める]** ボタンを使用するか、項目を追加するときに **Ctrl** キーを押します。

 ![呼び出し履歴コード マップのメソッドに関連するフィールド](../debugger/media/debuggermap_showedfields.png)

 ここでは、同じフィールドを使用するメソッドを簡単に表示できます。 追加された最新の項目は緑色で表示されます。

 コードのさらに多くの項目を表示するには、マップの作成を続けます。

 ![フィールドを使用するメソッドを参照: 呼び出し履歴コード マップ](../debugger/media/debuggermap_findallreferences.png)

 ![呼び出し履歴コード マップのフィールドを使用するメソッド](../debugger/media/debuggermap_foundallreferences.png)

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a>マップを使用してバグを見つける

 コードの視覚化はバグをよりすばやく見つけるために役立ちます。 たとえば、描画プログラムのバグを調査しているとします。 直線を描画して元に戻そうとしても、別の直線を描画するまで何も起こりません。

 そのため、`clear`、`undo`、および `Repaint` メソッドにブレークポイントを設定し、デバッグを開始して、次のようなマップを作成します。

 ![コード マップに別の呼び出し履歴を追加](../debugger/media/debuggermap_addpaintobjectcallstack.png)

 マップ上のすべてのユーザー ジェスチャーが、`Repaint` を除いて、`undo` を呼び出していることがわかります。 これが原因で `undo` がすぐに動作しない可能性があります。

 バグを修正してプログラムの実行を続けると、マップに `undo` から `Repaint` への新しい呼び出しが追加されます。

 ![コード マップの呼び出し履歴に新しいメソッド呼び出しを追加](../debugger/media/debuggermap_addnewcallforrepaint.png)

## <a name="q--a"></a><a name="QA"></a> Q & A

- **一部の呼び出しがマップに表示されません。なぜでしょうか。**

   既定では、ユーザー自身のコードだけがマップに表示されます。 外部コードを表示するには、 **[呼び出し履歴]** ウィンドウでオンにします。

   ![[呼び出し履歴] ウィンドウを使用して外部コードを表示](../debugger/media/debuggermap_callstackmenu.png)

   または、Visual Studio のデバッグ オプションで **[マイ コードのみを有効にする]** をオフにします。

   ![[オプション] ダイアログ ボックスを使用して、外部コードを表示](../debugger/media/debuggermap_debugoptions.png)

- **マップの変更はコードに影響を与えますか。**

   マップを変更してもコードには何の影響もありません。 マップでの名前変更、移動、削除は自由に行うことができます。

- **"ダイアグラムは古いバージョンのコードに基づいている可能性があります" というメッセージにはどのような意味がありますか。**

   マップを最後に更新してからコードが変更されている可能性があります。 たとえば、マップ上の呼び出しがコードに存在しなくなった可能性があります。 メッセージを閉じてから、マップを再び更新する前にソリューションをリビルドしてみます。

- **マップのレイアウトを制御するには、どのようにしますか。**

   マップのツール バーの **[レイアウト]** メニューを開きます。

  - 既定のレイアウトを変更します。

  - マップの自動再配置を停止するには、 **[デバッグ時に自動レイアウト]** をオフにします。

  - 項目を追加するときのマップの再配置を最小限にするには、 **[インクリメンタル レイアウト]** をオフにします。

- **マップを他のユーザーと共有できますか。**

   マップをエクスポートし、Microsoft Outlook があれば、他のユーザーに送信できます。または、マップを独自のソリューションに保存し、ソース管理にチェックインできます。

   ![呼び出し履歴コード マップを他のユーザーと共有](../debugger/media/debuggermap_sharewithothers.png)

- **マップに新しい呼び出し履歴が自動的に追加されないようにするには、どのようにしますか。**

   マップツールバーの ![&#45; [コード マップの呼び出し履歴を自動的に表示する]](../debugger/media/debuggermap_automaticupdateicon.gif) をクリックします。 マップに現在の呼び出し履歴を手動で追加するには、**Ctrl** + **Shift** +  **`** キーを押します。

   デバッグ中は、マップに既存の呼び出し履歴が引き続き強調表示されます。

- **項目のアイコンと矢印にはどのような意味がありますか。**

   項目に関する詳細を取得するには、マウス ポインターをその上に移動し、項目のヒントを確認します。 また、 **[凡例]** を参照すると、各アイコンの意味がわかります。

   ![呼び出し履歴コード マップのアイコンの意味](../debugger/media/debuggermap_showlegend.png)

  参照トピック

- [呼び出し履歴でマップを作成する](#MapStack)

- [コードに関するコメントを追加する](#MakeNotes)

- [次の呼び出し履歴でマップを更新する](#UpdateMap)

- [関連するコードをマップに追加する](#AddRelatedCode)

- [マップを使用してバグを見つける](#FindBugs)

## <a name="see-also"></a>関連項目

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)
- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [コード マップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)
