---
title: ユニバーサル Windows プロジェクトの管理 | Microsoft Docs
description: ユニバーサル Windows アプリをサポートするには、プロジェクトを管理する Visual Studio 拡張機能で、ユニバーサル Windows アプリ プロジェクトの構造を認識している必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8af418d8ffcaad18aca4497078f4e24f9bb679fd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090643"
---
# <a name="manage-universal-windows-projects"></a>ユニバーサル Windows プロジェクトを管理する

ユニバーサル Windows アプリは、Windows 8.1 と Windows Phone 8.1 の両方をターゲットとするアプリであり、これにより、開発者はコードやその他の資産を両方のプラットフォームで使用できます。 共有されるコードとリソースが共有プロジェクトに保持されるのに対して、プラットフォーム固有のコードとリソースは、Windows 用と Windows Phone 用に 1 つずつの個別のプロジェクトに保持されます。 ユニバーサル Windows アプリの詳細については、[ユニバーサル Windows アプリ](/windows/uwp/get-started/create-uwp-apps)に関するページを参照してください。 プロジェクトを管理する Visual Studio 拡張機能で、ユニバーサル Windows アプリ プロジェクトの構造が単一プラットフォーム アプリのものとは異なることを認識している必要があります。 このチュートリアルでは、共有プロジェクトを操作したり、共有項目を管理したりする方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールすることはしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="navigate-the-shared-project"></a>共有プロジェクトを操作する

1. **TestUniversalProject** という名前の C# VSIX プロジェクトを作成します。 ( **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** 、次に **[C#]**  >  **[機能拡張]**  >  **[Visual Studio パッケージ]** )。 **[カスタム コマンド]** プロジェクト項目テンプレートを追加します (**ソリューション エクスプローラー** で、プロジェクト ノードを右クリックし、 **[追加]**  >  **[新しい項目]** の順に選択してから **[機能拡張]** に移動します)。 このファイルに **TestUniversalProject** という名前を付けます。

2. *Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime.dll* と *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll* ( **[拡張機能]** セクション) への参照を追加します。

3. *TestUniversalProject.cs* を開き、次の `using` ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.PlatformUI;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using System.Collections.Generic;
    using System.IO;
    using System.Windows.Forms;
    ```

4. `TestUniversalProject` クラスで、 **[出力]** ウィンドウを指すプライベート フィールドを追加します。

    ```csharp
    public sealed class TestUniversalProject
    {
        IVsOutputWindowPane output;
    . . .
    }
    ```

5. TestUniversalProject コンストラクター内の出力ウィンドウへの参照を設定します。

    ```csharp
    private TestUniversalProject(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);
            EventHandler eventHandler = this.ShowMessageBox;
            MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);
            commandService.AddCommand(menuItem);
        }

        // get a reference to the Output window
        output = (IVsOutputWindowPane)ServiceProvider.GetService(typeof(SVsGeneralOutputWindowPane));
    }
    ```

6. `ShowMessageBox` メソッドから既存のコードを削除します。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
    }
    ```

7. DTE オブジェクトを取得します。これは、このチュートリアルでいくつかの異なる目的に使用します。 また、メニュー ボタンがクリックされたときにソリューションが読み込まれることを確認します。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (EnvDTE.DTE)this.ServiceProvider.GetService(typeof(EnvDTE.DTE));
        if (dte.Solution != null)
        {
            . . .
        }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

8. 共有プロジェクトを見つけます。 共有プロジェクトは純粋なコンテナーであり、出力を構築したり生成したりしません。 次のメソッドでは、共有プロジェクト機能を持つ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> オブジェクトを探すことによって、ソリューション内の最初の共有プロジェクトを見つけます。

    ```csharp
    private IVsHierarchy FindSharedProject()
    {
        var sln = (IVsSolution)this.ServiceProvider.GetService(typeof(SVsSolution));
        Guid empty = Guid.Empty;
        IEnumHierarchies enumHiers;

        //get all the projects in the solution
        ErrorHandler.ThrowOnFailure(sln.GetProjectEnum((uint)__VSENUMPROJFLAGS.EPF_LOADEDINSOLUTION, ref empty, out enumHiers));
        foreach (IVsHierarchy hier in ComUtilities.EnumerableFrom(enumHiers))
        {
            if (PackageUtilities.IsCapabilityMatch(hier, "SharedAssetsProject"))
            {
                return hier;
            }
        }
        return null;
    }
    ```

