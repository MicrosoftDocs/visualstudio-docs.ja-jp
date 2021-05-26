---
title: 最近使用した一覧のサブメニューへの追加 | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) のサブメニューに、最近使用したメニュー コマンドを含む動的リストを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bb238afb0f583f1b913fbd87f4f50e43679ebd7d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060017"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>最近使用した一覧のサブメニューへの追加
このチュートリアルは、「[メニューにサブメニューを追加する](../extensibility/adding-a-submenu-to-a-menu.md)」のデモを基にしており、サブメニューに動的リストを追加する方法を示しています。 動的リストは、最近使用した (MRU) リストを作成するための基礎となります。

動的メニュー リストは、メニューのプレースホルダーから始まります。 メニューが表示されるたびに、Visual Studio 統合開発環境 (IDE) によって、プレースホルダーに表示されるすべてのコマンドが VSPackage に要求されます。 動的リストは、メニュー上の任意の場所で実行できます。 ただし、動的リストは通常、サブメニューやメニューの下部に格納されてそれだけで表示されます。 これらの設計パターンを使用すると、メニュー上の他のコマンドの位置に影響を与えずに、コマンドの動的リストを拡張およびコントラクトすることができます。 このチュートリアルでは、既存のサブメニューの一番下に動的 MRU リストが表示されます。これは、サブメニューの残りの部分から、線によって区切られています。

技術的には、動的リストをツールバーに適用することもできます。 ただし、ユーザーが特定の手順を実行して変更しない限りは、ツールバーは変更されないようにするべきなので、その使用方法はお勧めしません。

このチュートリアルでは、4 つの項目のいずれかが選択されるたびに順序が変更される MRU リストを作成します (選択した項目が一覧の一番上に移動します)。

