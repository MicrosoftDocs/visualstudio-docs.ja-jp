---
title: '手順 4: CheckTheAnswer() メソッドの追加'
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: c66f3831-b4a0-40bc-a109-8f46f4db35ed
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 075c56a5d5bcb02ee443035ac26d7730f145a445
ms.sourcegitcommit: 98b02f87c7aa1f5eb7f0d1c86bfa36efa8580c57
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72314080"
---
# <a name="step-4-add-the-checktheanswer-method"></a>手順 4: CheckTheAnswer() メソッドの追加

このチュートリアルの第 4 部では、計算問題に対する解答が正しいかどうかを判断するメソッド、`CheckTheAnswer()` を記述します。 このトピックは、コーディングの基本概念に関するチュートリアル シリーズの一部です。 チュートリアルの概要については、「[チュートリアル 2:制限時間ありの計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」を参照してください。

> [!NOTE]
> このトピックは、コーディングの基本概念に関するチュートリアル シリーズの一部です。
> - チュートリアルの概要については、「[チュートリアル 2:制限時間ありの計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」を参照してください。
> - コードの完全バージョンをダウンロードするには、「[計算クイズのチュートリアルの完全なサンプル](https://code.msdn.microsoft.com/Complete-Math-Quiz-8581813c)」を参照してください。

## <a name="to-verify-whether-the-answers-are-correct"></a>解答が正しいかどうかを確認するには

> [!NOTE]
> Visual Basic を使用している場合、このメソッドは値を返すため、通常の `Function` キーワードではなく、`Sub` キーワードを使用することに注意してください。 これは単に、Sub は値を返さないため、値を返す Function を使用しているだけです。

1. `CheckTheAnswer()` メソッドを追加します。

     このメソッドが呼び出されると、addend1 と addend2 の値を加算し、その結果を sum <xref:System.Windows.Forms.NumericUpDown> コントロールの値と比較します。 値が等しい場合、メソッドは `true` を返します。 それ以外の場合、メソッドは `false` の値を返します。 コードは次のようになります。

     [!code-vb[VbExpressTutorial3Step4#8](../ide/codesnippet/VisualBasic/step-4-add-the-checktheanswer-parens-method_1.vb)]
     [!code-csharp[VbExpressTutorial3Step4#8](../ide/codesnippet/CSharp/step-4-add-the-checktheanswer-parens-method_1.cs)]

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

     次に、新しい `CheckTheAnswer()` メソッドを呼び出すタイマーの <xref:System.Windows.Forms.Timer.Tick> イベント ハンドラーのメソッドのコードを更新して解答を確認します。

2. 次のコードを `if else` ステートメントに追加します。

     [!code-vb[VbExpressTutorial3Step4#10](../ide/codesnippet/VisualBasic/step-4-add-the-checktheanswer-parens-method_2.vb)]
     [!code-csharp[VbExpressTutorial3Step4#10](../ide/codesnippet/CSharp/step-4-add-the-checktheanswer-parens-method_2.cs)]

     解答が正しい場合、`CheckTheAnswer()` は `true` を返します。 イベント ハンドラーはタイマーを停止し、クリアしたことを示すメッセージを表示し、 **[Start]** ボタンが再び使用できるようになります。 それ以外の場合は、クイズが続行されます。

3. プログラムを保存し、実行して、クイズを起動し、加算問題の正しい解答を提供します。

    > [!NOTE]
    > 解答を入力する場合、解答を入力する前に既定値を選択するか、手動でゼロを削除する必要があります。 この動作については、このチュートリアルで後ほど修正します。

     正しい解答を入力すると、メッセージ ボックスが開き、 **[Start]** が使用できるようになり、タイマーが停止します。

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 **[手順 5: NumericUpDown コントロールの Enter イベント ハンドラーの追加](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md)** 」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 3:カウントダウン タイマーの追加](../ide/step-3-add-a-countdown-timer.md)」をご覧ください。
