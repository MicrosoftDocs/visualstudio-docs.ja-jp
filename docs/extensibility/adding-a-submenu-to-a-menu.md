---
title: メニューへのサブメニューの追加 |Microsoft Docs
description: サブメニューを作成し、Visual Studio のメニュー バーに追加して、サブメニューに新しいコマンドを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- context menus
- submenus, cascading
- cascading submenus
- menus, creating cascading submenus
ms.assetid: 692600cb-d052-40e2-bdae-4354ae7c6c84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cc6d521e699beb2345ba76e2e617ff749886eee9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094901"
---
# <a name="add-a-submenu-to-a-menu"></a>メニューにサブメニューを追加する
このチュートリアルでは、 **[TestMenu]** メニューにサブメニューを追加する方法を示して、「[メニューを Visual Studio のメニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)」でのデモに基づいています。

 サブメニューは、別のメニューに表示されるセカンダリ メニューです。 名前の後に矢印が続いていれば、サブメニューと識別できます。 名前をクリックすると、サブメニューとそのコマンドが表示されます。

 このチュートリアルでは、Visual Studio のメニュー バーのメニューにサブメニューを作成し、サブメニューに新しいコマンドを配置します。 チュートリアルでは新しいコマンドも実装します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="add-a-submenu-to-a-menu"></a>メニューにサブメニューを追加する

1. 「[メニューを Visual Studio のメニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)」の手順に従って、プロジェクトとメニュー項目を作成します。 このチュートリアルの手順では、VSIX プロジェクトの名前が `TopLevelMenu` であることを想定しています。

2. *TestCommandPackage.vsct* を開きます。 `<Symbols>` セクションでは、サブメニュー、サブメニュー グループ、コマンドの `<IDSymbol>` 要素をすべて、"guidTopLevelMenuCmdSet" という名前の `<GuidSymbol>` ノードに追加します。 これは、トップレベル メニューの `<IDSymbol>` 要素を含むノードと同じです。

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3. 新しく作成したサブメニューを `<Menus>` セクションに追加します。

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     親の GUID/ID ペアはトップレベル メニューの子であり、「[メニューを Visual Studio のメニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)」で生成されたメニュー グループが指定されます。

4. 手順 2 で定義されたメニュー グループを、`<Groups>` セクションに追加し、サブメニューの子にします。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5. 新しい `<Button>` 要素を `<Buttons>` セクションに追加して、手順 2 で作成したコマンドをサブメニューでの項目として定義します。

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidTestSubCommand" priority="0x0000" type="Button">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <Strings>
           <CommandName>cmdidTestSubCommand</CommandName>
           <ButtonText>Test Sub Command</ButtonText>
        </Strings>
    </Button>
    ```

6. ソリューションをビルドし、デバッグを開始します。 実験用のインスタンスが表示されるはずです。

7. **[TestMenu]** をクリックして、 **[Sub Menu]** という名前の新しいサブメニューを表示します。 **[Sub Menu]** をクリックして、サブメニューを開き、新しいコマンド **[Test Sub Command]** を表示します。 **[Test Sub Command]** をクリックしても何も起こらないことに注意してしてください。

## <a name="add-a-command"></a>コマンドを追加する

1. *TestCommand.cs* を開き、既存のコマンド ID の後に、次のコマンド ID を追加します。

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2. サブコマンドを追加します。 コマンド コンストラクターを検索します。 `AddCommand` メソッドへの呼び出しのすぐ後に、次のコードを追加します。

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    `SubItemCallback` コマンド ハンドラーは後から定義されます。 コンストラクターは次のようになります。

    ```csharp
    private TestCommand(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            var menuCommandID = new CommandID(CommandSet, CommandId);
            var menuItem = new MenuCommand(this.MenuItemCallback, menuCommandID);
            commandService.AddCommand(menuItem);

            CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
            MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
            commandService.AddCommand(subItem);
        }
    }
    ```

3. `SubItemCallback()`を追加します。 これは、サブメニューの新しいコマンドがクリックされたときに呼び出されるメソッドです。

    ```csharp
    private void SubItemCallback(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();
        IVsUIShell uiShell = this.package.GetService<SVsUIShell, IVsUIShell>();
        Guid clsid = Guid.Empty;
        int result;
        uiShell.ShowMessageBox(
            0,
            ref clsid,
            "TestCommand",
            string.Format(CultureInfo.CurrentCulture,
            "Inside TestCommand.SubItemCallback()",
            this.ToString()),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result);
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. **[TestMenu]** メニューで、 **[Sub Menu]** をクリックし、 **[Test Sub Command]** をクリックします。 メッセージ ボックスが表示され、"Test Command Inside TestCommand.SubItemCallback()" というテキストが示されます。

## <a name="see-also"></a>関連項目

- [メニューを Visual Studio のメニュー バーに追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