9. `ShowMessageBox` メソッドで、共有プロジェクトのキャプション (**ソリューション エクスプローラー** に表示されるプロジェクト名) を出力します。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Found shared project: {0}\n", sharedCaption));
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
                return;
            }
        }
        else
        {
            MessageBox.Show("No solution is open");
            return;
        }
    }
    ```

10. アクティブなプラットフォーム プロジェクトを取得します。 プラットフォーム プロジェクトは、プラットフォーム固有のコードとリソースが含まれているプロジェクトです。 次のメソッドでは、新しいフィールド <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy> を使用して、アクティブなプラットフォーム プロジェクトを取得します。

    ```csharp
    private IVsHierarchy GetActiveProjectContext(IVsHierarchy hierarchy)
    {
        IVsHierarchy activeProjectContext;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, out activeProjectContext))
        {
            return activeProjectContext;
        }
        else
        {
            return null;
        }
    }
    ```

11. `ShowMessageBox` メソッドで、アクティブなプラットフォーム プロジェクトのキャプションを出力します。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));

        if (dte.Solution != null)
        {
            var sharedHier = this.FindSharedProject();
            if (sharedHier != null)
            {
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,
                     (int)__VSHPROPID.VSHPROPID_Caption);
                output.OutputStringThreadSafe(string.Format("Shared project: {0}\n", sharedCaption));

                var activePlatformHier = this.GetActiveProjectContext(sharedHier);
                if (activePlatformHier != null)
                {
                    string activeCaption = HierarchyUtilities.GetHierarchyProperty<string>(activePlatformHier,
                         (uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID.VSHPROPID_Caption);
                    output.OutputStringThreadSafe(string.Format("Active platform project: {0}\n", activeCaption));
                }
                else
                {
                    MessageBox.Show("Shared project has no active platform project");
                }
            }
            else
            {
                MessageBox.Show("Solution has no shared project");
            }
        }
        else
        {
            MessageBox.Show("No solution is open");
        }
    }
    ```

12. プラットフォーム プロジェクトを反復処理します。 次のメソッドでは、共有プロジェクトからすべてのインポート (プラットフォーム) プロジェクトを取得します。

    ```csharp
    private IEnumerable<IVsHierarchy> EnumImportingProjects(IVsHierarchy hierarchy)
    {
        IVsSharedAssetsProject sharedAssetsProject;
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID7.VSHPROPID_SharedAssetsProject, out sharedAssetsProject)
            && sharedAssetsProject != null)
        {
            foreach (IVsHierarchy importingProject in sharedAssetsProject.EnumImportingProjects())
            {
                yield return importingProject;
            }
        }
    }
    ```

    > [!IMPORTANT]
    > ユーザーが実験用インスタンスで C++ ユニバーサル Windows アプリ プロジェクトを開いている場合は、上記のコードによって例外がスローされます。 これは既知の問題です。 この例外を回避するには、上記の `foreach` ブロックを次のコードに置き換えます。

    ```csharp
    var importingProjects = sharedAssetsProject.EnumImportingProjects();
    for (int i = 0; i < importingProjects.Count; ++i)
    {
        yield return importingProjects[i];
    }
    ```

13. `ShowMessageBox` メソッドで、各プラットフォーム プロジェクトのキャプションを出力します。 アクティブなプラットフォーム プロジェクトのキャプションを出力する行の後に、次のコードを挿入します。 この一覧には、読み込まれているプラットフォーム プロジェクトのみが表示されます。

    ```csharp
    output.OutputStringThreadSafe("Platform projects:\n");

    IEnumerable<IVsHierarchy> projects = this.EnumImportingProjects(sharedHier);

    bool isActiveProjectSet = false;
    foreach (IVsHierarchy platformHier in projects)
    {
        string platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
            (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));
    }
    ```

14. アクティブなプラットフォーム プロジェクトを変更します。 次のメソッドでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A> を使用してアクティブなプロジェクトを設定します。

    ```csharp
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)
    {
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);
    }
    ```

15. `ShowMessageBox` メソッドで、アクティブなプラットフォーム プロジェクトを変更します。 このコードを `foreach` ブロック内に挿入します。

    ```csharp
    bool isActiveProjectSet = false;
    string platformCaption = null;
    foreach (IVsHierarchy platformHier in projects)
    {
        platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,
             (int)__VSHPROPID.VSHPROPID_Caption);
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));

        // if this project is neither the shared project nor the current active platform project,
        // set it to be the active project
        if (!isActiveProjectSet && platformHier != activePlatformHier)
        {
            this.SetActiveProjectContext(sharedHier, platformHier);
            activePlatformHier = platformHier;
            isActiveProjectSet = true;
        }
    }
    output.OutputStringThreadSafe("set active project: " + platformCaption +'\n');
    ```

