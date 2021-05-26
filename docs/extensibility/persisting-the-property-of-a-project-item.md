---
title: プロジェクト項目のプロパティの保存 | Microsoft Docs
description: 拡張されたプロジェクト タイプのプロジェクト ファイルにプロパティを格納して、プロジェクト項目に追加するプロパティを保存する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- properties, adding to a project item
- project items, adding properties
ms.assetid: d7a0f2b0-d427-4d49-9536-54edfb37c0f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58c46da9023cc64246f1ea9ee4bde1ec866c545d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090357"
---
# <a name="persist-the-property-of-a-project-item"></a>プロジェクト項目のプロパティの保存
ソース ファイルの作成者など、プロジェクト項目に追加したプロパティを保存することもできます。 これを行うには、プロパティをプロジェクト ファイルに格納します。

 プロジェクト ファイルでプロパティを保存するための最初の手順は、プロジェクトの階層を <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> インターフェイスとして取得することです。 このインターフェイスは、オートメーションを使用するか、<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> を使用して取得できます。 インターフェイスを取得したら、それを使用して、現在選択されているプロジェクト項目を特定できます。 プロジェクト項目 ID を取得したら、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> を使用してプロパティを追加できます。

 次の手順では、*VsPkg.cs* プロパティ `Author` を値 `Tom` と共にプロジェクト ファイルに保存します。

## <a name="to-obtain-the-project-hierarchy-with-the-dte-object"></a>DTE オブジェクトを使用してプロジェクト階層を取得するには

1. 次のコードを VSPackage に追加します。

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    ```

## <a name="to-persist-the-project-item-property-with-the-dte-object"></a>DTE オブジェクトを使用してプロジェクト項目のプロパティを保存するには

1. 前の手順でメソッドに指定したコードに次のコードを追加します。

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item(
            "VsPkg.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-obtain-the-project-hierarchy-using-ivsmonitorselection"></a>IVsMonitorSelection を使用してプロジェクト階層を取得するには

1. 次のコードを VSPackage に追加します。

    ```csharp
    IVsHierarchy hierarchy = null;
    IntPtr hierarchyPtr = IntPtr.Zero;
    IntPtr selectionContainer = IntPtr.Zero;
    uint itemid;

    // Retrieve shell interface in order to get current selection
    IVsMonitorSelection monitorSelection =     Package.GetGlobalService(typeof(SVsShellMonitorSelection)) as     IVsMonitorSelection;
    if (monitorSelection == null)
        throw new InvalidOperationException();

    try
    {
        // Get the current project hierarchy, project item, and selection container for the current selection
        // If the selection spans multiple hierachies, hierarchyPtr is Zero
        IVsMultiItemSelect multiItemSelect = null;
        ErrorHandler.ThrowOnFailure(
            monitorSelection.GetCurrentSelection(
                out hierarchyPtr, out itemid,
                out multiItemSelect, out selectionContainer));

        // We only care if there is only one node selected in the tree
        if (!(itemid == VSConstants.VSITEMID_NIL ||
            hierarchyPtr == IntPtr.Zero ||
            multiItemSelect != null ||
            itemid == VSConstants.VSITEMID_SELECTION))
        {
            hierarchy = Marshal.GetObjectForIUnknown(hierarchyPtr)
                as IVsHierarchy;
        }
    }
    finally
    {
        if (hierarchyPtr != IntPtr.Zero)
            Marshal.Release(hierarchyPtr);
        if (selectionContainer != IntPtr.Zero)
            Marshal.Release(selectionContainer);
    }
    ```

## <a name="to-persist-the-selected-project-item-property-given-the-project-hierarchy"></a>プロジェクト階層を指定して、選択したプロジェクト項目のプロパティを保存するには

1. 前の手順でメソッドに指定したコードに次のコードを追加します。

    ```csharp
    IVsBuildPropertyStorage buildPropertyStorage =
        hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        buildPropertyStorage.SetItemAttribute(itemId, "Author", "Tom");
    }
    ```

## <a name="to-verify-that-the-property-is-persisted"></a>プロパティが保存されていることを確認するには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を起動し、ソリューションを開くか作成します。

2. **ソリューション エクスプローラー** でプロジェクト項目 VsPkg.cs を選択します。

3. ブレークポイントを使用するか、または VSPackage が読み込まれていることと、SetItemAttribute が実行されることを確認します。

   > [!NOTE]
   > UI コンテキスト <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid> で VSPackage を自動読み込みできます。 詳細については、[VSPackage を読み込む](../extensibility/loading-vspackages.md)に関するページを参照してください。

4. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を閉じてから、メモ帳でプロジェクト ファイルを開きます。 次のように、値 Tom と共に \<Author> タグが表示されます。

   ```xml
   <Compile Include="VsPkg.cs">
       <Author>Tom</Author>
   </Compile>
   ```

## <a name="see-also"></a>関連項目

- [カスタム ツール](../extensibility/internals/custom-tools.md)
