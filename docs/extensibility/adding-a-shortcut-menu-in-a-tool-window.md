---
title: ツール ウィンドウへのショートカット メニューの追加 | Microsoft Docs
description: ボタン、テキスト ボックス、またはウィンドウの背景を右クリックしたときに表示されるショートカット メニューを、Visual Studio のツール ウィンドウに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- context menus, adding to tool windows
- menus, context menus
- shortcut menus, adding to tool windows
- tool windows, adding context menus
ms.assetid: 50234537-9e95-4b7e-9cb7-e5cf26d6e9d2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3ba0eb2324812ca7536b361d602bb683d627c743
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097618"
---
# <a name="add-a-shortcut-menu-in-a-tool-window"></a>ツール ウィンドウにショートカット メニューを追加する
このチュートリアルでは、ツール ウィンドウにショートカット メニューを追加します。 ショートカット メニューは、ユーザーがボタン、テキスト ボックス、またはウィンドウの背景を右クリックしたときに表示されるメニューです。 ショートカット メニューのコマンドは、他のメニューやツール バーのコマンドと同じように動作します。 ショートカット メニューをサポートするには、 *.vsct* ファイルでそれを指定し、マウスの右クリックに応答して表示されるようにします。

ツール ウィンドウは、<xref:Microsoft.VisualStudio.Shell.ToolWindowPane> から継承されるカスタム ツール ウィンドウ クラスの WPF ユーザー コントロールで構成されます。

このチュートリアルでは、ショートカット メニューを Visual Studio メニューとして作成する方法について説明します。方法としては、 *.vsct* ファイルでメニュー項目を宣言し、その後、Managed Package Framework を使用して、ツール ウィンドウを定義するクラスにそれらを実装します。 この方法を使用すると、Visual Studio のコマンド、UI 要素、およびオートメーション オブジェクト モデルに簡単にアクセスできるようになります。

なお、ショートカット メニューから Visual Studio の機能にアクセスしない場合は、ユーザー コントロールで XAML 要素の <xref:System.Windows.FrameworkElement.ContextMenu%2A> プロパティを使用することもできます。 詳細については、「[ContextMenu](/dotnet/framework/wpf/controls/contextmenu)」をご覧ください。

## <a name="prerequisites"></a>前提条件
Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールすることはしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」をご覧ください。

## <a name="create-the-tool-window-shortcut-menu-package"></a>ツール ウィンドウのショートカット メニュー パッケージを作成する

1. `TWShortcutMenu` という VSIX プロジェクトを作成し、それに **ShortcutMenu** というツール ウィンドウ テンプレートを追加します。 ツール ウィンドウの作成について詳しくは、「[ツール ウィンドウで拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)」をご覧ください。

## <a name="specifying-the-shortcut-menu"></a>ショートカット メニューの指定
このチュートリアルに示すようなショートカット メニューを追加すると、ツール ウィンドウの背景の塗りつぶしに使用する色の一覧から、ユーザーが色を選択できるようになります。

1. *ShortcutMenuPackage.vsct* で、guidShortcutMenuPackageCmdSet という GuidSymbol 要素を探し、ショートカット メニュー、ショートカット メニュー グループ、およびメニュー オプションを宣言します。 GuidSymbol 要素のコードは、次のようになります。

    ```xml
    <GuidSymbol name="guidShortcutMenuPackageCmdSet" value="{00000000-0000-0000-0000-0000}"> // your GUID here
        <IDSymbol name="ShortcutMenuCommandId" value="0x0100" />
        <IDSymbol name="ColorMenu" value="0x1000"/>
        <IDSymbol name="ColorGroup" value="0x1100"/>
        <IDSymbol name="cmdidRed" value="0x102"/>
        <IDSymbol name="cmdidYellow" value="0x103"/>
        <IDSymbol name="cmdidBlue" value="0x104"/>
    </GuidSymbol>
    ```

