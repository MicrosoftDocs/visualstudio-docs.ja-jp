---
title: ツール ウィンドウにツール バーを追加する | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) で、コマンドにバインドされているボタンを含むツール バーをツール ウィンドウに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1847801ed9dcbb1b7c7145c86b1998b54e2bb5d9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055792"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>ツール ウィンドウにツール バーを追加する
このチュートリアルでは、ツール ウィンドウにツール バーを追加する方法について説明します。

 ツール バーとは、コマンドにバインドされたボタンを含む、水平または垂直のストリップです。 ツール ウィンドウのツール バーの長さは、ツール バーがドッキングされている場所に応じて、ツール ウィンドウの幅または高さと常に同じになります。

 IDE のツール バーとは異なり、ツール ウィンドウのツール バーはドッキングされている必要があり、移動することもカスタマイズすることもできません。 VSPackage が アンマネージド コードで記述されている場合は、このツール バーをどの端にもドッキングできます。

 ツール バーを追加する方法の詳細については、「[ツール バーの追加](../extensibility/adding-a-toolbar.md)」をご覧ください。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-toolbar-for-a-tool-window"></a>ツール ウィンドウのツール バーを作成する

1. **TWTestCommand** という名前のメニュー コマンドと **TestToolWindow** という名前のツール ウィンドウの両方を含む、`TWToolbar` という名前の VSIX プロジェクトを作成します。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」および「[ツール ウィンドウで拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)」をご覧ください。 ツール ウィンドウ テンプレートを追加する前に、コマンド項目テンプレートを追加する必要があります。

2. *TWTestCommandPackage.vsct* で、Symbols セクションを探します。 guidTWTestCommandPackageCmdSet という名前の GuidSymbol ノードで、次のようにツール バーとツール バー グループを宣言します。

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. `Commands` セクションの最上部に、`Menus` セクションを作成します。 `Menu` 要素を追加して、ツール バーを定義します。

    ```xml
    <Menus>
        <Menu guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" type="ToolWindowToolbar">
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

     ツール バーは、サブメニューのように入れ子にすることはできません。 したがって、親を割り当てる必要はありません。 また、ユーザーはツール バーを移動できるため、優先度を設定する必要もありません。 通常、ツール バーの最初の配置はプログラムによって定義されますが、ユーザーによるその後の変更は保持されます。

4. Groups セクションで、ツール バーのコマンドを格納するグループを定義します。

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. Buttons セクションで、既存の Button 要素の親をそのツール バー グループに変更して、ツール バーが表示されるようにします。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     既定では、ツール バーにコマンドがない場合、ツール バーは表示されません。

     ツール ウィンドウに新しいツール バーが自動的に追加されることはないため、ツール バーは明示的に追加する必要があります。 これについては、次のセクションで説明します。

## <a name="add-the-toolbar-to-the-tool-window"></a>ツール ウィンドウにツール バーを追加する

1. *TWTestCommandPackageGuids.cs* に、次の行を追加します。

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. *TestToolWindow.cs* に、次の using ステートメントを追加します。

    ```csharp
    using System.ComponentModel.Design;
    ```

3. TestToolWindow コンストラクターに、次の行を追加します。

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>ツール ウィンドウのツールバーをテストする

1. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

2. **[表示] メニューの [その他のウィンドウ]** で、 **[ToolWindow のテスト]** をクリックしてツール ウィンドウを表示します。

     ツール ウィンドウの左上の、タイトルのすぐ下にツール バー (既定のアイコンのように見える) が表示されます。

3. ツール バーで、そのアイコンをクリックすると、**TWTestCommandPackage Inside TWToolbar.TWTestCommand.MenuItemCallback()** というメッセージが表示されます。

## <a name="see-also"></a>関連項目
- [ツールバーの追加](../extensibility/adding-a-toolbar.md)
