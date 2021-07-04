---
title: Web フォームをデバッグする | Microsoft Docs
description: チュートリアルに従い、ASP.NET Web アプリケーション (Web フォーム) をデバッグする方法について確認します。ブレークポイントの設定方法や変数の調べ方が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Web pages [.NET Framework], debugging
- Web sites [.NET Framework], debugging
- ASP.NET, debugging Web applications
- Web applications [.NET Framework], debugging
- ASP.NET Web sites, debugging
- ASP.NET Web pages, debugging
- debugging ASP.NET Web applications, Web Forms
- debugging [Visual Studio], Web Forms
ms.assetid: e2b4fa14-8f5b-444d-a903-54070b784bd4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 18347b7ba9ff52778b5acef685acd8f1ee400793
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385210"
---
# <a name="walkthrough-debugging-a-web-form"></a>チュートリアル: Web フォームのデバッグ
このチュートリアルでは、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーション (Web フォーム) をデバッグする方法について説明します。 実行の開始と終了の方法、ブレークポイントの設定方法、および **ウォッチ** ウィンドウでの変数の確認方法についても説明します。

> [!NOTE]
> このチュートリアルを完了するには、サーバー コンピューターに対する管理者特権が必要です。 既定では、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] プロセス (aspnet_wp.exe または w3wp.exe) は、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] プロセスとして実行されます。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] をデバッグするには、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] が実行されているコンピューターに対する管理者特権が必要です。 詳細については、「 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)」をご覧ください。

使用している設定またはエディションによっては、ヘルプの記載と異なるダイアログ ボックスやメニュー コマンドが表示される場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="to-create-the-web-form"></a>Web フォームを作成するには

1. 既に開いているソリューションがある場合は、そのソリューションを閉じます。

2. **[ファイル]** メニューで、 **[新規作成]** 、 **[Web サイト]** の順にクリックします。

    **[新しい Web サイト]** ダイアログ ボックスが表示されます。

3. **[テンプレート]** ペインの **[ASP.NET Web サイト]** をクリックします。

4. **[場所]** 行で、一覧の **[HTTP]** をクリックし、テキスト ボックスに「 **http://localhost/WebSite** 」と入力します。

5. **[言語]** ボックスの **[Visual C#]** または **[Visual Basic]** をクリックします。

6. **[OK]** をクリックします。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で新しいプロジェクトが作成され、既定の HTML ソース コードが表示されます。 また、IIS の **[既定の Web サイト]** の下に **[Web サイト]** という新しい仮想ディレクトリも作成されます。

7. 下部の余白の **[デザイン]** タブをクリックします。

8. 左のマージンにある **[ツールボックス]** タブをクリックするか、 **[表示]** メニューから選択します。

    **ツールボックス** が表示されます。

9. **ツールボックス** の **Button** コントロールをクリックし、主要なデザイン領域 (Default.aspx) に追加します。

10. **ツールボックス** の **Textbox** コントロールをクリックし、主要なデザイン領域 (Default.aspx) にドラッグします。

11. ドロップしたボタン コントロールをダブルクリックします。

     これにより、コード ページが表示されます (C# の場合は Default.aspx.cs、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] の場合は Default.aspx.vb)。 `Button1_Click` 関数の場所にカーソルがあります。

12. `Button1_Click` 関数に次のコードを追加します。

    ```vb
    TextBox1.Text = "Button was clicked!"
    ```

    ```csharp
    TextBox1.Text = "Button was clicked!";
    ```

13. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     プロジェクトがエラーのない状態でビルドされます。

     これで、デバッグを開始する準備ができました。

## <a name="to-debug-the-web-form"></a>Web フォームをデバッグするには

1. Default.aspx.cs または Default.aspx.vb ウィンドウで、テキストを追加した行の左の余白をクリックします。

   ```vb
   TextBox1.Text = "Button was clicked!"
   ```

   ```csharp
   textBox1.Text = "Button was clicked!";
   ```

    赤い点が表示され、その行のテキストが赤く強調表示されます。 赤い点はブレークポイントを表します。 デバッガーを起動した状態でアプリケーションを実行すると、そのコードに達したときにデバッガーが実行を中断します。 アプリケーションの状態を表示し、デバッグできます。 詳細については、[ブレークポイント](/previous-versions/ktf38f66(v=vs.100))に関するページを参照してください。

2. **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。

3. **[デバッグが無効です]** ダイアログ ボックスが表示されます。 **[デバッグを有効にするために Web.config ファイルを変更する]** をオンにして、 **[OK]** をクリックします。

    Internet Explorer が起動し、デザインしたページが表示されます。

4. Internet Explorer で、作成したボタンをクリックします。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、コード ページ Default.aspx.cs または Default.aspx.vb のブレークポイントを設定した行に移動します。 行は黄色で強調表示されます。 ここで、アプリケーションの変数を確認し、実行を制御できます。 アプリケーションの実行が中断され、コマンドの入力を待っている状態です。

5. **[デバッグ]** メニューの **[Windows]** 、 **[ウォッチ]** を順にクリックし、次に **[ウォッチ 1]** をクリックします。

6. **ウォッチ** ウィンドウに「**TextBox1.Text**」と入力します。

    **ウォッチ** ウィンドウに変数 `TextBox1.Text` の値が表示されます。

   '""'

7. **[デバッグ]** メニューの **[ステップ オーバー]** をクリックします。

    次のように、**ウォッチ** ウィンドウの `TextBox1.Text` の値が変更されます。

   `"Button was clicked!"`

8. **[デバッグ]** メニューの **[続行]** をクリックします。

9. Internet Explorer で、作成したボタンを再度クリックします。

     ブレークポイントで再度実行が中断されます。

10. Default.aspx.cs ウィンドウまたは Default.aspx.vb ウィンドウの左のマージンにある赤い点をクリックします。

     ブレークポイントが削除されます。

11. **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。

## <a name="to-attach-to-the-web-form-for-debugging"></a>デバッグする Web フォームにアタッチするには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、デバッガーを実行中のプロセスにアタッチできます。 デバッグの効率を最も高くするには、シンボル (PDB) ファイルを持つデバッグ バージョンとして実行可能ファイルをコンパイルします。

2. Default.aspx.cs ウィンドウまたは Default.aspx.vb ウィンドウの左のマージンをクリックして、追加した行に再度ブレークポイントを設定します。

   ```vb
   TextBox1.Text = "Button was clicked!"
   ```

   ```csharp
   textBox1.Text = "Button was clicked!";
   ```

3. **[デバッグ]** メニューの **[デバッグなしで開始]** をクリックします。

    Internet Explorer で Web フォームが起動しますが、デバッガーはアタッチされません。

4. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] プロセスにアタッチします。 詳細については、「[配置した Web アプリケーションのデバッグ](../debugger/debugging-deployed-web-applications.md)」を参照してください。

5. Internet Explorer で、フォームのボタンをクリックします。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で、Default.aspx.cs、Default.aspx.vb、または Default.aspx のブレークポイントにヒットします。

6. デバッグが終了したら、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。

## <a name="see-also"></a>関連項目

- [ASP.NET アプリケーションをデバッグする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)