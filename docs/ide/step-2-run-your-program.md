---
title: '手順 2: プログラムを実行する'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9a8fe90e-c97b-4e98-b6c8-0c6b3962c49d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c598aff620232ec56707206efa4715f8bc7ea2da
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55952322"
---
# <a name="step-2-run-your-program"></a>手順 2: プログラムを実行する
新しいソリューションを作成すると、実際には実行するプログラムが作成されます。 まだ実行される処理は少なく、タイトル バーに **Form1** と表示された空のウィンドウを表示するだけのプログラムですが、 もうおわかりのように実行することはできます。

 ![ビデオへのリンク](../data-tools/media/playvideo.gif)このトピックのビデオ版については、次をご覧ください。「[Tutorial 1:Create a picture viewer in Visual Basic - Video 1](http://go.microsoft.com/fwlink/?LinkId=205209)」(チュートリアル 1: Visual Basic でピクチャ ビューアーを作成する - ビデオ 1) または「[Tutorial 1:Create a picture viewer in C# - Video 1](http://go.microsoft.com/fwlink/?LinkId=205199)」(チュートリアル 1: C# でピクチャ ビューアーを作成する - ビデオ 1) をご覧ください。 これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

## <a name="to-run-your-program"></a>プログラムを実行するには

1.  プログラムを実行するには、次のいずれかの方法を使用します。

    -   **F5** キーを押します。

    -   メニュー バーで、**[デバッグ]** > **[デバッグ開始]** の順に選択します。

    -   ツール バーで、**[デバッグ開始]** ボタンを選択します (次の図を参照)。

         ![[デバッグの開始] ツール バー ボタン](../ide/media/express_icondebug.png)
 **[デバッグの開始]** ツール バー ボタン

2.  Visual Studio でプログラムが実行され、**Form1** というウィンドウが表示されます。 次の図は、作成したプログラムを示しています。 この実行中のプログラムに対し、これから機能を追加していきます。

     ![実行中の Windows フォーム アプリケーション プログラム](../ide/media/express_firstrun.png)
実行中の **Windows フォーム** アプリケーション プログラム

3.  Visual Studio 統合開発環境 (IDE) に戻り、新しいツール バーを参照します。 プログラムを実行すると、追加ボタンがツール バーに表示されます。 これらのボタンを使用するとプログラムの停止や開始などの操作ができ、発生する可能性のあるエラー (バグ) の追跡に役立ちます。 この例では、単にプログラムを開始および停止するために使用します。

     ![デバッグ ツール バー](../ide/media/express_debugtoolbar.png)
**デバッグ** ツール バー

4.  プログラムを停止するには、次のいずれかの方法を使用します。

    -   ツール バーで、**[デバッグの停止]** ボタンを選択します。

    -   メニュー バーで、**[デバッグ]** > **[デバッグの停止]** の順に選択します。

    -   **[Form1]** ウィンドウの上隅にある **X** ボタンを選択します。

    > [!NOTE]
    >  IDE 内からプログラムを実行する作業は、通常はプログラムでバグ (エラー) を特定して修正することが目的であるためデバッグと呼ばれます。 このプログラムは小さくて、実際には何も実行しませんが、それでも実際のプログラムです。 同じ手順で他のプログラムを実行し、デバッグします。 デバッグの詳細については、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」をご覧ください。

## <a name="to-continue-or-review"></a>続行または確認するには

-   チュートリアルの次の手順に進むには、「[手順 3:フォームのプロパティの設定](../ide/step-3-set-your-form-properties.md)」をご覧ください。

-   チュートリアルの前の手順に戻るには、「[手順 1:Windows フォーム アプリケーション プロジェクトの作成](../ide/step-1-create-a-windows-forms-application-project.md)」をご覧ください。
