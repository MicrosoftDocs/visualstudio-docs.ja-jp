---
title: メニュー コントローラーのツールバーへの追加 | Microsoft Docs
description: メニュー コントローラーを作成して Visual Studio のツール ウィンドウのツールバーに追加し、メニュー コントローラー コマンドを実装してテストする方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding menu controllers
- menus, adding menu controllers to toolbars
- menu controllers, adding to toolbars
ms.assetid: 6af9b0b4-037f-404c-bb40-aaa1970768ea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 304f4ea11abc332c01603f96b6b67c0bd22e38c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060069"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>メニュー コントローラーのツールバーへの追加
このチュートリアルは、「[ツール ウィンドウにツールバーを追加する](../extensibility/adding-a-toolbar-to-a-tool-window.md)」チュートリアルに基づいており、ツール ウィンドウのツールバーにメニュー コントローラーを追加する方法を示しています。 ここに示す手順は、「[ツールバーの追加](../extensibility/adding-a-toolbar.md)」チュートリアルで作成したツールバーにも適用できます。

メニュー コントローラーは分割コントロールです。 メニュー コントローラーの左側には最後に使用したコマンドが表示され、それをクリックすると実行できます。 メニュー コントローラーの右側は矢印です。これをクリックすると、追加のコマンドの一覧が表示されます。 一覧でコマンドをクリックすると、コマンドが実行され、メニュー コントローラーの左側のコマンドが置き換えられます。 このようにして、メニュー コントローラーは、一覧から最後に使用したコマンドを常に表示するコマンド ボタンのように動作します。

メニュー コントローラーはメニューに表示できますが、最も頻繁に使用されるのはツールバーです。

## <a name="prerequisites"></a>必須コンポーネント
Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-menu-controller"></a>メニュー コントローラーを作成する

1. 「[ツール ウィンドウにツールバーを追加する](../extensibility/adding-a-toolbar-to-a-tool-window.md)」で説明されている手順に従って、ツールバーを持つツール ウィンドウを作成します。

2. *TWTestCommandPackage.vsct* で、Symbols セクションに移動します。 **guidTWTestCommandPackageCmdSet** という GuidSymbol 要素で、メニュー コントローラー、メニュー コントローラー グループ、3 つのメニュー項目を宣言します。

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. [メニュー] セクションで、最後のメニュー エントリの後にメニュー コントローラーをメニューとして定義します。

    ```xml
    <Menu guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" priority="0x0100" type="MenuController">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <CommandFlag>IconAndText</CommandFlag>
        <CommandFlag>TextChanges</CommandFlag>
        <CommandFlag>TextIsAnchorCommand</CommandFlag>
        <Strings>
            <ButtonText>Test Menu Controller</ButtonText>
            <CommandName>Test Menu Controller</CommandName>
        </Strings>
    </Menu>
    ```

    メニュー コントローラーに最後に選択したコマンドを反映できるようにするには、`TextChanges` と `TextIsAnchorCommand` フラグを含める必要があります。

4. [グループ] セクションで、最後のグループ エントリの後にメニュー コントローラー グループを追加します。

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    メニュー コントローラーを親として設定すると、このグループに配置されているすべてのコマンドがメニュー コントローラーに表示されます。 `priority` 属性が省略されています。メニュー コントローラー上の唯一のグループであるため、これにより既定値の 0 に設定されます。