16. では、試してみましょう。F5 キーを押して実験用インスタンスを起動します。 実験用インスタンスで C# ユニバーサル ハブ アプリ プロジェクトを作成します ( **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]**  >  **[Windows]**  >  **[Windows 8]**  >  **[ユニバーサル]**  >  **[ハブ アプリ]** )。 ソリューションが読み込まれたら、 **[ツール]** メニューに移動し、 **[TestUniversalProject の呼び出し]** をクリックして **[出力]** ウィンドウのテキストを確認します。 次のように表示されます。

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    ```

### <a name="manage-the-shared-items-in-the-platform-project"></a>プラットフォーム プロジェクトで共有項目を管理する

1. プラットフォーム プロジェクトで共有項目を見つけます。 共有プロジェクト内の項目は、プラットフォーム プロジェクトでは共有項目として表示されます。 これらは、**ソリューション エクスプローラー** には表示できませんが、プロジェクト階層内を移動して見つけることができます。 次のメソッドでは、この階層内を移動して、すべての共有項目を収集します。 また、必要に応じて各項目のキャプションを出力します。 共有項目は、新しいプロパティ <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_IsSharedItem> によって識別されます。

    ```csharp
    private void InspectHierarchyItems(IVsHierarchy hier, uint itemid, int level, List<uint> itemIds, bool getSharedItems, bool printItems)
    {
        string caption = HierarchyUtilities.GetHierarchyProperty<string>(hier, itemid, (int)__VSHPROPID.VSHPROPID_Caption);
        if (printItems)
            output.OutputStringThreadSafe(string.Format("{0}{1}\n", new string('\t', level), caption));

        // if getSharedItems is true, inspect only shared items; if it's false, inspect only unshared items
        bool isSharedItem;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID7.VSHPROPID_IsSharedItem, out isSharedItem)
            && (isSharedItem == getSharedItems))
        {
            itemIds.Add(itemid);
        }

        uint child;
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID.VSHPROPID_FirstChild, Unbox.AsUInt32, out child)
            && child != (uint)VSConstants.VSITEMID.Nil)
        {
            this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);

            while (HierarchyUtilities.TryGetHierarchyProperty(hier, child, (int)__VSHPROPID.VSHPROPID_NextSibling, Unbox.AsUInt32, out child)
                && child != (uint)VSConstants.VSITEMID.Nil)
            {
                this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);
            }
        }
    }
    ```

2. `ShowMessageBox` メソッドで、プラットフォーム プロジェクト階層項目内を移動する次のコードを追加します。 これを `foreach` ブロック内に挿入します。

    ```csharp
    output.OutputStringThreadSafe("Walk the active platform project:\n");
    var sharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ```

3. 共有項目を読み取ります。 共有項目は、プラットフォーム プロジェクトでは非表示のリンクされたファイルとして表示されるため、すべてのプロパティを通常のリンクされたファイルとして読み取ることができます。 次のコードでは、最初の共有項目の完全なパスを読み取ります。

    ```csharp
    var sharedItemId = sharedItemIds[0];
    string fullPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));
    ```

4. では、試してみましょう。**F5** キーを押して実験用インスタンスを起動します。 実験用インスタンスで C# ユニバーサル ハブ アプリ プロジェクトを作成して ( **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]**  >  **[Windows]**  >  **[Windows 8]**  >  **[ユニバーサル]**  >  **[ハブ アプリ]** ) **[ツール]** メニューに移動し、 **[TestUniversalProject の呼び出し]** をクリックして **[出力]** ウィンドウのテキストを確認します。 次のように表示されます。

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    Walk the active platform project:
        HubApp.WindowsPhone
            <HubApp.Shared>
                App.xaml
                    App.xaml.cs
                Assets
                    DarkGray.png
                    LightGray.png
                    MediumGray.png
                Common
                    NavigationHelper.cs
                    ObservableDictionary.cs
                    RelayCommand.cs
                    SuspensionManager.cs
                DataModel
                    SampleData.json
                    SampleDataSource.cs
                HubApp.Shared.projitems
                Strings
                    en-US
                        Resources.resw
            Assets
                HubBackground.theme-dark.png
                HubBackground.theme-light.png
                Logo.scale-240.png
                SmallLogo.scale-240.png
                SplashScreen.scale-240.png
                Square71x71Logo.scale-240.png
                StoreLogo.scale-240.png
                WideLogo.scale-240.png
            HubPage.xaml
                HubPage.xaml.cs
            ItemPage.xaml
                ItemPage.xaml.cs
            Package.appxmanifest
            Properties
                AssemblyInfo.cs
            References
                .NET for Windows Store apps
                HubApp.Shared
                Windows Phone 8.1
            SectionPage.xaml
                SectionPage.xaml.cs
    ```

