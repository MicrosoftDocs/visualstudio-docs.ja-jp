---
title: ステータス バーの拡張 | Microsoft Docs
description: IDE の下部にある Visual Studio のステータス バーを拡張して、情報を表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- status bars, about status bars
- status bars, overview
ms.assetid: f955115c-4c5f-45ec-b41b-365868c5ec0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5ab87f9c8b54d9c31466068668eb8dd5a1857a06
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070103"
---
# <a name="extend-the-status-bar"></a>ステータス バーを拡張する
IDE の下部にある Visual Studio のステータス バーを使用して、情報を表示できます。

 ステータス バーを拡張すると、フィードバック領域、進行状況バー、アニメーション領域、およびデザイナー領域の 4 つの領域に情報と UI を表示できます。 フィードバック領域を使用すると、テキストを表示したり、表示されているテキストを強調表示したりすることができます。 進行状況バーには、ファイルの保存など、実行時間の短い操作の増分の進行状況が表示されます。 アニメーション領域には、ソリューション内での複数のプロジェクトのビルドなど、実行時間の長い操作や長さが不確定の操作のために、連続的にループするアニメーションが表示されます。 また、デザイナー領域には、カーソル位置の行番号と列番号が表示されます。

 ステータス バーは、(<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> サービスから) <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> インターフェイスを使用して取得できます。 さらに、ウィンドウ フレームに配置されるオブジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> インターフェイスの実装によりステータス バーのクライアント オブジェクトとして登録できます。 ウィンドウがアクティブにされるたびに、Visual Studio からそのウィンドウに配置されているオブジェクトに対して `IVsStatusbarUser` インターフェイスが照会されます。 見つかった場合は、返されたインターフェイスで <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> メソッドが呼び出され、オブジェクトにより、そのメソッド内からステータス バーを更新できるようになります。 たとえば、ドキュメント ウィンドウで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> メソッドを使用して、デザイナー領域がアクティブになったときにその中の情報を更新できます。

 次の手順は、VSIX プロジェクトを作成し、カスタム メニュー コマンドを追加する方法について理解していることを前提としています。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

## <a name="modify-the-status-bar"></a>ステータス バーを変更する
 この手順では、ステータス バーのフィードバック領域におけるテキストの設定と取得、静的なテキストの表示、表示されているテキストの強調表示を行う方法について説明します。

### <a name="read-and-write-to-the-status-bar"></a>ステータス バーの読み取りと書き込み

1. **TestStatusBarExtension** という名前の VSIX プロジェクトを作成し、**TestStatusBarCommand** という名前のメニュー コマンドを追加します。

2. *TestStatusBarCommand.cs* で、コマンド ハンドラーのメソッド コード (`MenuItemCallback`) を次の内容に置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Make sure the status bar is not frozen
        int frozen;

        statusBar.IsFrozen(out frozen);

        if (frozen != 0)
        {
            statusBar.FreezeOutput(0);
        }

        // Set the status bar text and make its display static.
        statusBar.SetText("We just wrote to the status bar.");

        // Freeze the status bar.
        statusBar.FreezeOutput(1);

        // Get the status bar text.
        string text;
        statusBar.GetText(out text);
        System.Windows.Forms.MessageBox.Show(text);

        // Clear the status bar text.
        statusBar.FreezeOutput(0);
        statusBar.Clear();
    }
    ```

3. コードをコンパイルし、デバッグを開始します。

4. Visual Studio の実験用インスタンスで **[ツール]** メニューを開きます。 **[Invoke TestStatusBarCommand]\(TestStatusBarCommand の呼び出し\)** ボタンをクリックします。

     ステータス バーのテキストに "**We just wrote to the status bar.** " と表示され、 表示されるメッセージ ボックスも同じテキストになります。

### <a name="update-the-progress-bar"></a>進行状況バーを更新する

1. この手順では、進行状況バーを初期化して更新する方法について説明します。

2. *TestStatusBarCommand.cs* ファイルを開き、`MenuItemCallback` メソッドを次のコードに置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));
        uint cookie = 0;
        string label = "Writing to the progress bar";

        // Initialize the progress bar.
        statusBar.Progress(ref cookie, 1, "", 0, 0);

        for (uint i = 0, total = 20; i <= total; i++)
        {
            // Display progress every second.
            statusBar.Progress(ref cookie, 1, label, i, total);
            System.Threading.Thread.Sleep(1000);
        }

        // Clear the progress bar.
        statusBar.Progress(ref cookie, 0, "", 0, 0);
    }
    ```

3. コードをコンパイルし、デバッグを開始します。

4. Visual Studio の実験用インスタンスで **[ツール]** メニューを開きます。 **[Invoke TestStatusBarCommand]\(TestStatusBarCommand の呼び出し\)** ボタンをクリックします。

     ステータス バーのテキストに "**Writing to the progress bar**" と表示されます。 また、20 秒間、進行状況バーが 1 秒ごとに更新されていることがわかります。 その後、ステータス バーと進行状況バーがクリアされます。

### <a name="display-an-animation"></a>アニメーションを表示する

1. ステータス バーには、実行時間の長い操作 (ソリューション内での複数のプロジェクトのビルドなど) を示すループするアニメーションが表示されます。 このアニメーションが表示されない場合は、 **[ツール]**  >  **[オプション]** の設定が適切であることを確認します。

     **[ツール]**  >  **[オプション]**  >  **[全般]** タブに移動し、 **[クライアントのパフォーマンスに基づいて視覚的効果を自動的に調整する]** をオフにします。 次に、 **[リッチ クライアントの視覚的効果を有効にする]** サブ オプションをオンにします。 これで、Visual Studio の実験用インスタンスでプロジェクトをビルドするときにアニメーションが表示されるようになります。

     この手順で、プロジェクトまたはソリューションのビルドを表す標準の Visual Studio アニメーションを表示します。

2. *TestStatusBarCommand.cs* ファイルを開き、`MenuItemCallback` メソッドを次のコードに置き換えます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar =(IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Use the standard Visual Studio icon for building.
        object icon = (short)Microsoft.VisualStudio.Shell.Interop.Constants.SBAI_Build;

        // Display the icon in the Animation region.
        statusBar.Animation(1, ref icon);

        // The message box pauses execution for you to look at the animation.
        System.Windows.Forms.MessageBox.Show("showing?");

        // Stop the animation.
        statusBar.Animation(0, ref icon);
    }
    ```

3. コードをコンパイルし、デバッグを開始します。

4. Visual Studio の実験用インスタンスで **[ツール]** メニューを開き、 **[Invoke TestStatusBarCommand]\(TestStatusBarCommand の呼び出し\)** をクリックします。

     メッセージ ボックスが表示されると、右端にあるステータス バーにアニメーションが表示されます。 メッセージ ボックスを閉じると、アニメーションは表示されなくなります。