5. [ボタン] セクションで、最後のボタン エントリの後に、各メニュー項目の Button 要素を追加します。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem1" priority="0x0000" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 1</ButtonText>
            <CommandName>MC Item 1</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem2" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 2</ButtonText>
            <CommandName>MC Item 2</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem3" priority="0x0200" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPicSearch" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 3</ButtonText>
            <CommandName>MC Item 3</CommandName>
        </Strings>
    </Button>
    ```

6. この時点で、メニュー コントローラーを見ることができます。 プロジェクトをビルドし、デバッグを開始します。 実験用のインスタンスが表示されるはずです。

   1. **[表示] メニューの [その他のウィンドウ]** で、 **[ToolWindow のテスト]** を開きます。

   2. ツール ウィンドウのツールバーにメニュー コントローラーが表示されます。

   3. メニュー コントローラーの右側にある矢印をクリックすると、使用可能な 3 つのコマンドが表示されます。

      コマンドをクリックすると、メニュー コントローラーのタイトルが変更され、そのコマンドが表示されることに注意してください。 次のセクションでは、これらのコマンドをアクティブにするコードを追加します。

## <a name="implement-the-menu-controller-commands"></a>メニュー コントローラーのコマンドを実装する

1. *TWTestCommandPackageGuids.cs* で、既存のコマンド ID の後に 3 つのメニュー項目のコマンド ID を追加します。

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. *TWTestCommand.cs* で、`TWTestCommand` クラスの先頭に次のコードを追加します。

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. TWTestCommand コンストラクターで、`AddCommand` メソッドの最後の呼び出しの後に、同じハンドラーを使用して各コマンドのイベントをルーティングするコードを追加します。

    ```csharp
    for (int i = TWTestCommandPackageGuids.cmdidMCItem1; i <=
        TWTestCommandPackageGuids.cmdidMCItem3; i++)
    {
        CommandID cmdID = new
        CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), i);
        OleMenuCommand mc = new OleMenuCommand(new
          EventHandler(OnMCItemClicked), cmdID);
        mc.BeforeQueryStatus += new EventHandler(OnMCItemQueryStatus);
        commandService.AddCommand(mc);
        // The first item is, by default, checked. 
        if (TWTestCommandPackageGuids.cmdidMCItem1 == i)
        {
            mc.Checked = true;
            this.currentMCCommand = i;
        }
    }
    ```

4. **TWTestCommand** クラスにイベント ハンドラーを追加して、選択したコマンドをチェック対象としてマークします。

    ```csharp
    private void OnMCItemQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            mc.Checked = (mc.CommandID.ID == this.currentMCCommand);
        }
    }
    ```

5. ユーザーがメニュー コントローラーでコマンドを選択したときにメッセージ ボックスを表示するイベント ハンドラーを追加します。

    ```csharp
    private void OnMCItemClicked(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            string selection;
            switch (mc.CommandID.ID)
            {
                case c.cmdidMCItem1:
                    selection = "Menu controller Item 1";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem2:
                    selection = "Menu controller Item 2";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem3:
                    selection = "Menu controller Item 3";
                    break;

                default:
                    selection = "Unknown command";
                    break;
            }
            this.currentMCCommand = mc.CommandID.ID;

            IVsUIShell uiShell =
              (IVsUIShell) ServiceProvider.GetService(typeof(SVsUIShell));
            Guid clsid = Guid.Empty;
            int result;
            uiShell.ShowMessageBox(
                    0,
                    ref clsid,
                    "Test Tool Window Toolbar Package",
                    string.Format(CultureInfo.CurrentCulture,
                                 "You selected {0}", selection),
                    string.Empty,
                    0,
                    OLEMSGBUTTON.OLEMSGBUTTON_OK,
                    OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
                    OLEMSGICON.OLEMSGICON_INFO,
                    0,
                    out result);
        }
    }
    ```

## <a name="testing-the-menu-controller"></a>メニュー コントローラーのテスト

1. プロジェクトをビルドし、デバッグを開始します。 実験用のインスタンスが表示されるはずです。

2. **[表示] メニューの [その他のウィンドウ]** で、 **[ToolWindow のテスト]** を開きます。

    ツール ウィンドウのツールバーにメニュー コントローラーが表示され、 **[MC 項目 1]** が表示されます。

3. 矢印の左側にあるメニュー コントローラーのボタンをクリックします。

    3 つの項目が表示されます。最初の項目が選択されており、そのアイコンは強調表示ボックスで囲まれています。 **[MC 項目 3]** をクリックします。

    ダイアログ ボックスが開き、「**メニュー コントローラー項目 3 を選択しました**」というメッセージが表示されます。 メッセージがメニュー コントローラー ボタンのテキストに対応することに注意してください。 メニュー コントローラー ボタンに **[MC 項目 3]** が表示されるようになりました。

## <a name="see-also"></a>関連項目
- [ツール ウィンドウへのツールバーの追加](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [ツール バーの追加](../extensibility/adding-a-toolbar.md)