### <a name="detect-changes-in-platform-projects-and-shared-projects"></a>プラットフォーム プロジェクトと共有プロジェクト内の変更を検出する

1. 階層とプロジェクト イベントを使用すると、プラットフォーム プロジェクトの場合と同様に、共有プロジェクト内の変更を検出できます。 ただし、共有プロジェクト内のプロジェクト項目は表示されません。つまり、共有プロジェクト項目が変更されたとき、特定のイベントは発生しません。

    プロジェクト内のファイルの名前が変更されたときの一連のイベントを考えてみます。

   1. ファイル名がディスク上で変更されます。

   2. プロジェクト ファイルは、そのファイルの新しい名前を含むように更新されます。

      階層イベント (<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> など) は一般に、**ソリューション エクスプローラー** のように、UI に表示される変更を追跡します。 階層イベントでは、ファイル名の変更操作を、ファイルの削除とその後のファイルの追加で構成されると見なします。 ただし、表示されない項目が変更されたとき、階層イベント システムでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> イベントが発生しますが、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> イベントは発生しません。 そのため、プラットフォーム プロジェクト内のファイルの名前を変更した場合は <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> の両方を取得しますが、共有プロジェクト内のファイルの名前を変更した場合は <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> しか取得しません。

      プロジェクト項目内の変更を追跡するために、DTE プロジェクト項目イベント (<xref:EnvDTE.ProjectItemsEventsClass> にあるイベント) を処理することができます。 ただし、多数のイベントを処理している場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> でイベントを処理した方が高いパフォーマンスを得ることができます。 このチュートリアルでは、階層イベントと DTE イベントのみを示します。 この手順では、共有プロジェクトとプラットフォーム プロジェクトにイベント リスナーを追加します。 その後、共有プロジェクト内のあるファイルとプラットフォーム プロジェクト内の別のファイルの名前を変更すると、名前の変更操作ごとに発生したイベントを確認できます。

      この手順では、共有プロジェクトとプラットフォーム プロジェクトにイベント リスナーを追加します。 その後、共有プロジェクト内のあるファイルとプラットフォーム プロジェクト内の別のファイルの名前を変更すると、名前の変更操作ごとに発生したイベントを確認できます。

2. イベント リスナーを追加します。 プロジェクトに新しいクラス ファイルを追加し、それに *HierarchyEventListener.cs* という名前を付けます。

3. *HierarchyEventListener.cs* ファイルを開き、ディレクティブを使用して次を追加します。

   ```csharp
   using Microsoft.VisualStudio.Shell.Interop;
   using Microsoft.VisualStudio;
   using System.IO;
   ```

4. `HierarchyEventListener` クラスに <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> を実装します。

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   { }
   ```

5. 次のコードのように、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> のメンバーを実装します。

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   {
       private IVsHierarchy hierarchy;
       IVsOutputWindowPane output;

       internal HierarchyEventListener(IVsHierarchy hierarchy, IVsOutputWindowPane outputWindow) {
            this.hierarchy = hierarchy;
            this.output = outputWindow;
       }

       int IVsHierarchyEvents.OnInvalidateIcon(IntPtr hIcon) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnInvalidateItems(uint itemIDParent) {
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemAdded(uint itemIDParent, uint itemIDSiblingPrev, uint itemIDAdded) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemAdded: " + itemIDAdded + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemDeleted(uint itemID) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemDeleted: " + itemID + "\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnItemsAppended(uint itemIDParent) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemsAppended\n");
           return VSConstants.S_OK;
       }

       int IVsHierarchyEvents.OnPropertyChanged(uint itemID, int propID, uint flags) {
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnPropertyChanged: item ID " + itemID + "\n");
           return VSConstants.S_OK;
       }
   }
   ```

6. 同じクラスで、プロジェクト項目の名前が変更されるたびに発生する DTE イベント <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> のための別のイベント ハンドラーを追加します。

   ```csharp
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)
   {
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));
   }
   ```

