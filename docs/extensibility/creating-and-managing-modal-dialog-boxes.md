---
title: モーダル ダイアログ ボックスの作成と管理 | Microsoft Docs
description: DialogWindow を使用する場合と DialogWindow を使用しない場合の両方で、Visual Studio 内にモーダル ダイアログ ボックスを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 96ac3c9ee92cd9124485dde29814f4a1e5c942c8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055753"
---
# <a name="create-and-manage-modal-dialog-boxes"></a>モーダル ダイアログ ボックスの作成と管理
Visual Studio 内にモーダル ダイアログ ボックスを作成する場合は、そのダイアログ ボックスが表示されている間はダイアログ ボックスの親ウィンドウが必ず無効になるようにし、そのダイアログ ボックスが閉じた後で親ウィンドウを再び有効にする必要があります。 そうしないと、*Microsoft Visual Studio cannot shut down because a modal dialog is active. Close the active dialog and try again.* (モーダル ダイアログがアクティブになっているため、Microsoft Visual Studio をシャットダウンできません。アクティブなダイアログを閉じてから、もう一度お試しください。) というエラーが表示される可能性があります。

これを行うには 2 つの方法があります。 推奨される方法 (WPF ダイアログ ボックスがある場合) は、<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> からそれを派生させた後、<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A> を呼び出してそのダイアログ ボックスを表示することです。 これを行うと、親ウィンドウのモーダル状態を管理する必要がなくなります。

お使いのダイアログ ボックスが WPF でない場合、または他の何らかの理由で <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> からダイアログ ボックス クラスを派生できない場合は、ダイアログ ボックスの親を取得する必要があります。そのためには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A> を呼び出してモーダル状態を自身で管理するか、ダイアログ ボックスの表示前にパラメーター 0 (false) を指定して <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A> メソッドを呼び出し、ダイアログ ボックスのクローズ後にパラメーター 1 (true) を指定してそのメソッドを呼び出します。

## <a name="create-a-dialog-box-derived-from-dialogwindow"></a>DialogWindow から派生したダイアログ ボックスを作成する

1. **OpenDialogTest** という名前の VSIX プロジェクトを作成し、**OpenDialog** という名前のメニュー コマンドを追加します。 この方法の詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」をご覧ください。

2. <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> クラスを使用するために、以下のアセンブリへの参照を追加する必要があります ( **[参照の追加]** ダイアログ ボックスの [フレームワーク] タブを使用)。

    - *PresentationCore*

    - *PresentationFramework*

    - *WindowsBase*

    - *System.Xaml*

3. *OpenDialog.cs* に、次の `using` ステートメントを追加します。

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    ```

4. <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> から派生する `TestDialogWindow` という名前のクラスを宣言します。

    ```csharp
    class TestDialogWindow : DialogWindow
    {. . .}
    ```

5. ダイアログ ボックスを最小化および最大化できるようにするために、<xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A> と <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A> を true に設定します。

    ```csharp
    internal TestDialogWindow()
    {
        this.HasMaximizeButton = true;
        this.HasMinimizeButton = true;
    }
    ```

6. `OpenDialog.ShowMessageBox` メソッド内で、既存のコードを次のように置き換えます。

    ```csharp
    TestDialogWindow testDialog = new TestDialogWindow();
    testDialog.ShowModal();
    ```

7. アプリケーションをビルドして実行します。 Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの **[ツール]** メニューに、**Invoke OpenDialog** という名前のコマンドが表示されます。 このコマンドをクリックすると、ダイアログ ウィンドウが表示されます。 ウィンドウを最小化および最大化できるようになります。

## <a name="create-and-manage-a-dialog-box-not-derived-from-dialogwindow"></a>DialogWindow から派生していないダイアログ ボックスを作成して管理する

1. この手順では、前の手順で作成した **OpenDialogTest** ソリューションと、同じアセンブリ参照を使用できます。

2. 次の `using` 宣言を追加します。

    ```csharp
    using System.Windows;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    ```

3. <xref:System.Windows.Window> から派生する `TestDialogWindow2` という名前のクラスを作成します。

    ```csharp
    class TestDialogWindow2 : Window
    {. . .}
    ```

4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> へのプライベート参照を追加します。

    ```
    private IVsUIShell shell;
    ```

5. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> への参照を設定するコンストラクターを追加します。

    ```csharp
    public TestDialogWindow2(IVsUIShell uiShell)
    {
        shell = uiShell;
    }
    ```

6. `OpenDialog.ShowMessageBox` メソッド内で、既存のコードを次のように置き換えます。

    ```csharp
    IVsUIShell uiShell = (IVsUIShell)ServiceProvider.GetService(typeof(SVsUIShell));

    TestDialogWindow2 testDialog2 = new TestDialogWindow2(uiShell);
    //get the owner of this dialog
    IntPtr hwnd;
    uiShell.GetDialogOwnerHwnd(out hwnd);
    testDialog2.WindowStartupLocation = System.Windows.WindowStartupLocation.CenterOwner;
    uiShell.EnableModeless(0);
    try
    {
        WindowHelper.ShowModal(testDialog2, hwnd);
    }
    finally
    {
        // This will take place after the window is closed.
        uiShell.EnableModeless(1);
    }
    ```

7. アプリケーションをビルドして実行します。 **[ツール]** メニューに、**Invoke OpenDialog** という名前のコマンドが表示されます。 このコマンドをクリックすると、ダイアログ ウィンドウが表示されます。
