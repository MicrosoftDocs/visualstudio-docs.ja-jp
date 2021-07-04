---
title: プロジェクト項目への属性の追加 | Microsoft Docs
description: Shell Interop メソッドである GetItemAttribute と SetItemAttribute を使用して、Visual Studio でプロジェクト項目に属性を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- attributes [Visual Studio], adding to a project item
ms.assetid: 404a71d5-cce5-44e7-9eaf-d747c794fedb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 36fc5905fd2b1423865982a80a6cb2ba6a803cc5
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902021"
---
# <a name="add-an-attribute-to-a-project-item"></a>プロジェクト項目に属性を追加する
<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetItemAttribute%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> のメソッドは、プロジェクト項目の属性の値を取得し設定します。 SetItemAttribute では、属性がまだ存在しない場合に属性を作成し、プロジェクト項目メタデータに追加します。

## <a name="add-an-attribute-to-a-project-item"></a>プロジェクト項目に属性を追加する

- 次のコードでは、<xref:EnvDTE.DTE> オートメーション オブジェクトと <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetItemAttribute%2A> メソッドを使用して、プロジェクト項目に属性を追加します。 プロジェクト項目 ID は、プロジェクト項目名 "program.cs" から取得されます。 属性 "MyAttribute" がこのプロジェクト項目に追加され、"MyValue" という値が指定されます。

    ```csharp
    EnvDTE.DTE dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));
    EnvDTE.Project project = dte.Solution.Projects.Item(1);

    string uniqueName = project.UniqueName;
    IVsSolution solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));
    IVsHierarchy hierarchy;
    solution.GetProjectOfUniqueName(uniqueName, out hierarchy);
    IVsBuildPropertyStorage buildPropertyStorage = hierarchy as IVsBuildPropertyStorage;
    if (buildPropertyStorage != null)
    {
        uint itemId;
        string fullPath = (string)project.ProjectItems.Item("Program.cs").Properties.Item("FullPath").Value;
        hierarchy.ParseCanonicalName(fullPath, out itemId);
        buildPropertyStorage.SetItemAttribute(itemId, "MyAttribute", "MyValue");
    }

    ```

## <a name="see-also"></a>関連項目
- [MSBuild プロジェクト ファイルにデータを保持する](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
