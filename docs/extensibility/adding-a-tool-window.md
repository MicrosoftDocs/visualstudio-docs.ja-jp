---
title: ツール ウィンドウの追加 | Microsoft Docs
description: ツール ウィンドウを作成し、コマンドを含むツール バーとコントロールをツール ウィンドウに追加することによって Visual Studio に統合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 314a684e34c91f43abe9babe4cdd6efc8a15cc35
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085521"
---
# <a name="add-a-tool-window"></a>ツール ウィンドウを追加する

このチュートリアルでは、次の手順でツール ウィンドウを作成し、Visual Studio に統合する方法について説明します。

- ツール ウィンドウにコントロールを追加します。

- ツール ウィンドウにツール バーを追加します。

- ツール バーにコマンドを追加します。

- コマンドを実装します。

- ツール ウィンドウの既定の位置を設定します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio SDK は、Visual Studio セットアップのオプション機能です。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-tool-window"></a>ツール ウィンドウを作成する

1. VSIX テンプレートを使用して **FirstToolWin** という名前のプロジェクトを作成し、**FirstToolWindow** という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツール ウィンドウでの拡張機能の作成について詳しくは、「[ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」をご覧ください。

## <a name="add-a-control-to-the-tool-window"></a>ツール ウィンドウにコントロールを追加する

1. 既定のコントロールを削除します。 *FirstToolWindowControl.xaml* を開き、 **[Click Me!]** ボタンを削除します。 を追加します。

2. **ツールボックス** で、 **[すべての WPF コントロール]** セクションを展開し、 **[メディア要素]** コントロールを **FirstToolWindowControl** フォームにドラッグします。 コントロールを選択し、 **[プロパティ]** ウィンドウで、この要素に **mediaElement1** という名前を付けます。

## <a name="add-a-toolbar-to-the-tool-window"></a>ツール ウィンドウにツール バーを追加する
次のようにツール バーを追加すると、そのグラデーションと色が IDE の他の部分と一致することが保証されます。

1. **ソリューション エクスプローラー** で、*FirstToolWindowPackage.vsct* を開きます。 *.vsct* ファイルでは、XML を使用して、ツール ウィンドウ内のグラフィカル ユーザー インターフェイス (GUI) 要素を定義します。

2. `<Symbols>` セクションで、`name` 属性が `guidFirstToolWindowPackageCmdSet` である `<GuidSymbol>` ノードを見つけます。 ツール バーとツール バー グループを定義するには、このノードの `<IDSymbol>` 要素のリストに次の 2 つの `<IDSymbol>` 要素を追加します。

    ```xml
    <IDSymbol name="ToolbarID" value="0x1000" />
    <IDSymbol name="ToolbarGroupID" value="0x1001" />
    ```

3. `<Buttons>` セクションのすぐ上に、次のような `<Menus>` セクションを作成します。

    ```xml
    <Menus>
        <Menu guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" priority="0x0000" type="ToolWindowToolbar">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
            <Strings>
                <ButtonText>Tool Window Toolbar</ButtonText>
                <CommandName>Tool Window Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

    メニューにはいくつかの種類があります。 このメニューはツール ウィンドウ内のツール バーであり、属性 `type` によって定義されています。 `guid` と `id` の設定からツール バーの完全修飾 ID が構成されます。 通常、メニューの `<Parent>` は、親グループです。 ただし、ツール バーは自身の親として定義されます。 したがって、`<Menu>` 要素と `<Parent>` 要素には同じ識別子が使用されます。 `priority` 属性は単に "0" です。

4. ツール バーは、さまざまな点でメニューに似ています。 たとえば、メニューにコマンドのグループが含まれる場合があるのと同様に、ツール バーにもグループが含まれる場合があります。 (メニューでは、コマンド グループは横線で区切られます。 ツール バーでは、グループは視覚的な区切り線で区切られていません)。

    `<Group>` 要素を含む `<Groups>` セクションを追加します。 これにより、`<Symbols>` セクションで宣言した ID を持つグループが定義されます。 `<Menus>` セクションの直後に `<Groups>` セクションを追加します。

    ```xml
    <Groups>
        <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
        </Group>
    </Groups>
    ```

    親の GUID と ID をツール バーの GUID と ID に設定すると、そのグループがツール バーに追加されます。

## <a name="add-a-command-to-the-toolbar"></a>ツール バーにコマンドを追加する

ツール バーにコマンドを追加します。これはボタンとして表示されます。

1. `<Symbols>` セクションで、ツール バーとツール バー グループの宣言の直後に、次の IDSymbol 要素を宣言します。

    ```xml
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />
    ```

2. `<Buttons>` セクション内に Button 要素を追加します。 この要素は、ツール ウィンドウ内のツール バーに、**検索** (虫眼鏡) アイコンで表示されます。

    ```xml
    <Button guid="guidFirstToolWindowPackageCmdSet" id="cmdidWindowsMediaOpen" priority="0x0101" type="Button">
        <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID"/>
        <Icon guid="guidImages" id="bmpPicSearch" />
        <Strings>
            <CommandName>cmdidWindowsMediaOpen</CommandName>
            <ButtonText>Load File</ButtonText>
        </Strings>
    </Button>
    ```

3. *FirstToolWindowCommand.cs* を開き、既存のフィールドの直後に次の行をクラスに追加します。

    ```csharp
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const uint cmdidWindowsMedia = 0x100;
    public const int cmdidWindowsMediaOpen = 0x132;
    public const int ToolbarID = 0x1000;
    ```

    これにより、コードでコマンドを使用できるようになります。

## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>MediaPlayer プロパティを FirstToolWindowControl に追加する
コードでは、ツール バー コントロールのイベント ハンドラーから、FirstToolWindowControl クラスの子である Media Player コントロールにアクセスできる必要があります。

**ソリューション エクスプローラー** で、*FirstToolWindowControl.xaml* を右クリックし、 **[コードの表示]** をクリックして、FirstToolWindowControl クラスに次のコードを追加します。

```csharp
public System.Windows.Controls.MediaElement MediaPlayer
{
    get { return mediaElement1; }
}
```

## <a name="instantiate-the-tool-window-and-toolbar"></a>ツール ウィンドウとツールバーをインスタンス化する
ツール バーを追加し、 **[ファイルを開く]** ダイアログを起動して選択されたメディア ファイルを再生するメニュー コマンドを追加します。

1. *FirstToolWindow.cs* を開き、次の `using` ディレクティブを追加します。

    ```csharp
    using System.ComponentModel.Design;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. FirstToolWindow クラス内に、FirstToolWindowControl コントロールへのパブリック参照を追加します。

    ```csharp
    public FirstToolWindowControl control;
    ```

3. コンストラクターの末尾で、このコントロール変数を新しく作成したコントロールに設定します。

    ```csharp
    control = new FirstToolWindowControl();
    base.Content = control;
    ```

4. コンストラクター内でツール バーをインスタンス化します。

    ```csharp
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.ToolbarID);
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    ```

5. この時点で、FirstToolWindow コンストラクターは次のようになります。

    ```csharp
    public FirstToolWindow() : base(null)
    {
        this.Caption = "FirstToolWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
        control = new FirstToolWindowControl();
        base.Content = control;
        this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.ToolbarID);
            this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    }
    ```

6. ツール バーにメニュー コマンドを追加します。 FirstToolWindowCommand.cs クラスで、次の using ディレクティブを追加します。

    ```csharp
    using System.Windows.Forms;
    ```

7. FirstToolWindowCommand クラスで、ShowToolWindow() メソッドの末尾に次のコードを追加します。 ButtonHandler コマンドは、次のセクションで実装されます。

    ```csharp
    // Create the handles for the toolbar command.
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.cmdidWindowsMediaOpen);
    var menuItem = new MenuCommand(new EventHandler(
        ButtonHandler), toolbarbtnCmdID);
    mcs.AddCommand(menuItem);
    ```

### <a name="to-implement-a-menu-command-in-the-tool-window"></a>ツール ウィンドウにメニュー コマンドを実装するには

1. FirstToolWindowCommand クラスに、 **[ファイルを開く]** ダイアログを呼び出す ButtonHandler メソッドを追加します。 ファイルが選択されると、メディア ファイルが再生されます。

2. FirstToolWindowCommand クラスに、FindToolWindow() メソッドで作成される FirstToolWindow ウィンドウへのプライベート参照を追加します。

    ```csharp
    private FirstToolWindow window;
    ```

3. ShowToolWindow() メソッドを変更して、上で定義したウィンドウを設定します。これにより、ButtonHandler コマンド ハンドラーがウィンドウ コントロールにアクセスできるようになります。 完全な ShowToolWindow() メソッドを次に示します。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        window = (FirstToolWindow) this.package.FindToolWindow(typeof(FirstToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create tool window");
        }

        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommandguidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.cmdidWindowsMediaOpen);
        var menuItem = new MenuCommand(new EventHandler(
            ButtonHandler), toolbarbtnCmdID);
        mcs.AddCommand(menuItem);
    }
    ```

4. ButtonHandler メソッドを追加します。 これは、ユーザーが再生するメディア ファイルを指定するための OpenFileDialog を作成してから、選択されたファイルを再生します。

    ```csharp
    private void ButtonHandler(object sender, EventArgs arguments)
    {
        OpenFileDialog openFileDialog = new OpenFileDialog();
        DialogResult result = openFileDialog.ShowDialog();
        if (result == DialogResult.OK)
        {
            window.control.MediaPlayer.Source = new System.Uri(openFileDialog.FileName);
        }
    }
    ```

## <a name="set-the-default-position-for-the-tool-window"></a>ツール ウィンドウの既定の位置を設定する

次に、IDE でのツール ウィンドウの既定位置を指定します。 ツール ウィンドウの構成情報は、*FirstToolWindowPackage.cs* ファイルにあります。

1. *FirstToolWindowPackage.cs* で、`FirstToolWindowPackage` クラスの <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 属性を見つけます。これにより、 FirstToolWindow 型がコンストラクターに渡されます。 既定の位置を指定するには、次の例のように、コンストラクターにさらにパラメーターを追加する必要があります。

    ```csharp
    [ProvideToolWindow(typeof(FirstToolWindow),
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
    ```

    最初の名前付きパラメーターは `Style` で、その値は `Tabbed` です。これは、ウィンドウが既存のウィンドウのタブになることを意味します。 ドッキング位置は、`Window` パラメーターによって指定されます。このケースでは、**ソリューション エクスプローラー** の GUID です。

    > [!NOTE]
    > IDE のウィンドウの種類の詳細については、<xref:EnvDTE.vsWindowType> を参照してください。

## <a name="test-the-tool-window"></a>ツール ウィンドウをテストする

1. **F5** キーを押して、Visual Studio 試験的ビルドの新しいインスタンスを開きます。

2. **[表示]** メニューの **[その他のウィンドウ]** をポイントし、 **[最初のツール ウィンドウ]** をクリックします。

    メディア プレーヤーのツール ウィンドウが **ソリューション エクスプローラー** と同じ位置で開くはずです。 まだ以前と同じ位置に表示される場合は、ウィンドウのレイアウトをリセットします ( **[ウィンドウ] / [ウィンドウ レイアウトのリセット]** )。

3. ツール ウィンドウで、ボタン (**検索** アイコンが表示されています) をクリックします。 サポートされているサウンド ファイルまたはビデオ ファイル (たとえば、*C:\windows\media\chimes.wav*) を選択し、 **[開く]** を押します。

    チャイム音が聞こえます。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