2. Buttons 要素の直前に、Menus 要素を作成し、その中にショートカット メニューを定義します。

    ```vb
    <Menus>
      <Menu guid="guidShortcutMenuPackageCmdSet" id="ColorMenu" type="Context">
        <Strings>
          <ButtonText>Color change</ButtonText>
          <CommandName>ColorChange</CommandName>
        </Strings>
      </Menu>
    </Menus>
    ```

    ショートカット メニューは、メニューやツール バーの一部ではないため、親はありません。

3. Groups 要素と、ショートカット メニュー項目を含んだ Group 要素を作成し、グループをショートカット メニューに関連付けます。

    ```xml
    <Groups>
        <Group guid="guidShortcutMenuPackageCmdSet" id="ColorGroup">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorMenu"/>
        </Group>
    </Groups>
    ```

4. Buttons 要素で、ショートカット メニューに表示される個々のコマンドを定義します。 Buttons 要素は次のようになります。

    ```xml
    <Buttons>
        <Button guid="guidShortcutMenuPackageCmdSet" id="ShortcutMenuCommandId" priority="0x0100" type="Button">
            <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
            <Icon guid="guidImages" id="bmpPic1" />
            <Strings>
                <ButtonText>ShortcutMenu</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidRed" priority="1" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Red</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidYellow" priority="3" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Yellow</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidBlue" priority="5" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Blue</ButtonText>
            </Strings>
        </Button>
    </Buttons>
    ```

5. *ShortcutMenuCommand.cs* で、コマンド セット GUID、ショートカット メニュー、およびメニュー項目の定義を追加します。

    ```csharp
    public const string guidShortcutMenuPackageCmdSet = "00000000-0000-0000-0000-00000000"; // your GUID will differ
    public const int ColorMenu = 0x1000;
    public const int cmdidRed = 0x102;
    public const int cmdidYellow = 0x103;
    public const int cmdidBlue = 0x104;
    ```

    これらのコマンド ID は、*ShortcutMenuPackage.vsct* ファイルの Symbols セクションで定義されているものと同じです。 ここには、コンテキスト グループは含まれていません。コンテキスト グループは、 *.vsct* ファイルでのみ必要です。

## <a name="implementing-the-shortcut-menu"></a>ショートカット メニューの実装
 このセクションでは、ショートカット メニューとそのコマンドを実装します。

1. *ShortcutMenu.cs* では、ツール ウィンドウでメニュー コマンド サービスを取得できますが、それに含まれるコントロールは取得できません。 次の手順は、メニュー コマンド サービスをユーザー コントロールで使用できるようにする方法を示したものです。

