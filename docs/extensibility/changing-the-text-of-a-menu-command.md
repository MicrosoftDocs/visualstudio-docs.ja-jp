---
title: メニュー コマンドのテキストの変更 | Microsoft Docs
description: このコード例を確認することにより、IMenuCommandService サービスを使用してメニュー コマンドのテキスト ラベルを変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 541acf1bcf448541fe6c440eb2aada687cfbe0e9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904992"
---
# <a name="change-the-text-of-a-menu-command"></a>メニュー コマンドのテキストを変更する
次の手順は、<xref:System.ComponentModel.Design.IMenuCommandService> サービスを使用してメニュー コマンドのテキスト ラベルを変更する方法を示しています。

## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>IMenuCommandService を使用したメニュー コマンドのラベルの変更

1. **ChangeMenuText** という名前のメニュー コマンドを使用して、`MenuText` という名前の VSIX プロジェクトを作成します。 詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. *.vsct* ファイルで、次の例に示すように、メニュー コマンドに `TextChanges` フラグを追加します。

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

3. *ChangeMenuText.cs* ファイルで、メニュー コマンドが表示される前に呼び出されるイベント ハンドラーを作成します。

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

    また、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand> オブジェクトの <xref:System.ComponentModel.Design.MenuCommand.Visible%2A>、<xref:System.ComponentModel.Design.MenuCommand.Checked%2A>、<xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> の各プロパティを変更することによって、この方法でメニュー コマンドの状態を更新することもできます。

4. ChangeMenuText コンストラクターで、コマンドの初期化と配置を行う元のコードを、メニュー コマンドを表す (`MenuCommand` ではなく) <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> を作成し、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> イベント ハンドラーを追加し、このメニュー コマンドをメニュー コマンド サービスに提供するコードに置き換えます。

    そのコードは次のようになります。

    ```csharp
    private ChangeMenuText(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));
        
        var menuCommandID = new CommandID(CommandSet, CommandId);
        var menuItem = new OleMenuCommand(this.Excute, menuCommandID);
        menuItem.BeforeQueryStatus += new EventHandler(OnBeforeQueryStatus);
        commandService.AddCommand(menuItem);
    }
    ```

5. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

6. **[ツール]** メニューに **Invoke ChangeMenuText** という名前のコマンドが表示されます。

7. このコマンド クリックします。 **MenuItemCallback** が呼び出されたことを通知するメッセージ ボックスが表示されます。 このメッセージ ボックスを閉じると、[ツール] メニューにあるコマンドの名前が **New Text** になっていることがわかります。
