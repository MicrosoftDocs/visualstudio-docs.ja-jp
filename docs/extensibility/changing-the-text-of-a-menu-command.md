---
title: メニュー コマンドのテキストの変更 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6ba19a6536be7f0f5855ee9035e80989c105cbf7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321110"
---
# <a name="change-the-text-of-a-menu-command"></a>メニュー コマンドのテキストを変更します。
次の手順を使用してメニュー コマンドのテキスト ラベルを変更する方法を示して、<xref:System.ComponentModel.Design.IMenuCommandService>サービス。

## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>IMenuCommandService でメニュー コマンドのラベルを変更します。

1. という名前の VSIX プロジェクトを作成する`MenuText`メニュー コマンドを使用して名前付き**ChangeMenuText**します。 詳細については、次を参照してください。[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)します。

2. *.Vsct*ファイルを追加、`TextChanges`の次の例に示すように、メニュー コマンドにフラグを設定します。

    ```xml
    <Button guid="guidChangeMenuTextPackageCmdSet" id="ChangeMenuTextId" priority="0x0100" type="Button">
        <Parent guid="guidChangeMenuTextPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>TextChanges</CommandFlag>
        <Strings>
            <ButtonText>Invoke ChangeMenuText</ButtonText>
        </Strings>
    </Button>
    ```

3. *ChangeMenuText.cs*ファイルで、メニュー コマンドが表示される前に呼び出されるイベント ハンドラーを作成します。

    ```csharp
    private void OnBeforeQueryStatus(object sender, EventArgs e)
    {
        var myCommand = sender as OleMenuCommand;
        if (null != myCommand)
        {
            myCommand.Text = "New Text";
        }
    }
    ```

    変更することで、このメソッドでメニュー コマンドの状態を更新することも、 <xref:System.ComponentModel.Design.MenuCommand.Visible%2A>、 <xref:System.ComponentModel.Design.MenuCommand.Checked%2A>、および<xref:System.ComponentModel.Design.MenuCommand.Enabled%2A>プロパティを<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>オブジェクト。

4. ChangeMenuText コンス トラクターで作成するコードを元のコマンドの初期化と配置のコードを置き換えますを<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>(なく`MenuCommand`) メニュー コマンドを表す、追加、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>イベント ハンドラーでは、メニューと。メニュー コマンド サービスにコマンド。

    次のようになりますに示します。

    ```csharp
    private ChangeMenuText(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException(nameof(package));
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);
            EventHandler eventHandler = this.ShowMessageBox;
            OleMenuCommand menuItem = new OleMenuCommand(ShowMessageBox, menuCommandID);
            menuItem.BeforeQueryStatus +=
                new EventHandler(OnBeforeQueryStatus);
            commandService.AddCommand(menuItem);
        }
    }
    ```

5. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

6. **ツール**メニューという名前のコマンドを表示する必要があります**呼び出す ChangeMenuText**します。

7. コマンドをクリックします。 お知らせをメッセージ ボックスが表示されます**MenuItemCallback**が呼び出されました。 メッセージ ボックスを消去するときに、[ツール] メニュー コマンドの名前を参照する必要があります**新しいテキスト**します。
