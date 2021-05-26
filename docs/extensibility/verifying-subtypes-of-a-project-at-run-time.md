---
title: 実行時におけるプロジェクトのサブタイプの確認 | Microsoft Docs
description: 依存する指定されたカスタム プロジェクトのサブタイプの有無を VSPackage に確認させる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c52d3297ce4903cb8f8e7cb2f9ab5169d21ac94e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062604"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>実行時におけるプロジェクトのサブタイプの確認
カスタム プロジェクトのサブタイプに依存する VSPackage には、サブタイプが存在しない場合にも正常に失敗するように、そのサブタイプを検索するロジックを含める必要があります。 次の手順は、指定されたサブタイプの有無を確認する方法を示しています。

### <a name="to-verify-the-presence-of-a-subtype"></a>サブタイプの有無を確認するには

1. VSPackage に次のコードを追加して、プロジェクトとソリューション オブジェクトからプロジェクト階層を <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> オブジェクトとして取得します。

    ```csharp
    EnvDTE.DTE dte;
    dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));

    EnvDTE.Project project;
    project = dte.Solution.Projects.Item(1);

    IVsSolution solution;
    solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));

    IVsHierarchy hierarchy;
    hierarchy = solution.GetProjectOfUniqueName(project.UniqueName);

    ```

2. 階層を <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected> インターフェイスにキャストします。

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> を呼び出して、プロジェクト タイプの GUID の一覧を取得します。

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. 指定されたサブタイプの GUID の一覧を確認します。

    ```csharp
    // Replace the string "MyGUID" with the GUID of the subtype.
    string guidMySubtype = "MyGUID";
    if (projTypeGuids.IndexOf(guidMySubtype) > 0)
    {
        // The specified subtype is present.
    }
    ```

## <a name="see-also"></a>関連項目
- [プロジェクト サブタイプ](../extensibility/internals/project-subtypes.md)
- [プロジェクト サブタイプのデザイン](../extensibility/internals/project-subtypes-design.md)
- [プロジェクト サブタイプによって拡張されるプロパティとメソッド](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
