---
title: Windows フォームのデバッグ | Microsoft Docs
description: チュートリアルに従い、一般的なマネージド アプリケーションである Windows フォームを作成し、デバッグする方法について確認します。 C#、Visual Basic、C++、F# を使用できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- debugging managed code, Windows Forms
- debugging [Visual Studio], Windows Forms
- Attach to Process dialog box
- debugger, attaching to programs
- Attach to Process dialog box, walkthroughs
- Windows Forms, debugging
- debugging Windows Forms, walkthroughs
ms.assetid: 529db1e2-d9ea-482a-b6a0-7c543d17f114
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 73b58326bb594f275a508e5ba7fb17071f283ac2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385176"
---
# <a name="walkthrough-debugging-a-windows-form"></a>チュートリアル: Windows フォームのデバッグ
Windows フォームは、最も一般的なマネージド アプリケーションの 1 つです。 Windows フォームは、標準 Windows アプリケーションを作成します。 このチュートリアルは、Visual Basic、C#、または C++ を使用して実行できます。

 開いているソリューションがある場合は、ソリューションを閉じる必要があります。

### <a name="to-prepare-for-this-walkthrough"></a>このチュートリアルの準備をするには

- 既に開いているソリューションがある場合は、そのソリューションを閉じます。 ( **[ファイル]** メニューの **[ソリューションを閉じる]** をクリックします。)

## <a name="create-a-new-windows-form"></a>新しい Windows フォームを作成する
 次に、新しい Windows フォームを作成します。

#### <a name="to-create-the-windows-form-for-this-walkthrough"></a>このチュートリアルの Windows フォームを作成するには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. [プロジェクトの種類] ペインで、 **[Visual Basic]** ノード、 **[Visual C#]** ノード、または **[Visual C++]** ノードを開き、次の手順を行います。

    1. Visual Basic または Visual C# の場合は、 **[Windows デスクトップ]**  >  **[Windows フォーム アプリ]** を選択します。

    2. Visual C++ の場合は、 **[Windows デスクトップ アプリケーション]** を選択します。

3. **[プロジェクト名]** ボックスに、一意のプロジェクト名 (Walkthrough_SimpleDebug など) を入力します。

4. **[OK]** をクリックします。

     新しいプロジェクトが作成され、Windows フォーム デザイナーに新しいフォームが表示されます。 詳細については、「[Windows フォーム デザイナー](/previous-versions/visualstudio/visual-studio-2010/e06hs424\(v\=vs.100\))」を参照してください。

5. **[表示]** メニューの **[ツールボックス]** を選択します。

     ツールボックスが表示されます。 詳細については、「[ツールボックス](../ide/reference/toolbox.md)」をご覧ください。

6. ツールボックスの **[Button]** コントロールをクリックし、フォームのデザイン サーフェイスにドラッグします。 フォームに [Button] をドロップします。

7. ツールボックスの **[TextBox]** コントロールをクリックし、フォームのデザイン サーフェイスにドラッグします。 フォームに **[TextBox]** をドロップします。

8. フォームのデザイン サーフェイスで、ボタンをダブルクリックします。

     コード ページが表示されます。 カーソルは `button1_Click` 内にあります。

10. `button1_Click` 関数に、次のコードを追加します。

    ```vb
    textBox1.Text = "Button was clicked!"
    ```

    ```csharp
    textBox1.Text = "Button was clicked!";
    ```

    ```cpp
    textBox1->Text = "Button was clicked!";
    ```

11. **[ビルド]** メニューの **[ソリューションのビルド]** を選択します。

     プロジェクトがエラーのない状態でビルドされます。

## <a name="debug-your-form"></a>フォームをデバッグする
 これで、デバッグを開始する準備ができました。

#### <a name="to-debug-the-windows-form-created-for-this-walkthrough"></a>このチュートリアルで作成した Windows フォームをデバッグするには