2. *ShortcutMenu.cs* で、次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    ```

3. ツール ウィンドウの Initialize() メソッドをオーバーライドしてメニュー コマンド サービスを取得し、コントロールを追加して、メニュー コマンド サービスをコンストラクターに渡します。

    ```csharp
    protected override void Initialize()
    {
        var commandService = (OleMenuCommandService)GetService(typeof(IMenuCommandService));
        Content = new ShortcutMenuControl(commandService);
    }
    ```

4. ShortcutMenu ツール ウィンドウ コンストラクターで、コントロールを追加する行を削除します。 コンストラクターは次のようになります。

    ```csharp
    public ShortcutMenu() : base(null)
    {
        this.Caption = "ShortcutMenu";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
    }
    ```

5. *ShortcutMenuControl.xaml.cs* で、メニュー コマンド サービスのプライベート フィールドを追加し、メニュー コマンド サービスを取得するようにコントロールのコンストラクターを変更します。 次に、メニュー コマンド サービスを使用して、コンテキスト メニューのコマンドを追加します。 ShortcutMenuControl のコンストラクターは次のコードのようになります。 コマンド ハンドラーは、後で定義します。

    ```csharp
    public ShortcutMenuControl(OleMenuCommandService service)
    {
        this.InitializeComponent();
        commandService = service;

        if (null !=commandService)
        {
            // Create an alias for the command set guid.
            Guid guid = new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet);

            // Create the command IDs.
            var red = new CommandID(guid, ShortcutMenuCommand.cmdidRed);
            var yellow = new CommandID(guid, ShortcutMenuCommand.cmdidYellow);
            var blue = new CommandID(guid, ShortcutMenuCommand.cmdidBlue);

            // Add a command for each command ID.
            commandService.AddCommand(new MenuCommand(ChangeColor, red));
            commandService.AddCommand(new MenuCommand(ChangeColor, yellow));
            commandService.AddCommand(new MenuCommand(ChangeColor, blue));
        }
    }
    ```

6. *ShortcutMenuControl.xaml* で、最上位レベルの <xref:System.Windows.Controls.UserControl> 要素に <xref:System.Windows.UIElement.MouseRightButtonDown> イベントを追加します。 XAML ファイルは次のようになります。

    ```vb
    <UserControl x:Class="TWShortcutMenu.ShortcutMenuControl"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            Background="{DynamicResource VsBrush.Window}"
            Foreground="{DynamicResource VsBrush.WindowText}"
            mc:Ignorable="d"
            d:DesignHeight="300" d:DesignWidth="300"
            Name="MyToolWindow"
            MouseRightButtonDown="MyToolWindow_MouseRightButtonDown">
        <Grid>
            <StackPanel Orientation="Vertical">
                <TextBlock Margin="10" HorizontalAlignment="Center">ShortcutMenu</TextBlock>
            </StackPanel>
        </Grid>
    </UserControl>
    ```

7. *ShortcutMenuControl.xaml.cs* で、イベント ハンドラーのスタブを追加します。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
    . . .
    }
    ```

8. 同じファイルに、次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    using System;
    using System.Windows.Input;
    using System.Windows.Media;
    ```

9. 次のように、`MyToolWindowMouseRightButtonDown` イベントを実装します。

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
        if (null != commandService)
        {
            CommandID menuID = new CommandID(
                new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet),
                ShortcutMenuCommand.ColorMenu);
            Point p = this.PointToScreen(e.GetPosition(this));
            commandService.ShowContextMenu(menuID, (int)p.X, (int)p.Y);
        }
    }
    ```

    これにより、ショートカット メニューの <xref:System.ComponentModel.Design.CommandID> オブジェクトが作成され、マウス クリックの位置が識別されて、<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService.ShowContextMenu%2A> メソッドを使ってその場所でショートカット メニューが開くようになります。

10. コマンド ハンドラーを実装します。

    ```csharp
    private void ChangeColor(object sender, EventArgs e)
    {
        var mc = sender as MenuCommand;

        switch (mc.CommandID.ID)
        {
            case ShortcutMenuCommand.cmdidRed:
                MyToolWindow.Background = Brushes.Red;
                break;
            case ShortcutMenuCommand.cmdidYellow:
                MyToolWindow.Background = Brushes.Yellow;
                break;
            case ShortcutMenuCommand.cmdidBlue:
                MyToolWindow.Background = Brushes.Blue;
                break;
        }
    }
    ```

    この例の場合、<xref:System.ComponentModel.Design.CommandID> を識別し、背景色を適切に設定することで、すべてのメニュー項目のイベントが 1 つのメソッドによって処理されます。 メニュー項目に関連しないコマンドが含まれている場合は、コマンドごとに個別のイベント ハンドラーを作成していることになります。

## <a name="test-the-tool-window-features"></a>ツール ウィンドウの機能をテストする

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. 実験用インスタンスで、 **[表示]/[その他のウィンドウ]** をクリックし、 **[ShortcutMenu]** をクリックします。 これを行うと、ツール ウィンドウが表示されます。

3. ツール ウィンドウの本体を右クリックします。 色の一覧を含んだショートカット メニューが表示されます。

4. ショートカット メニューで色をクリックします。 ツール ウィンドウの背景色が、選択した色に変更されます。

## <a name="see-also"></a>こちらもご覧ください
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
