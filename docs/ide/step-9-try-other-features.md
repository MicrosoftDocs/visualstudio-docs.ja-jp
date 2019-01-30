---
title: '手順 9: その他の機能を試す'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: 1b0c5c80-e5a6-4f69-a4a4-0e89a82d4de0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4fcc95d0383919d17e5620204119248e9d5c5f30
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54959984"
---
# <a name="step-9-try-other-features"></a>手順 9: その他の機能を試す
さらに詳しく学習するために、アイコンおよび色の変更、ゲーム タイマーの追加、サウンドの追加を試します。 ゲームをよりやりがいのあるものにするために、ボードの拡大およびタイマーの調整を試します。

 サンプルの完全バージョンをダウンロードするには、「[Complete Matching Game tutorial sample](https://code.msdn.microsoft.com/Complete-Matching-Game-4cffddba)」(絵合わせゲームのチュートリアルの完全なサンプル) を参照してください。

## <a name="to-try-other-features"></a>その他の機能を試すには

-   アイコンおよび色を、選択したものに置き換えます。

    > [!TIP]
    >  ラベルの [Forecolor](<xref:System.Windows.Forms.Control.ForeColor%2A>) プロパティを見てみてください。

-   プレーヤーが勝利するまでにかかる時間の長さを追跡するゲーム タイマーを追加します。

    > [!TIP]
    >  そのためには、フォーム上の <xref:System.Windows.Forms.TableLayoutPanel> の上に経過時間を表示するためのラベルを追加し、その時間を追跡するための別のタイマーを追加します。 プレーヤーがゲームを開始するとタイマーを開始し、最後の 2 つのアイコンが一致した後にタイマーを停止するコードを使用します。

-   プレーヤーが一致を見つけたときのサウンド、プレーヤーが一致しない 2 つのアイコンを表示したときの別のサウンド、およびプログラムでアイコンが再度非表示になるときの 3 つ目のサウンドを追加します。

    > [!TIP]
    >  サウンドを再生するには、<xref:System.Media> 名前空間を使用できます。 詳細については、「[Play Sounds in Windows Forms App (C#)](http://youtu.be/qOh4ooHg1UU)」(Windows フォーム アプリでサウンドを再生する (C#)) または「[How To Play Audio In Visual Basic](http://youtu.be/-4oPDeQrtMs)」(Visual Basic でオーディオを再生する方法) をご覧ください。

-   ボードを拡大して、ゲームをより難しくします 

    > [!TIP]
    >  TableLayoutPanel に行や列を追加する以上のことを行う必要があります。作成するアイコンの数を検討する必要もあります。

-   プレーヤーが、選択が遅すぎて一定時間内に 2 つ目のアイコンをクリックしなかった場合に、1 つ目のアイコンを非表示にするようにして、ゲームをよりやりがいのあるものにします。

## <a name="to-continue-or-review"></a>続行または確認するには

-   プログラミングに行き詰まった場合や疑問がある場合は、MSDN フォーラムのいずれかに質問を投稿してみてください。 [Visual Basic フォーラム](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vbgeneral) と [Visual C# フォーラム](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=csharpgeneral)を参照してください。

-   無料で利用できる便利なビデオ学習リソースがあります。 Visual Basic でのプログラミングの詳細については、「[Visual Basic の基礎:入門者向けの開発](https://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners)」を参照してください。 Visual C# でのプログラミングの詳細については、「[C# の基礎:入門者向けの開発](https://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners)」を参照してください。

-   チュートリアルの前の手順に戻るには、「[手順 8:プレーヤーが勝利したかどうかを確認するメソッドの追加](../ide/step-8-add-a-method-to-verify-whether-the-player-won.md)」を参照してください。