メニューおよび *.vsct* ファイルの詳細については、「[コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension"></a>拡張機能を作成する

- 「[メニューにサブメニューを追加する](../extensibility/adding-a-submenu-to-a-menu.md)」の手順に従って、次の手順で変更されるサブメニューを作成します。

  このチュートリアルの手順では、VSPackage の名前が `TestCommand` であることを前提としています。これは、「[Visual Studio のメニューバーにメニューを追加する](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)」で使用される名前です。

## <a name="create-a-dynamic-item-list-command"></a>動的項目リスト コマンドの作成

1. *TestCommandPackage.vsct* を開きます。

2. `Symbols` セクションの、guidTestCommandPackageCmdSet という名前の `GuidSymbol` ノードで `MRUListGroup` グループと `cmdidMRUList` コマンドのシンボルを次のように追加します。

    ```xml
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. `Groups` セクションで、宣言されたグループを既存のグループ エントリの後に追加します。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

4. `Buttons` セクションで、新しく宣言されたコマンドを表すノードを既存のボタン エントリの後に追加します。

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidMRUList"
        type="Button" priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="MRUListGroup" />
        <CommandFlag>DynamicItemStart</CommandFlag>
        <Strings>
            <CommandName>cmdidMRUList</CommandName>
            <ButtonText>MRU Placeholder</ButtonText>
        </Strings>
    </Button>
    ```

    `DynamicItemStart` フラグを使用すると、コマンドを動的に生成できます。

5. プロジェクトをビルドし、デバッグを開始して、新しいコマンドの表示をテストします。

    **[TestMenu]** メニューの新しいサブメニュー **[SubMenu]** をクリックして、新しいコマンド **MRU Placeholder** を表示します。 次の手順で動的 MRU のコマンド リストが実装されたら、サブメニューが開かれるたびに、このコマンド ラベルがそのリストに置き換えられます。

## <a name="filling-the-mru-list"></a>MRU リストの入力

1. *TestCommandPackageGuids.cs* で、`TestCommandPackageGuids` クラス定義の既存のコマンド ID の後に次の行を追加します。

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. *TestCommand.cs* に、次の using ステートメントを追加します。

    ```csharp
    using System.Collections;
    ```

3. 最後の AddCommand 呼び出しの後に、TestCommand コンストラクターに次のコードを追加します。 `InitMRUMenu` は後で定義されます

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. TestCommand クラスに次のコードを追加します。 このコードにより、MRU リストに表示される項目を表す文字列のリストが初期化されます。

    ```csharp
    private int numMRUItems = 4;
    private int baseMRUID = (int)TestCommandPackageGuids.cmdidMRUList;
    private ArrayList mruList;

    private void InitializeMRUList()
    {
        if (null == this.mruList)
        {
            this.mruList = new ArrayList();
            if (null != this.mruList)
            {
                for (int i = 0; i < this.numMRUItems; i++)
                {
                    this.mruList.Add(string.Format(CultureInfo.CurrentCulture,
                        "Item {0}", i + 1));
                }
            }
        }
    }
    ```

5. `InitializeMRUList` メソッドの後に、`InitMRUMenu` メソッドを追加します。 これにより、MRU リスト メニュー コマンドが初期化されます。

    ```csharp
    private void InitMRUMenu(OleMenuCommandService mcs)
    {
        InitializeMRUList();
        for (int i = 0; i < this.numMRUItems; i++)
        {
            var cmdID = new CommandID(
                new Guid(TestCommandPackageGuids.guidTestCommandPackageCmdSet), this.baseMRUID + i);
            var mc = new OleMenuCommand(
                new EventHandler(OnMRUExec), cmdID);
            mc.BeforeQueryStatus += new EventHandler(OnMRUQueryStatus);
            mcs.AddCommand(mc);
        }
    }
    ```

    MRU リストに表示されるすべての項目に対して、メニュー コマンド オブジェクトを作成する必要があります。 IDE により、項目がなくなるまで、MRU リストの各項目に対して `OnMRUQueryStatus` メソッドが呼び出されます。 マネージド コードでは、これ以上項目がないことが IDE により確認される唯一の方法は、可能なすべての項目を最初に作成することです。 必要に応じて、メニュー コマンドが作成された後で `mc.Visible = false;` を使用して、追加の項目を当初非表示にすることができます。 これらの項目は、後で `OnMRUQueryStatus` メソッドで `mc.Visible = true;` を使用して表示できます。

6. `InitMRUMenu` メソッドの後に次の `OnMRUQueryStatus` メソッドを追加します。 これは、各 MRU 項目のテキストを設定するハンドラーです。

    ```csharp
    private void OnMRUQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                menuCommand.Text = this.mruList[MRUItemIndex] as string;
            }
        }
    }
    ```

7. `OnMRUQueryStatus` メソッドの後に次の `OnMRUExec` メソッドを追加します。 これは、MRU 項目を選択するためのハンドラーです。 このメソッドは、選択した項目をリストの一番上に移動し、選択した項目をメッセージ ボックスに表示します。

    ```csharp
    private void OnMRUExec(object sender, EventArgs e)
    {
        var menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                string selection = this.mruList[MRUItemIndex] as string;
                for (int i = MRUItemIndex; i > 0; i--)
                {
                    this.mruList[i] = this.mruList[i - 1];
                }
                this.mruList[0] = selection;
                System.Windows.Forms.MessageBox.Show(
                    string.Format(CultureInfo.CurrentCulture,
                                  "Selected {0}", selection));
            }
        }
    }
    ```

## <a name="testing-the-mru-list"></a>MRU リストのテスト

1. プロジェクトをビルドし、デバッグを開始します。

2. **[テスト メニュー]** メニューの **[TestCommand の呼び出し]** をクリックします。 この操作を実行すると、コマンドが選択されたことを示すメッセージ ボックスが表示されます。

    > [!NOTE]
    > この手順は、VSPackage に MRU リストを読み込んで正しく表示するために必要です。 この手順を省略した場合、MRU リストは表示されません。

3. **[テスト メニュー]** メニューの **[サブメニュー]** をクリックします。 サブメニューの末尾、区切りの下に 4 つの項目の一覧が表示されます。 **[項目 3]** をクリックすると、メッセージ ボックスが表示され、「**項目 3 を選択**」というテキストが表示されます。 (4 つの項目の一覧が表示されない場合は、前の手順の指示に従っていることを確認してください)。

4. もう一度サブメニューを開きます。 **[項目 3]** がリストの一番上にあり、他の項目が 1 つ下に移動されていることを確認します。 もう一度 **[項目 3]** をクリックすると、メッセージ ボックスにはまだ「**項目 3 を選択**」が表示されます。これは、テキストがコマンド ラベルと共に新しい位置に正しく移動したことを示しています。

## <a name="see-also"></a>関連項目
- [メニュー項目の動的な追加](../extensibility/dynamically-adding-menu-items.md)
