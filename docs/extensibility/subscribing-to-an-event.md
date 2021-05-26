---
title: イベントのサブスクライブ | Microsoft Docs
description: Visual Studio SDK で実行中のドキュメント テーブル内のイベントに応答するツール ウィンドウを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a887e7d50f14c76cf993eae64b0efd88dee2181
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056286"
---
# <a name="subscribing-to-an-event"></a>イベントのサブスクライブ
このチュートリアルでは、実行中のドキュメント テーブル (RDT) 内のイベントに応答するツール ウィンドウを作成する方法について説明します。 ツール ウィンドウでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> を実装するユーザー コントロールをホストします。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> メソッドでは、そのインターフェイスをイベントに接続します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="subscribing-to-rdt-events"></a>RDT イベントのサブスクライブ

#### <a name="to-create-an-extension-with-a-tool-window"></a>ツール ウィンドウで拡張機能を作成するには

1. VSIX テンプレートを使用して **RDTExplorer** という名前のプロジェクトを作成し、**RDTExplorerWindow** という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

     ツール ウィンドウでの拡張機能の作成について詳しくは、「[ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」をご覧ください。

#### <a name="to-subscribe-to-rdt-events"></a>RDT イベントをサブスクライブするには

1. RDTExplorerWindowControl.xaml ファイルを開き、`button1` という名前のボタンを削除します。 <xref:System.Windows.Forms.ListBox> コントロールを追加し、既定の名前をそのまま使用します。 Grid 要素は次のようになります。

    ```xml
    <Grid>
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>
            <ListBox x:Name="listBox" Height="100" />
        </StackPanel>
    </Grid>
    ```

2. コード ビューで RDTExplorerWindow.cs ファイルを開きます。 そのファイルの先頭に次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> クラスから派生することに加え、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> インターフェイスも実装するように `RDTExplorerWindow` クラスを変更します。

    ```csharp
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents
    {. . .}
    ```

4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>を実装します。

    - そのインターフェイスを実装します。 IVsRunningDocTableEvents 名にカーソルを置きます。 左余白に電球が表示されます。 電球の右側にある下矢印をクリックし、 **[インターフェイスの実装]** を選択します。

5. インターフェイスの各メソッドで、`throw new NotImplementedException();` 行を次のように置き換えます。

    ```csharp
    return VSConstants.S_OK;
    ```

6. cookie フィールドを RDTExplorerWindow クラスに追加します。

    ```csharp
    private uint rdtCookie;
    ```

     これには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> メソッドから返される cookie が入ります。

7. RDTExplorerWindow の Initialize() メソッドをオーバーライドして、RDT イベントに登録します。 必ず、コンストラクターではなく ToolWindowPane の Initialize() メソッドでサービスを取得するようにしてください。

    ```csharp
    protected override void Initialize()
    {
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
        this.GetService(typeof(SVsRunningDocumentTable));
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);
    }
    ```

     <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> サービスが呼び出されて、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> インターフェイスが取得されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> メソッドにより、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> (この場合は RDTExplorer オブジェクト) を実装するオブジェクトに RDT イベントが接続されます。

8. RDTExplorerWindow の Dispose() メソッドを更新します。

    ```csharp
    protected override void Dispose(bool disposing)
    {
        // Release the RDT cookie.
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
            Package.GetGlobalService(typeof(SVsRunningDocumentTable));
        rdt.UnadviseRunningDocTableEvents(rdtCookie);

        base.Dispose(disposing);
    }
    ```

     <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A> メソッドにより、`RDTExplorer` と RDT イベント通知の間の接続が削除されます。

9. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A> ハンドラーの本体の `return` ステートメントの直前に、次の行を追加します。

    ```csharp
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");
        return VSConstants.S_OK;
    }
    ```

10. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A> ハンドラーの本体 と、リスト ボックスに表示させるその他のイベントに同様の行を追加します。

    ```csharp
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");
        return VSConstants.S_OK;
    }
    ```

11. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

12. **RDTExplorerWindow** ( **[表示] > [その他のウィンドウ] > [RDTExplorerWindow]** ) を開きます。

     **RDTExplorerWindow** ウィンドウが開き、空のイベント リストが表示されます。

13. ソリューションを開くか、作成します。

     `OnBeforeLastDocument` および `OnAfterFirstDocument` イベントが発生し、各イベントの通知がイベント リストに表示されます。
