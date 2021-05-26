---
title: プロジェクトのプロパティの取得 | Microsoft Docs
description: ツール ウィンドウでプロジェクトのプロパティを表示する方法について説明します。 この例では、ツール ウィンドウのツリー コントロールを示します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- project properties, displaying in tool window
- tool windows, displaying project properties
ms.assetid: 96ba07ca-0811-4013-8602-12550ac4ba79
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8de3f32951cb70b8115781ce067950c7e518b102
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057664"
---
# <a name="get-project-properties"></a>プロジェクトのプロパティの取得

このチュートリアルでは、ツール ウィンドウでプロジェクトのプロパティを表示する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>VSIX プロジェクトを作成してツール ウィンドウを追加する方法

1. すべての Visual Studio 拡張機能は、拡張機能アセットを格納する VSIX デプロイ プロジェクトから始まります。 `ProjectPropertiesExtension` という名前の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. `ProjectPropertiesToolWindow` という名前のカスタム ツール ウィンドウ項目テンプレートを追加して、ツール ウィンドウを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C# 項目]**  >  **[機能拡張]** の順にアクセスし、 **[カスタム ツール ウィンドウ]** を選択します。 ダイアログの下部にある **[名前]** フィールドで、ファイル名を `ProjectPropertiesToolWindow.cs` に変更します。 カスタム ツール ウィンドウの作成方法について詳しくは、「[ツールウィンドウで拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)」をご覧ください。

3. ソリューションをビルドし、エラーが発生することなくソリューションがコンパイルされることを確認します。

### <a name="to-display-project-properties-in-a-tool-window"></a>ツール ウィンドウでプロジェクトのプロパティを表示する方法

1. ProjectPropertiesToolWindowCommand.cs ファイルで、次の using ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using System.Windows.Controls;

    ```

2. *ProjectPropertiesToolWindowControl.xaml* で、既存のボタンを削除し、ツール ボックスから TreeView を追加します。 また、*ProjectPropertiesToolWindowControl.xaml.cs* ファイルから click イベント ハンドラーを削除することもできます。

3. *ProjectPropertiesToolWindowCommand.cs* で、`ShowToolWindow()` メソッドを使用してプロジェクトを開き、そのプロパティを読み取り、プロパティを TreeView に追加します。 ShowToolWindow のコードは次のようになります。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        ToolWindowPane window = this.package.FindToolWindow(typeof(ProjectPropertiesToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create window.");
        }
        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        // Get the tree view and populate it if there is a project open.
        ProjectPropertiesToolWindowControl control = (ProjectPropertiesToolWindowControl)window.Content;
        TreeView treeView = control.treeView;

        // Reset the TreeView to 0 items.
        treeView.Items.Clear();

        DTE dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));
        Projects projects = dte.Solution.Projects;
        if (projects.Count == 0)   // no project is open
        {
            TreeViewItem item = new TreeViewItem();
            item.Name = "Projects";
            item.ItemsSource = new string[]{ "no projects are open." };
            item.IsExpanded = true;
            treeView.Items.Add(item);
            return;
        }

        Project project = projects.Item(1);
        TreeViewItem item1 = new TreeViewItem();
        item1.Header = project.Name + "Properties";
        treeView.Items.Add(item1);

        foreach (Property property in project.Properties)
        {
            TreeViewItem item = new TreeViewItem();
            item.ItemsSource = new string[] { property.Name };
            item.IsExpanded = true;
            treeView.Items.Add(item);
        }
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. この実験用インスタンスで、プロジェクトを開きます。

6. **[表示]**  >  **[その他のウィンドウ]** で、 **[ProjectPropertiesToolWindow]** をクリックします。

  ツール ウィンドウにツリー コントロールが表示され、共に最初のプロジェクトとそのすべてのプロジェクト プロパティの名前が表示されます。
