---
title: 'ワークフロー デザイナー - 方法: 式エディターを使用する'
description: 式エディターが、式を入力および評価するために多くのワークフロー アクティビティで使用できるワークフロー デザイナー コントロールであることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 192418439bc25e6ac1b969483c0c48a030caa024
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894076"
---
# <a name="how-to-use-the-expression-editor"></a>式エディターを使用する方法

式エディターは、式を入力および評価するために多くのワークフロー アクティビティで使用できるワークフロー デザイナー コントロールです。 式エディターには、IntelliSense、色付け、パラメーター情報、エラーを示す波線などの、本格的な IDE 編集機能が用意されています。 入力した式はコンパイラによって検証されます。 式が無効な場合は、エラー アイコンが表示されます。 このエディターは、 **[式エディター]** ダイアログ ボックスとして開くこともできます。

式は、引数またはプロパティにバインドされたリテラル値または Visual Basic コードです。 式には、新しい値を生成するための操作と組み合わされた値要素 (変数、定数、リテラル、プロパティなど) が含まれます。 アプリケーションが C# を使用したプログラムに含まれている場合でも、式の記述には VB.NET 構文が使用されます。 つまり、大文字と小文字は区別されず、比較は 1 つの等号を使用して行われ ("==" ではなく "=")、ブール演算子は記号の "&&" と "||" ではなく単語 "and" と "or" であり、**null** の代わりに **Nothing** が使用されます。 Visual Basic の式と演算子の詳細情報およびサンプルについては、「[Visual Basic の演算子および式](/previous-versions/visualstudio/visual-studio-2010/a1w3te48(v=vs.100))」を参照してください。

**式エディター** は、次のように動作します。

- フォーカスがない場合、式エディターは通常の TextBlock コントロールと同様の外観になります。

- フォーカスが式エディターに移ると、式エディター コントロールと同様の外観と動作になります。 フォーカスが失われると、式エディターは通常の TextBlock と同様の外観に戻ります。

- 再ホストされたワークフロー デザイナーで式エディターにフォーカスを設定した場合は、TextBox と同じように動作します。 再ホストされたワークフロー デザイナーでフォーカスが失われると、式エディターは、通常の TextBlock と同様の外観に戻ります。

> [!NOTE]
> 式エディター用の IntelliSense は、Visual Studio 内でのみ使用できます。 Visual Studio および再ホストのシナリオではいずれも、入力した式がコンパイラによって検証され、式が無効な場合は、式エディターにエラー アイコンが表示されます。

## <a name="use-the-expression-editor"></a>式エディターを使用する

1. Visual Studio で新規または既存のワークフロー プロジェクトを開きます。

2. ワークフローに <xref:System.Activities.Statements.Assign> などのアクティビティを追加します。

    > [!NOTE]
    > 式エディターを使用できるワークフロー アクティビティは複数あります。 変数デザイナー、引数デザイナー、および動的引数デザイナーには、式 TextBlock も表示されます。 ここでは、例として <xref:System.Activities.Statements.Assign> アクティビティを使用しています。

3. <xref:System.Activities.Statements.Assign> アクティビティのアクティビティ デザイナーで、左側の式エディターをクリックします。

     灰色のウォーターマークの文字列 **\<To>** および **\<Enter a VB Expression>** は、<xref:System.Activities.Statements.Assign> アクティビティの式エディターに表示される既定のテキスト文字列です。

4. 式を入力します。 文字列を入力する場合は、文字列を引用符で囲みます。 式の引数を変数にバインドする場合は、引用符を省略してください。

     式を入力し終えたら、式エディターの外部を選択して、デザイナーの他の部分にフォーカスを移動させます。 フォーカスを移動すると、既に説明したように、コンパイラによって式が検証されます。

     式を入力または編集する別の方法として、プロパティ グリッドのプロパティ名の横にある省略記号をクリックするという方法もあります。 省略記号を選択すると、**式エディター** がダイアログ ボックスとして開きます。

## <a name="see-also"></a>関連項目

- <xref:System.Activities.Presentation.View.ExpressionTextBox>