1. ソース ウィンドウで、テキストを追加した行の左マージンをクリックします。

     ```vb
    textBox1.Text = "Button was clicked!"
    ```

    ```csharp
    textBox1.Text = "Button was clicked!";
    ```

    ```cpp
    textBox1->Text = "Button was clicked!";
    ```

     赤い点が表示され、その行のテキストが赤く強調表示されます。 赤い点はブレークポイントを表します。 詳細については、[ブレークポイント](/previous-versions/ktf38f66(v=vs.100))に関するページを参照してください。 デバッガーを起動した状態でアプリケーションを実行すると、そのコードに達したときにデバッガーが実行を中断します。 アプリケーションの状態を表示し、デバッグできます。

    > [!NOTE]
    > また、コードの任意の行で右クリックし、 **[ブレークポイント]** をポイントし、 **[ブレークポイントの挿入]** をクリックして、行にブレークポイントを設定することもできます。

2. **[デバッグ]** メニューの **[開始]** を選びます。

     Windows フォームの実行が開始されます。

3. Windows フォームで、追加したボタンをクリックします。

     Visual Studio では、コード ページのブレークポイントを設定した行に移動します。 行は黄色で強調表示されます。 ここで、アプリケーションの変数を確認し、実行を制御できます。 アプリケーションの実行は中断され、ユーザーのアクションを待っている状態です。

4. **[デバッグ]** メニューの **[ウィンドウ]** 、 **[ウォッチ]** を順にクリックし、 **[ウォッチ 1]** をクリックします。

5. **[ウォッチ 1]** ウィンドウで、空白行をクリックします。 **[名前]** 列に「`textBox1.Text`」(Visual Basic または Visual C# を使用している場合) または「`textBox1->Text`」(C++ を使用している場合) と入力し、Enter キーを押します。

     **[ウォッチ 1]** ウィンドウに、引用符で囲まれたこの変数の値が表示されます。

    `""`

6. **[デバッグ]** メニューの **[ステップ イン]** をクリックします。

     **[ウォッチ 1]** ウィンドウの textBox1.Text の値が次の値に変わります。

    `Button was clicked!`

7. プログラムのデバッグを再開するには、 **[デバッグ]** メニューの **[続行]** をクリックします。

8. Windows フォームで、再びボタンをクリックします。

     Visual Studio の実行が再び中断されます。

9. ブレークポイントを表す赤丸をクリックします。

     これにより、ブレークポイントがコードから削除されます。

10. **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。

## <a name="attach-to-your-windows-form-application-for-debugging"></a>デバッグする Windows フォーム アプリケーションにアタッチする
 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] では、デバッガーを実行中のプロセスにアタッチできます。 Express Edition を使用している場合、この機能はサポートされません。

#### <a name="to-attach-to-the-windows-form-application-for-debugging"></a>デバッグする Windows フォーム アプリケーションにアタッチするには

1. 作成したプロジェクトで、追加した行の左マージンをクリックして、再度ブレークポイントを設定します。

     ```vb
    textBox1.Text = "Button was clicked!"
    ```

    ```csharp
    textBox1.Text = "Button was clicked!";
    ```

    ```cpp
    textBox1->Text = "Button was clicked!";
    ```

2. **[デバッグ]** メニューの **[デバッグなしで開始]** を選択します。

     Windows フォームは、実行可能ファイルをダブルクリックしたときと同様に、Windows で実行を開始します。 デバッガーはアタッチされていません。

3. **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします (このコマンドは、 **[ツール]** メニューで選択することもできます)。

     **[プロセスにアタッチ]** ダイアログ ボックスが表示されます。

4. **[選択可能なプロセス]** ペインの **[プロセス]** 列で、プロセス名 (Walkthrough_SimpleDebug.exe) を探してクリックします。

5. **[アタッチ]** をクリックします。

6. Windows フォームで、1 つだけあるボタンをクリックします。

     ブレークポイントの位置で、Windows フォームの実行が中断します。

## <a name="see-also"></a>関連項目
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)