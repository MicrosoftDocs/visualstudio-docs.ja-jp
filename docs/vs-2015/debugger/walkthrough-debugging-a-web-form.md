---
title: 'チュートリアル: Web フォームのデバッグ |Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
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
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7024a9abc58117bf28ed78de107b1c17ddad601f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51747268"
---
# <a name="walkthrough-debugging-a-web-form"></a>チュートリアル : Web フォームのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web アプリケーション (Web フォーム) をデバッグする方法について説明します。 開始し実行を停止、ブレークポイントを設定およびで変数を確認する方法を示します、**ウォッチ**ウィンドウ。  
  
> [!NOTE]
>  このチュートリアルを完了するには、サーバー コンピューターに対する管理者特権が必要です。 既定では、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] プロセス (aspnet_wp.exe または w3wp.exe) は、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] プロセスとして実行されます。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] をデバッグするには、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] が実行されているコンピューターに対する管理者特権が必要です。 詳細については、「 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)」をご覧ください。  
  
 使用している設定またはエディションによっては、ヘルプの記載と異なるダイアログ ボックスやメニュー コマンドが表示される場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-create-the-web-form"></a>Web フォームを作成するには  
  
1.  既に開いているソリューションがある場合は、そのソリューションを閉じます。  
  
2.  **ファイル** メニューのをクリックして**新規**、 をクリックし、 **Web サイト**します。  
  
     **新しい Web サイト** ダイアログ ボックスが表示されます。  
  
3.  **テンプレート**ウィンドウで、をクリックして**ASP.NET Web サイト**します。  
  
4.  **場所**行、 をクリックして**HTTP** 、一覧から、テキスト ボックスには、入力 **http://localhost/WebSite**します。  
  
5.  **言語**一覧で、 **Visual c#** または**Visual Basic**します。  
  
6.  **[OK]** をクリックします。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で新しいプロジェクトが作成され、既定の HTML ソース コードが表示されます。 という名前の新しい仮想ディレクトリも作成**web サイト****既定の Web サイト**IIS でします。  
  
7.  をクリックして、**デザイン**下余白のタブ。  
  
8.  をクリックして、**ツールボックス**左の余白のタブまたはで選択し、**ビュー**メニュー。  
  
     **ツールボックス** が表示されます。  
  
9. **ツールボックス**、クリックして、**ボタン**を制御し、Default.aspx、メインのデザイン サーフェイスに追加します。  
  
10. **ツールボックス**、クリックして、 **Textbox**制御、および Default.aspx、メインのデザイン サーフェイスにドラッグします。  
  
11. ドロップしたボタン コントロールをダブルクリックします。  
  
     これで、コード ページが表示されます。C# の場合は Default.aspx.cs、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] の場合は Default.aspx.vb です。 `Button1_Click` 関数の場所にカーソルがあります。  
  
12. `Button1_Click` 関数に次のコードを追加します。  
  
    ```  
    ' Visual Basic  
    TextBox1.Text = "Button was clicked!"  
  
    // C#  
    TextBox1.Text = "Button was clicked!";  
    ```  
  
13. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
     プロジェクトがエラーのない状態でビルドされます。  
  
     これで、デバッグを開始する準備ができました。  
  
### <a name="to-debug-the-web-form"></a>Web フォームをデバッグするには  
  
1.  Default.aspx.cs または Default.aspx.vb ウィンドウで、テキストを追加した行の左の余白をクリックします。  
  
    ```  
    ' Visual Basic  
    TextBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
    ```  
  
     赤い点が表示され、その行のテキストが赤く強調表示されます。 赤い点はブレークポイントを表します。 デバッガーを起動した状態でアプリケーションを実行すると、そのコードに達したときにデバッガーが実行を中断します。 アプリケーションの状態を表示し、デバッグできます。 詳細については、[ブレークポイント](http://msdn.microsoft.com/en-us/fe4eedc1-71aa-4928-962f-0912c334d583)を参照してください。  
  
2.  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
3.  **デバッグが無効** ダイアログ ボックスが表示されます。 選択**デバッグを有効にする Web.config ファイルを変更** をクリックし、 **OK**します。  
  
     Internet Explorer が起動し、デザインしたページが表示されます。  
  
4.  Internet Explorer で、作成したボタンをクリックします。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、コード ページ Default.aspx.cs または Default.aspx.vb のブレークポイントを設定した行に移動します。 行は黄色で強調表示されます。 ここで、アプリケーションの変数を確認し、実行を制御できます。 アプリケーションの実行が中断され、コマンドの入力を待っている状態です。  
  
5.  **デバッグ** メニューのをクリックして**Windows**、 をクリックし、**ウォッチ**、順にクリックします**ウォッチ 1**します。  
  
6.  **ウォッチ**ウィンドウで、「 **TextBox1.Text**します。  
  
     **ウォッチ**ウィンドウには、変数の値が表示されます`TextBox1.Text`:。  
  
    ```  
    ""  
    ```  
  
7.  **デバッグ** メニューのをクリックして**ステップ オーバー**します。  
  
     値`TextBox1.Text`の変更、**ウォッチ**ウィンドウ。  
  
    ```  
    "Button was clicked!"  
    ```  
  
8.  **デバッグ** メニューのをクリックして**続行**します。  
  
9. Internet Explorer で、作成したボタンを再度クリックします。  
  
     ブレークポイントで再度実行が中断されます。  
  
10. Default.aspx.cs ウィンドウまたは Default.aspx.vb ウィンドウの左のマージンにある赤い点をクリックします。  
  
     ブレークポイントが削除されます。  
  
11. **デバッグ** メニューのをクリックして**デバッグの停止**します。  
  
### <a name="to-attach-to-the-web-form-for-debugging"></a>デバッグする Web フォームにアタッチするには  
  
1.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、デバッガーを実行中のプロセスにアタッチできます。 デバッグの効率を最も高くするには、シンボル (PDB) ファイルを持つデバッグ バージョンとして実行可能ファイルをコンパイルします。  
  
2.  Default.aspx.cs ウィンドウまたは Default.aspx.vb ウィンドウの左のマージンをクリックして、追加した行に再度ブレークポイントを設定します。  
  
    ```  
    ' Visual Basic  
    TextBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
    ```  
  
3.  **デバッグ** メニューのをクリックして**デバッグなしで開始**します。  
  
     Internet Explorer で Web フォームが起動しますが、デバッガーはアタッチされません。  
  
4.  [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] プロセスにアタッチします。 詳細については、[デプロイされた Web アプリケーションのデバッグ](../debugger/debugging-deployed-web-applications.md)を参照してください。  
  
5.  Internet Explorer で、フォームのボタンをクリックします。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で、Default.aspx.cs、Default.aspx.vb、または Default.aspx のブレークポイントにヒットします。  
  
6.  終了するときに、デバッグ、**デバッグ** メニューのをクリックして**デバッグの停止**。  
  
## <a name="see-also"></a>関連項目  
 [ASP.NET アプリケーションおよび AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)



