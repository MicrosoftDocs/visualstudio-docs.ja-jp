---
title: メニュー項目を動的に追加する | Microsoft Docs
description: DynamicItemStart コマンド フラグを使用して実行時にメニュー項目を追加する方法について説明します。 この記事では、Visual Studio ソリューションでスタートアップ プロジェクトを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa85d5b5cf4b99840e181fb24b5913ff72a3fee0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070337"
---
# <a name="dynamically-add-menu-items"></a>メニュー項目を動的に追加する
実行時にメニュー項目を追加するには、Visual Studio コマンドテーブル ( *.vsct*) ファイルのプレースホルダー ボタン定義に `DynamicItemStart` コマンド フラグを指定し、コマンドを表示および処理するメニュー項目数を (コードで) 定義します。 VSPackage が読み込まれると、プレースホルダーは動的メニュー項目に置き換えられます。

 Visual Studio には、最近開いたドキュメント名が表示される **[直前に使用]** (MRU) リストと、現在開かれているウィンドウ名が表示される **[ウィンドウ]** リストの動的リストが使用されます。   コマンド定義の `DynamicItemStart` フラグには、VSPackage が開かれるまではコマンドがプレースホルダーであることが指定されています。 VSPackage を開くと、プレースホルダーは、実行時に作成されて動的リストに追加される 0 個以上のコマンドに置き換えられます。 VSPackage が開かれるまで、動的リストが表示されるメニュー上の位置を確認できない場合があります。  動的リストを設定するために、Visual Studio から VSPackage に対して、ID の最初の文字がプレースホルダーの ID と同じコマンドを探すように要求されます。 Visual Studio によって一致するコマンドを見つけられると、コマンドの名前が動的リストに追加されます。 次に、ID がインクリメントされ、動的コマンドがなくなるまで、動的リストに追加する別の一致するコマンドが検索されます。

 このチュートリアルでは、**ソリューション エクスプローラー** ツール バーのコマンドを使用して、Visual Studio ソリューションでスタートアップ プロジェクトを設定する方法について説明します。 これには、アクティブなソリューションにプロジェクトの動的ドロップダウン リストを持つメニュー コントローラーが使用されます。 開いているソリューションがない場合、または開いているソリューションにプロジェクトが 1 つしかない場合に、このコマンドが表示されないようにするために、ソリューションに複数のプロジェクトがある場合にのみ VSPackage が読み込まれます。

 *.vsct* ファイルの詳細については、「[Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用して拡張機能を作成する

1. `DynamicMenuItems` という名前の VSIX プロジェクトを作成します。

2. プロジェクトが開いたら、カスタム コマンド項目テンプレートを追加して、**DynamicMenu** という名前を付けます。 詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

## <a name="setting-up-the-elements-in-the-vsct-file"></a>*.vsct* ファイル内の要素の設定
 ツール バーに動的メニュー項目を含むメニュー コントローラーを作成するには、次の要素を指定します。

- メニュー コントローラーを含むコマンド グループと、ドロップダウンのメニュー項目を含むコマンド グループという 2 つのコマンド グループ

- 種類が `MenuController` の 1 つのメニュー要素

- 1 つはメニュー項目のプレースホルダーとして、もう 1 つはツール バーのアイコンとツールヒントとして機能する 2 つのボタン。

1. *DynamicMenuPackage.vsct* で、コマンド ID を定義します。 Symbols セクションに移動し、**guidDynamicMenuPackageCmdSet** GuidSymbol ブロックの IDSymbol 要素を置き換えます。 2 つのグループの IDSymbol 要素 (メニュー コントローラー、プレースホルダー コマンド、およびアンカー コマンド) を定義する必要があります。

    ```xml
    <GuidSymbol name="guidDynamicMenuPackageCmdSet" value="{ your GUID here }">
        <IDSymbol name="MyToolbarItemGroup" value="0x1020" />
        <IDSymbol name="MyMenuControllerGroup" value="0x1025" />
        <IDSymbol name="MyMenuController" value ="0x1030"/>
        <IDSymbol name="cmdidMyAnchorCommand" value="0x0103" />
        <!-- NOTE: The following command expands at run time to some number of ids.
         Try not to place command ids after it (e.g. 0x0105, 0x0106).
         If you must add a command id after it, make the gap very large (e.g. 0x200) -->
        <IDSymbol name="cmdidMyDynamicStartCommand" value="0x0104" />
    </GuidSymbol>
    ```

2. Groups セクションで、既存のグループを削除し、定義した 2 つのグループを追加します。

    ```xml
    <Groups>
        <!-- The group that adds the MenuController on the Solution Explorer toolbar.
             The 0x4000 priority adds this group after the group that contains the
             Preview Selected Items button, which is normally at the far right of the toolbar. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" priority="0x4000" >
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN" />
        </Group>
        <!-- The group for the items on the MenuController drop-down. It is added to the MenuController submenu. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" priority="0x4000" >
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" />
        </Group>
    </Groups>
    ```

     MenuController を追加します。 常に表示されるとは限らないため、DynamicVisibility コマンド フラグを設定します。 ButtonText は表示されません。

    ```xml
    <Menus>
        <!-- The MenuController to display on the Solution Explorer toolbar.
             Place it in the ToolbarItemGroup.-->
        <Menu guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" priority="0x1000" type="MenuController">
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" />
            <CommandFlag>DynamicVisibility</CommandFlag>
            <Strings>
               <ButtonText></ButtonText>
           </Strings>
        </Menu>
    </Menus>
    ```

3. 2 つのボタン (1 つは動的メニュー項目のプレースホルダー、もう 1 つは MenuController のアンカー) を追加します。

     プレースホルダー ボタンの親は、**MyMenuControllerGroup** です。 DynamicItemStart、DynamicVisibility、TextChanges のコマンド フラグをプレースホルダー ボタンに追加します。 ButtonText は表示されません。

     アンカー ボタンには、アイコンとツールヒント テキストが保持されます。 アンカー ボタンの親は、**MyMenuControllerGroup** でもあります。 NoShowOnMenuController コマンド フラグを追加して、ボタンがメニュー コントローラーのドロップダウンに実際に表示されないようにし、FixMenuController コマンド フラグを追加して、ボタンを永続的なアンカーにします。

    ```xml
    <!-- The placeholder for the dynamic items that expand to N items at run time. -->
    <Buttons>
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyDynamicStartCommand" priority="0x1000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <CommandFlag>DynamicItemStart</CommandFlag>
          <CommandFlag>DynamicVisibility</CommandFlag>
          <CommandFlag>TextChanges</CommandFlag>
          <!-- This text does not appear. -->
          <Strings>
            <ButtonText>Project</ButtonText>
          </Strings>
        </Button>

        <!-- The anchor item to supply the icon/tooltip for the MenuController -->
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyAnchorCommand" priority="0x0000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <!-- This is the icon that appears on the Solution Explorer toolbar. -->
          <Icon guid="guidImages" id="bmpPicArrows"/>
          <!-- Do not show on the menu controller's drop down list-->
          <CommandFlag>NoShowOnMenuController</CommandFlag>
          <!-- Become the permanent anchor item for the menu controller -->
          <CommandFlag>FixMenuController</CommandFlag>
          <!-- The text that appears in the tooltip.-->
          <Strings>
            <ButtonText>Set Startup Project</ButtonText>
          </Strings>
        </Button>
    </Buttons>
    ```

4. (*Resources* フォルダー内の) プロジェクトにアイコンを追加し、そのアイコンへの参照を *.vsct* ファイルに追加します。 このチュートリアルでは、プロジェクト テンプレートに含まれている矢印アイコンを使用します。

5. Symbols セクションの直前にある Commands セクションの外側に VisibilityConstraints セクションを追加します (Symbols の後に追加すると、警告が表示される場合があります)。このセクションを使用して、複数のプロジェクトを含むソリューションが読み込まれたときにのみメニュー コントローラーが表示されるようにします。

    ```xml
    <VisibilityConstraints>
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>
    </VisibilityConstraints>
    ```

## <a name="implement-the-dynamic-menu-command"></a>動的メニュー コマンドを実装する
 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> から継承する動的メニュー コマンド クラスを作成します。 この実装では、コンストラクターに、コマンドの照合に使用される述語を指定します。 この述部を使用して、呼び出されるコマンドを識別する <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> プロパティを設定するには、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> メソッドをオーバーライドする必要があります。

1. *DynamicItemMenuCommand.cs* という名前の新しい C# クラス ファイルを作成し、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand> から継承する **DynamicItemMenuCommand** という名前のクラスを追加します。

    ```csharp
    class DynamicItemMenuCommand : OleMenuCommand
    {

    }

    ```

2. ディレクティブを使用して以下を追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    using System.ComponentModel.Design;
    ```

3. match 述語を格納するプライベート フィールドを追加します。

    ```csharp
    private Predicate<int> matches;

    ```

4. <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> コンストラクターから継承し、コマンド ハンドラーと <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> ハンドラーを指定するコンストラクターを追加します。 コマンドを照合するための述語を追加します。

    ```csharp
    public DynamicItemMenuCommand(CommandID rootId, Predicate<int> matches, EventHandler invokeHandler, EventHandler beforeQueryStatusHandler)
        : base(invokeHandler, null /*changeHandler*/, beforeQueryStatusHandler, rootId)
    {
        if (matches == null)
        {
            throw new ArgumentNullException("matches");
        }

        this.matches = matches;
    }
    ```

5. matches 述語を呼び出し、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> プロパティを設定するように <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> メソッドをオーバーライドします。

    ```csharp
    public override bool DynamicItemMatch(int cmdId)
    {
        // Call the supplied predicate to test whether the given cmdId is a match.
        // If it is, store the command id in MatchedCommandid
        // for use by any BeforeQueryStatus handlers, and then return that it is a match.
        // Otherwise clear any previously stored matched cmdId and return that it is not a match.
        if (this.matches(cmdId))
        {
            this.MatchedCommandId = cmdId;
            return true;
        }

        this.MatchedCommandId = 0;
        return false;
    }
    ```

## <a name="add-the-command"></a>コマンドを追加する
 DynamicMenu コンストラクターは、動的メニューやメニュー項目などのメニュー コマンドを設定する場所です。

1. *DynamicMenuPackage.cs* に、コマンド セットの GUID とコマンド ID を追加します。

    ```csharp
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    public const uint cmdidMyCommand = 0x104;
    ```

2. *DynamicMenu.cs* ファイルで、次の using ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using System.ComponentModel.Design;
    ```

3. `DynamicMenu` クラスに、プライベート フィールド **dte2** を追加します。

    ```csharp
    private DTE2 dte2;
    ```

4. プライベート rootItemId フィールドを追加します。

    ```csharp
    private int rootItemId = 0;
    ```

5. DynamicMenu コンストラクターに、menu コマンドを追加します。 次のセクションに、コマンド ハンドラー、`BeforeQueryStatus` イベント ハンドラー、match 述語を定義します。

    ```csharp
    private DynamicMenu(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException(nameof(package));
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            // Add the DynamicItemMenuCommand for the expansion of the root item into N items at run time.
            CommandID dynamicItemRootId = new CommandID(new Guid(DynamicMenuPackageGuids.guidDynamicMenuPackageCmdSet), (int)DynamicMenuPackageGuids.cmdidMyCommand);
            DynamicItemMenuCommand dynamicMenuCommand = new DynamicItemMenuCommand(dynamicItemRootId,
                IsValidDynamicItem,
                OnInvokedDynamicItem,
                OnBeforeQueryStatusDynamicItem);
                commandService.AddCommand(dynamicMenuCommand);
                }

        dte2 = (DTE2)this.ServiceProvider.GetService(typeof(DTE));
    }
    ```

## <a name="implement-the-handlers"></a>ハンドラーを実装する
 メニュー コントローラーに動的メニュー項目を実装するには、動的項目がクリックされたときにコマンドを処理する必要があります。 メニュー項目の状態を設定するロジックも実装する必要があります。 ハンドラーを `DynamicMenu` クラスに追加します。

1. **Set Startup Project** コマンドを実装するには、**OnInvokedDynamicItem** イベント ハンドラーを追加します。 これにより、呼び出されたコマンドのテキストと同じ名前のプロジェクトが検索されます。また、<xref:EnvDTE.SolutionBuild.StartupProjects%2A> プロパティに絶対パスを設定することで、これはスタートアップ プロジェクトとして設定されます。

    ```csharp
    private void OnInvokedDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand invokedCommand = (DynamicItemMenuCommand)sender;
        // If the command is already checked, we don't need to do anything
        if (invokedCommand.Checked)
            return;

        // Find the project that corresponds to the command text and set it as the startup project
        var projects = dte2.Solution.Projects;
        foreach (Project proj in projects)
        {
            if (invokedCommand.Text.Equals(proj.Name))
            {
                dte2.Solution.SolutionBuild.StartupProjects = proj.FullName;
                return;
            }
        }
    }
    ```

2. `OnBeforeQueryStatusDynamicItem` イベント ハンドラーを追加します。 これは、`QueryStatus` イベントの前に呼び出されるハンドラーです。 メニュー項目が "実際の" 項目であるかどうか (つまりプレースホルダー項目ではないかどうか) と、項目が既に確認されているかどうか (つまり、プロジェクトが既にスタートアップ プロジェクトとして設定されているかどうか) が判断されます。

    ```csharp
    private void OnBeforeQueryStatusDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand matchedCommand = (DynamicItemMenuCommand)sender;
        matchedCommand.Enabled = true;
        matchedCommand.Visible = true;

        // Find out whether the command ID is 0, which is the ID of the root item.
        // If it is the root item, it matches the constructed DynamicItemMenuCommand,
         // and IsValidDynamicItem won't be called.
        bool isRootItem = (matchedCommand.MatchedCommandId == 0);

        // The index is set to 1 rather than 0 because the Solution.Projects collection is 1-based.
        int indexForDisplay = (isRootItem ? 1 : (matchedCommand.MatchedCommandId - (int) DynamicMenuPackageGuids.cmdidMyCommand) + 1);

        matchedCommand.Text = dte2.Solution.Projects.Item(indexForDisplay).Name;

        Array startupProjects = (Array)dte2.Solution.SolutionBuild.StartupProjects;
        string startupProject = System.IO.Path.GetFileNameWithoutExtension((string)startupProjects.GetValue(0));

        // Check the command if it isn't checked already selected
        matchedCommand.Checked = (matchedCommand.Text == startupProject);

        // Clear the ID because we are done with this item.
        matchedCommand.MatchedCommandId = 0;
    }
    ```

## <a name="implement-the-command-id-match-predicate"></a>コマンド ID の match 述語を実装する

次に、match 述語を実装します。 2 つのことを判断する必要があります。1 つ目はコマンド ID が有効かどうか (宣言されたコマンド ID 以上かどうか)、2 つ目は可能なプロジェクトが指定されているかどうか (ソリューション内のプロジェクト数未満かどうか) です。

```csharp
private bool IsValidDynamicItem(int commandId)
{
    // The match is valid if the command ID is >= the id of our root dynamic start item
    // and the command ID minus the ID of our root dynamic start item
    // is less than or equal to the number of projects in the solution.
    return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);
}
```

## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>ソリューションに複数のプロジェクトがある場合にのみ読み込むように VSPackage を設定する
 アクティブなソリューションに複数のプロジェクトがない限り、 **[スタートアップ プロジェクトの設定]** コマンドは意味をなさないため、そのような場合にのみ VSPackage を自動的に読み込むように設定できます。 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> を UI コンテキスト <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects> と共に使用します。 *DynamicMenuPackage.cs* ファイルに、次の属性を DynamicMenuPackage クラスに追加します。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
[ProvideMenuResource("Menus.ctmenu", 1)]
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]
[Guid(DynamicMenuPackage.PackageGuidString)]
public sealed class DynamicMenuItemsPackage : Package
{}
```

## <a name="test-the-set-startup-project-command"></a>[スタートアップ プロジェクトの設定] コマンドをテストする
 これで、コードをテストできるようになりました。

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. 実験用インスタンスで、複数のプロジェクトがあるソリューションを開きます。

     **ソリューション エクスプローラー** ツール バーに矢印アイコンが表示されます。 展開すると、ソリューション内のさまざまなプロジェクトを表すメニュー項目が表示されます。

3. プロジェクトの 1 つを確認すると、それがスタートアップ プロジェクトになります。

4. ソリューションを閉じるか、プロジェクトが 1 つしかないソリューションを開くと、ツール バー アイコンは非表示になります。

## <a name="see-also"></a>こちらもご覧ください
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
