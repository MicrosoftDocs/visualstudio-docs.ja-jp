---
title: 複数インスタンスのツール ウィンドウの作成 | Microsoft Docs
description: ツール ウィンドウを変更して、複数のインスタンスを同時に開くことができるようにする方法について説明します。 既定では、ツール ウィンドウは 1 つのインスタンスしか開くことができません。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce6122cbf4d6f85ab50e067fbbd643053ac4e4dd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089356"
---
# <a name="create-a-multi-instance-tool-window"></a>複数インスタンスのツール ウィンドウの作成
ツール ウィンドウをプログラムすると、複数のインスタンスを同時に開くことができます。 既定では、ツール ウィンドウは 1 つのインスタンスしか開くことができません。

複数インスタンスのツール ウィンドウを使用すると、複数の関連する情報ソースを同時に表示できます。 たとえば、複数インスタンスのツール ウィンドウに複数行の <xref:System.Windows.Forms.TextBox> コントロールを配置すると、プログラミング セッション中に複数のコード スニペットを同時に使用できます。 また、たとえば複数インスタンスのツール ウィンドウに <xref:System.Windows.Forms.DataGrid> コントロールとドロップダウン リスト ボックスを配置すると、複数のリアルタイム データ ソースを同時に追跡できます。

## <a name="create-a-basic-single-instance-tool-window"></a>基本 (単一インスタンス) のツール ウィンドウを作成する

1. VSIX テンプレートを使用して **MultiInstanceToolWindow** という名前のプロジェクトを作成し、**MIToolWindow** という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツール ウィンドウでの拡張機能の作成について詳しくは、「[ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」をご覧ください。

## <a name="make-a-tool-window-multi-instance"></a>ツール ウィンドウを複数インスタンスにする

1. *MIToolWindowPackage.cs* ファイルを開き、`ProvideToolWindow` 属性を見つけます。 次の例に示すように、`MultiInstances=true` パラメーターを指定します。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
        [ProvideMenuResource("Menus.ctmenu", 1)]
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]
        [Guid(MIToolWindowPackage.PackageGuidString)]
        public sealed class MIToolWindowPackage : Package
    {. . .}
    ```

2. *MIToolWindowCommand.cs* ファイルで、`ShowToolWindos()` メソッドを見つけます。 このメソッドでは、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> メソッドを呼び出し、その `create` フラグを `false` に設定します。これにより、使用可能な `id` が見つかるまで、既存のツール ウィンドウ インスタンスが反復処理されます。

3. ツール ウィンドウのインスタンスを作成するには、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> メソッドを呼び出して、`id` を使用可能な値に設定し、`create` フラグを `true` に設定します。

    既定では、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> メソッドの `id` パラメーターの値は `0` です。 この値により、単一インスタンスのツール ウィンドウが作成されます。 複数のインスタンスをホストするには、すべてのインスタンスが一意の `id` を持つ必要があります。

4. ツール ウィンドウ インスタンスの <xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A> プロパティによって返される <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> オブジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> メソッドを呼び出します。

5. 既定では、ツール ウィンドウ項目テンプレートによって作成された `ShowToolWindow` メソッドでは、単一インスタンスのツール ウィンドウが作成されます。 次の例では、`ShowToolWindow` メソッドを変更して複数のインスタンスを作成する方法を示します。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        for (int i = 0; i < 10; i++)
        {
            ToolWindowPane window = this.package.FindToolWindow(typeof(MIToolWindow), i, false);
            if (window == null)
            {
                // Create the window with the first free ID.
                window = (ToolWindowPane)this.package.FindToolWindow(typeof(MIToolWindow), i, true);
                if ((null == window) || (null == window.Frame))
                {
                    throw new NotSupportedException("Cannot create tool window");
                }

            IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());
            break;
            }
        }
    }
    ```