7. 階層イベントにサインアップします。 追跡するプロジェクトごとに個別にサインアップする必要があります。 `ShowMessageBox` に次のコードを追加します。1 つは共有プロジェクト用、もう 1 つはいずれかのプラットフォーム プロジェクト用です。

   ```csharp
   // hook up the event listener for hierarchy events on the shared project
   HierarchyEventListener listener1 = new HierarchyEventListener(sharedHier, output);
   uint cookie1;
   sharedHier.AdviseHierarchyEvents(listener1, out cookie1);

   // hook up the event listener for hierarchy events on the
   active project
   HierarchyEventListener listener2 = new HierarchyEventListener(activePlatformHier, output);
   uint cookie2;
   activePlatformHier.AdviseHierarchyEvents(listener2, out cookie2);
   ```

8. DTE プロジェクト項目イベント <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> にサインアップします。 2 番目のリスナーをフックした後、次のコードを追加します。

   ```csharp
   // hook up DTE events for project items
   Events2 dteEvents = (Events2)dte.Events;
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;
   ```

9. 共有項目を変更します。 プラットフォーム プロジェクトで共有項目を変更することはできません。代わりに、これらの項目の実際の所有者である共有プロジェクトで変更する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> を使用して共有プロジェクト内の対応する項目 ID を取得し、それに共有項目の完全なパスを割り当てることができます。 その後、その共有項目を変更できます。 この変更がプラットフォーム プロジェクトに伝達されます。

    > [!IMPORTANT]
    > プロジェクト項目を変更する前に、それが共有項目であるかどうかを調べる必要があります。

     次のメソッドでは、プロジェクト項目ファイルの名前を変更します。

    ```csharp
    private void ModifyFileNameInProject(IVsHierarchy project, string path)
    {
        int found;
        uint projectItemID;
        VSDOCUMENTPRIORITY[] priority = new VSDOCUMENTPRIORITY[1];
        if (ErrorHandler.Succeeded(((IVsProject)project).IsDocumentInProject(path, out found, priority, out projectItemID))
            && found != 0)
        {
            var name = DateTime.Now.Ticks.ToString() + Path.GetExtension(path);
            project.SetProperty(projectItemID, (int)__VSHPROPID.VSHPROPID_EditLabel, name);
            output.OutputStringThreadSafe(string.Format("Renamed {0} to {1}\n", path,name));
        }
    }
    ```

10. 共有プロジェクト内の項目のファイル名を変更するには、このメソッドを `ShowMessageBox` 内のその他のすべてのコードの後に呼び出します。 これを、共有プロジェクト内の項目の完全なパスを取得するコードの後に挿入します。

    ```csharp
    // change the file name of an item in a shared project
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));
    this.ModifyFileNameInProject(sharedHier, fullPath);
    ```

11. プロジェクトをビルドして実行します。 実験用インスタンスで C# ユニバーサル ハブ アプリを作成して **[ツール]** メニューに移動し、 **[TestUniversalProject の呼び出し]** をクリックして、一般的な出力ウィンドウのテキストを確認します。 共有プロジェクト内の最初の項目 (これは *App.xaml* ファイルであることが予測されます) の名前が変更され、<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> イベントが発生したことが表示されます。 この場合は、*App.xaml* の名前の変更によって *App.xaml.cs* の名前も変更されるため、4 つのイベント (プラットフォーム プロジェクトごとに 2 つ) が表示されます。 (DTE イベントでは、共有プロジェクト内の項目は追跡されません)。2 つの <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> イベント (プラットフォーム プロジェクトごとに 1 つ) が表示されますが、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> イベントは表示されません。

12. ここで、プラットフォーム プロジェクト内のファイルの名前を変更してみると、発生するイベントの違いを確認できます。 次のコードを `ShowMessageBox` 内の `ModifyFileName` の呼び出しの後に追加します。

    ```csharp
    // change the file name of an item in a platform project
    var unsharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, unsharedItemIds, false, false);

    var unsharedItemId = unsharedItemIds[0];
    string unsharedPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(unsharedItemId, out unsharedPath));
    output.OutputStringThreadSafe(string.Format("Platform project item ID = {0}, full path = {1}\n", unsharedItemId, unsharedPath));

    this.ModifyFileNameInProject(activePlatformHier, unsharedPath);
    ```

13. プロジェクトをビルドして実行します。 実験用インスタンスで C# ユニバーサル プロジェクトを作成して **[ツール]** メニューに移動し、 **[TestUniversalProject の呼び出し]** をクリックして、一般的な出力ウィンドウのテキストを確認します。 プラットフォーム プロジェクト内のファイルの名前が変更されると、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> イベントと <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> イベントの両方が表示されます。 このファイルを変更しても他のファイルは変更されず、またプラットフォーム プロジェクト内の項目の変更はどこにも伝達されないため、これらの各イベントの 1 つだけが発生します。