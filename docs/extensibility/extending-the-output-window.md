---
title: 出力ウィンドウの拡張 | Microsoft Docs
description: Visual Studio SDK の出力ウィンドウを拡張し、独自のカスタム ウィンドウを作成および管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf875d070d27d307380f23e71af2bda7c4a205b5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075043"
---
# <a name="extend-the-output-window"></a>出力ウィンドウを拡張する
**出力** ウィンドウは、一連の読み取り/書き込みテキスト ウィンドウです。 Visual Studio には、プロジェクトによってビルドに関するメッセージを伝達する **ビルド** と [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって IDE に関するメッセージを伝達する **全般** という組み込みのウィンドウがあります。 プロジェクトでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> インターフェイス メソッドを使用して、**ビルド** ウィンドウへの参照が自動的に取得され、Visual Studio によって、<xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> サービスから、**全般** ウィンドウに直接アクセスできます。 組み込みのウィンドウに加えて、独自のカスタム ウィンドウを作成して管理することもできます。

 **出力** ウィンドウは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> インターフェイスと <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> インターフェイスを使用して直接制御できます。 <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> サービスによって提供される <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> インターフェイスは、**出力** ウィンドウ ペインを作成、取得、および破棄するためのメソッドを定義します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> インターフェイスは、ウィンドウの表示、ウィンドウの非表示、およびそれらのテキストの操作を行うためのメソッドを定義します。 **出力** ウィンドウを制御する別の方法として、Visual Studio オートメーション オブジェクト モデルの <xref:EnvDTE.OutputWindow> オブジェクトと <xref:EnvDTE.OutputWindowPane> オブジェクトを使用する方法があります。 これらのオブジェクトには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> インターフェイスと <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> インターフェイスのほぼすべての機能がカプセル化されています。 さらに、<xref:EnvDTE.OutputWindow> オブジェクトと <xref:EnvDTE.OutputWindowPane> オブジェクトにより、**出力** ウィンドウ ペインの列挙やウィンドウからのテキストの取得を簡単に行える上位レベルの機能が追加されます。

## <a name="create-an-extension-that-uses-the-output-pane"></a>出力ウィンドウを使用する拡張機能を作成する
 出力ウィンドウのさまざまな側面を実行する拡張機能を作成できます。

1. **TestOutput** という名前のメニュー コマンドを使用して、`TestOutput` という名前の VSIX プロジェクトを作成します。 詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. 次の参照を追加します。

    1. EnvDTE

    2. EnvDTE80

3. *TestOutput.cs* に、次の using ステートメントを追加します。

    ```f#
    using EnvDTE;
    using EnvDTE80;
    ```

4. *TestOutput.cs* で、`ShowMessageBox`メソッドを削除します。 次のメソッド スタブを追加します。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
    }
    ```

5. TestOutput コンストラクターで、コマンド ハンドラーを OutputCommandHandler に変更します。 コマンドを追加する部分を次に示します。

    ```csharp
    OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    if (commandService != null)
    {
        CommandID menuCommandID = new CommandID(MenuGroup, CommandId);
        EventHandler eventHandler = OutputCommandHandler;
        MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

6. 以下のセクションでは、出力ペインを扱うさまざまな方法を示すさまざまなメソッドを紹介します。 これらのメソッドは、`OutputCommandHandler()` メソッドの本体に対して呼び出すことができます。 たとえば、次のコードでは、次のセクションで示されている `CreatePane()` メソッドを追加します。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
        CreatePane(new Guid(), "Created Pane", true, false);
    }
    ```

## <a name="create-an-output-window-with-ivsoutputwindow"></a>IVsOutputWindow を使用して出力ウィンドウを作成する
 この例では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> インターフェイスを使用して、新しい **出力** ウィンドウ ペインを作成する方法を示します。

```csharp
void CreatePane(Guid paneGuid, string title,
    bool visible, bool clearWithSolution)
{
    IVsOutputWindow output =
        (IVsOutputWindow)GetService(typeof(SVsOutputWindow));
    IVsOutputWindowPane pane;

    // Create a new pane.
    output.CreatePane(
        ref paneGuid,
        title,
        Convert.ToInt32(visible),
        Convert.ToInt32(clearWithSolution));

    // Retrieve the new pane.
    output.GetPane(ref paneGuid, out pane);

     pane.OutputString("This is the Created Pane \n");
}
```

 前のセクションで指定した拡張機能にこのメソッドを追加した場合、 **[TestOutput の呼び出し]** コマンドをクリックすると、ウィンドウ自体に **出力元の表示: CreatedPane** と **This is the Created Pane** という語句を示すヘッダーのある **出力** ウィンドウが表示されるはずです。

## <a name="create-an-output-window-with-outputwindow"></a>OutputWindow を使用して出力ウィンドウを作成する
 この例では、<xref:EnvDTE.OutputWindow> オブジェクトを使って **出力** ウィンドウ ペインを作成する方法を示します。

```csharp
void CreatePane(string title)
{
    DTE2 dte = (DTE2)GetService(typeof(DTE));
    OutputWindowPanes panes =
        dte.ToolWindows.OutputWindow.OutputWindowPanes;

    try
    {
        // If the pane exists already, write to it.
        panes.Item(title);
    }
    catch (ArgumentException)
    {
        // Create a new pane and write to it.
        panes.Add(title);
    }
}
```

 <xref:EnvDTE.OutputWindowPanes> コレクションによって、**出力** ウィンドウ ペインをタイトルで取得できますが、ウィンドウのタイトルは確実に一意であるとは限りません。 タイトルが一意であるか疑わしい場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A> メソッドを使用して、正しいウィンドウをその GUID で取得します。

 前のセクションで指定した拡張機能にこのメソッドを追加した場合、 **[TestOutput の呼び出し]** コマンドをクリックすると、ウィンドウ自体に **出力元の表示: DTEPane** と **Added DTE Pane** という語句を示すヘッダーのある出力ウィンドウが表示されるはずです。

## <a name="delete-an-output-window"></a>出力ウィンドウを削除する
 この例では、**出力** ウィンドウ ペインを削除する方法を示します。

```csharp
void DeletePane(Guid paneGuid)
{
    IVsOutputWindow output =
    (IVsOutputWindow)ServiceProvider.GetService(typeof(SVsOutputWindow));

    IVsOutputWindowPane pane;
    output.GetPane(ref paneGuid, out pane);

    if (pane == null)
    {
        CreatePane(paneGuid, "New Pane\n", true, true);
    }
     else
    {
        output.DeletePane(ref paneGuid);
    }
}
```

 前のセクションで指定した拡張機能にこのメソッドを追加した場合、 **[TestOutput の呼び出し]** コマンドをクリックすると、ウィンドウ自体に **出力元の表示: New Pane** と **Added Created Pane** という語句を示すヘッダーのある出力ウィンドウが表示されるはずです。 **[TestOutput の呼び出し]** コマンドをもう一度クリックすると、ウィンドウが削除されます。

## <a name="get-the-general-pane-of-the-output-window"></a>出力ウィンドウの全般ウィンドウを取得する
 この例では、**出力** ウィンドウの組み込みの **全般** ウィンドウを取得する方法を示します。

```csharp
IVsOutputWindowPane GetGeneralPane()
{
    return (IVsOutputWindowPane)GetService(
        typeof(SVsGeneralOutputWindowPane));
}
```

 前のセクションで指定した拡張機能にこのメソッドを追加した場合、 **[TestOutput の呼び出し]** コマンドをクリックすると、ウィンドウに **Added Created Pane** という単語を示すヘッダーのある **出力** ウィンドウが表示されるはずです。

## <a name="get-the-build-pane-of-the-output-window"></a>出力ウィンドウのビルド ウィンドウを取得する
 この例では、**ビルド** ウィンドウを見つけて、それに書き込む方法を示します。 **ビルド** ウィンドウは既定でアクティブにされていないため、アクティブにします。

```csharp
void OutputTaskItemStringExExample(string buildMessage)
{
    EnvDTE80.DTE2 dte = (EnvDTE80.DTE2)ServiceProvider.GetService(typeof(EnvDTE.DTE));

    EnvDTE.OutputWindowPanes panes =
        dte.ToolWindows.OutputWindow.OutputWindowPanes;
    foreach (EnvDTE.OutputWindowPane pane in panes)
        {
            if (pane.Name.Contains("Build"))
            {
                pane.OutputString(buildMessage + "\n");
                pane.Activate();
                return;
             }
        }
}
```
