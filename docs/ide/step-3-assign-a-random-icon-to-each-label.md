---
title: "手順 3: 各ラベルへのランダムなアイコンの割り当て | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
caps.latest.revision: 31
author: kempb
ms.author: kempb
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
translationtype: Human Translation
ms.sourcegitcommit: 9044821c2bfee0dba8ffa91f3d91afd565b8d957
ms.openlocfilehash: 75c899caa3b620899bb2bd8107c63386dd4f40d9
ms.lasthandoff: 02/22/2017

---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>手順 3: 各ラベルへのランダムなアイコンの割り当て
ゲームで毎回、同じアイコンが同じセルに表示されていたのでは、やりがいがありません。 これを避けるには、`AssignIconsToSquares()` メソッドを使用して、フォームのラベル コントロールにアイコンをランダムに割り当てます。  
  
### <a name="to-assign-a-random-icon-to-each-label"></a>各ラベルにランダムなアイコンを割り当てるには  
  
1.  次のコードを追加する前に、メソッドのしくみについて検討します。 新しいキーワード `foreach` (Visual C# の場合) および `For Each` (Visual Basic の場合) があります  (1 つの行は意図的にコメント アウトされています。これについてはこの手順の最後に説明します)。  
  
     [!code-cs[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_1.vb)]  
  
2.  前の手順で示されているように、`AssignIconsToSquares()` メソッドを追加します。 このメソッドを、「[手順 2: Random オブジェクトおよびアイコンのリストの追加](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)」で追加したコードのすぐ下に配置できます。  
  
     前に説明したように、`AssignIconsToSquares()` メソッドに新しいものが含まれています。つまり、`foreach` ループ (Visual C# の場合) および `For Each` (Visual Basic の場合) です。 `For Each` ループは、同じ処理を繰り返し実行する必要がある場合にいつでも使用できます。 ここでは、次のコードで説明されているように、TableLayoutPanel のラベルごとに同じステートメントを実行する必要があります。 最初の行では、`control` という名前の変数を作成し、その変数に一度に&1; つずつコントロールを格納して、そのコントロールに対してループ内のステートメントを実行します。  
  
     [!code-cs[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_2.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_2.vb)]  
  
    > [!NOTE]
    >  "iconLabel" および "control" という名前が使用されているのは、わかりやすくするためです。 これらの名前を任意の名前に置き換えても、コードはまったく同じように動作します (ただしループ内の各ステートメントで名前を変更する必要はあります)。  
  
     `AssignIconsToSquares()` メソッドは、TableLayoutPanel の各ラベル コントロールを反復処理し、それぞれに対し同じステートメントを実行します。 これらのステートメントは、「[手順 2: Random オブジェクトおよびアイコンのリストの追加](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)」からランダムなアイコンを取得します。 (リストに各アイコンを&2; つずつ含め、ランダムなラベル コントロールにアイコンのペアが割り当てられるようにしたのはこのためです)。  
  
     `foreach` または `For Each` ループ内で実行されるコードを詳しく見てみましょう。 次に示しているのは前に示したコードの一部です。  
  
     [!code-cs[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_3.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_3.vb)]  
  
     最初の行では、`control` 変数を `iconLabel` という名前のラベルに変換しています。 その次の行は、変換が成功したかどうかを確認する `if` ステートメントです。 変換が成功した場合は、`if` ステートメント内のステートメントが実行されます  (前のチュートリアルでも説明したように、`if` ステートメントは、指定した任意の条件を評価するために使用されます)。`if` ステートメントの最初の行では、`randomNumber` という名前の変数を作成し、icons リスト内の項目のいずれかに対応する乱数をこの変数に格納します。 そのために、前に作成した `Next` オブジェクトの `Random` メソッドを使用します。 `Next` メソッドは乱数を返します。 またこの行では、`Count` リストの `icons` プロパティを使用して、乱数を選択する範囲を決定しています。 次の行では、icons リストのいずれかの項目をラベルの `Text` プロパティに割り当てています。 コメントアウトしている行は、このトピックの後半で説明します。 最後に、`if` ステートメントの最終の行で、フォームに追加したアイコンをリストから削除しています。  
  
     コード内にわからない部分があれば、コード要素の上にマウス ポインターを合わせると、関連するヒントが表示されます。 Visual Studio デバッガーを使用して、プログラムの実行中にコードの各行をステップ実行することもできます。 詳細については、「[How Do I: Step with The Debugger in Visual Studio?](http://msdn.microsoft.com/vstudio/ee672313.aspx)」 (操作方法: Visual Studio のデバッガーでステップ実行する) または「[デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)」を参照してください。  
  
3.  ゲーム ボードをアイコンで埋めるには、プログラムが起動したらすぐに `AssignIconsToSquares()` メソッドを呼び出す必要があります。 Visual C# を使用している場合は、`Form1`*constructor* の `InitializeComponent()` メソッドの呼び出しのすぐ下にステートメントを追加し、フォームが新しいメソッドを呼び出してフォーム自体の設定後に表示されるようにします。 新しいオブジェクト (クラスや構造体など) を作成するときは、コンストラクターを呼び出します。 詳細については、「[コンストラクター (C# プログラミング ガイド)](http://msdn.microsoft.com/library/ace5hbzh.aspx)」または「[コンストラクタとデストラクターの使用方法](http://msdn.microsoft.com/library/2z08e49e.aspx)」 (Visual Basic の場合) を参照してください。  
  
     [!code-cs[VbExpressTutorial4Step2_3_4#13](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_4.cs)]  
  
     Visual Basic の場合は、`AssignIconsToSquares()` メソッドの呼び出しを `Form1_Load` メソッドに追加します。コードは次のようになります。  
  
    ```vb  
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load  
        AssignIconsToSquares()  
    End Sub  
    ```  
  
4.  プログラムを保存し、実行します。 各ラベルに割り当てられたランダムなアイコンを備えたフォームが表示されます。  
  
5.  いったんプログラムを終了して、再び実行します。 次の図に示すように、各ラベルに別のアイコンが割り当てられています。  
  
     ![ランダムなアイコンが表示された絵合わせゲーム](../ide/media/express_tut4step3.png "Express_Tut4Step3")  
ランダムなアイコンが表示された絵合わせゲーム  
  
     アイコンは、まだ非表示に設定されていないため、表示されています。 アイコンをプレーヤーに非表示にするには、各ラベルの `Forecolor` プロパティをその `BackColor` プロパティと同じ色に設定できます。  
  
    > [!TIP]
    >  ラベルのようなコントロールを非表示にする別の方法は、**Visible** プロパティを `False` に設定することです。  
  
6.  アイコンを非表示にするには、プログラムを停止し、`For Each` ループ内のコードのコメント行からコメント記号を削除します。  
  
     [!code-cs[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_5.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_5.vb)]  
  
7.  メニュー バーで、[**すべて保存**] をクリックし、プログラムを保存したうえで実行します。 アイコンが非表示になったように見えます。青い背景のみが表示されます。 ただし、アイコンはランダムに割り当てられて、そこに存在しています。 アイコンは、背景と同じ色であるため、プレーヤーには見えなくなっています。 これで、ゲームはやりがいのあるものになりました。プレーヤーはすべてのアイコンをすぐに見ることができなくなったためです。  
  
### <a name="to-continue-or-review"></a>続行または確認するには  
  
-   チュートリアルの次の手順に進むには、「[手順 4: 各ラベルへの Click イベント ハンドラーの追加](../ide/step-4-add-a-click-event-handler-to-each-label.md)」を参照してください。  
  
-   チュートリアルの前の手順に戻るには、「[手順 2: Random オブジェクトおよびアイコンのリストの追加](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)」を参照してください。
