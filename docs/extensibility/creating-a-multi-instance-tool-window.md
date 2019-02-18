---
title: マルチ インスタンスのツール ウィンドウの作成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 687d46136ad4ed0f043210839e95caf6071f87f2
ms.sourcegitcommit: 752f03977f45169585e407ef719450dbe219b7fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56317485"
---
# <a name="create-a-multi-instance-tool-window"></a>マルチ インスタンスのツール ウィンドウを作成します。
複数のインスタンスは同時に開くできるように、ツール ウィンドウをプログラミングできます。 既定では、ツール ウィンドウには 1 つだけのインスタンスを開くことができます。

複数インスタンスのツール ウィンドウを使用すると同時に情報のいくつかの関連するソースを表示できます。 たとえば、複数の行に配置する<xref:System.Windows.Forms.TextBox>プログラミング セッション中にいくつかのコード スニペットは同時に使用できるように、複数インスタンスのツール ウィンドウを制御します。 また、たとえばを置いたり、<xref:System.Windows.Forms.DataGrid>コントロール ドロップダウン リスト ボックスと複数インスタンスのツール ウィンドウで同時にいくつかのリアルタイムのデータ ソースを追跡できるようにします。

## <a name="create-a-basic-single-instance-tool-window"></a>(単一インスタンス) の基本的なツール ウィンドウを作成します。

1. という名前のプロジェクトを作成する**MultiInstanceToolWindow** VSIX のテンプレートを使用して、という名前のカスタム ツール ウィンドウの項目テンプレートを追加**MIToolWindow**します。

    > [!NOTE]
    > ツール ウィンドウで拡張機能の作成の詳細については、次を参照してください。[ツール ウィンドウで拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)します。

## <a name="make-a-tool-window-multi-instance"></a>ツール ウィンドウの複数インスタンスを作成します。

1. 開く、 *MIToolWindowPackage.cs*ファイルを見つけて、`ProvideToolWindow`属性。 および`MultiInstances=true`パラメーターは、次の例に示すようにします。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
        [ProvideMenuResource("Menus.ctmenu", 1)]
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]
        [Guid(MIToolWindowPackage.PackageGuidString)]
        public sealed class MIToolWindowPackage : Package
    {. . .}
    ```

2. *MIToolWindowCommand.cs*ファイルで、検索、`ShowToolWindos()`メソッド。 このメソッドを呼び出して、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>メソッドとその`create`フラグを`false`まで、使用可能なツール ウィンドウの既存のインスタンスを反復ことができるように`id`が見つかった。

3. ツール ウィンドウのインスタンスを作成するには、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>メソッドとその`id`使用可能な値とその`create`フラグを`true`。

    既定の値で、`id`のパラメーター、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>メソッドは`0`します。 この値は、単一インスタンスのツール ウィンドウです。 ホストする 1 つ以上のインスタンスの場合は、すべてのインスタンスを独自の一意なにいる必要があります`id`します。

4. 呼び出す、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>オブジェクトによって返される、<xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A>ツール ウィンドウのインスタンスのプロパティ。

5. 既定で、`ShowToolWindow`ツール ウィンドウの項目テンプレートによって作成されるメソッドは、単一インスタンスのツール ウィンドウを作成します。 次の例を変更する方法を示しています、`ShowToolWindow`メソッドを複数のインスタンスを作成します。

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
