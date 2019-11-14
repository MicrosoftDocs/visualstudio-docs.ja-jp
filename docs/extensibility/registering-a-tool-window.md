---
title: ツールウィンドウの登録 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34fddd6513aad612398c700b935c6d1d3ee72b59
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186260"
---
# <a name="register-a-tool-window"></a>ツールウィンドウを登録する
<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> と <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>を使用して、ツールウィンドウを登録できます。

## <a name="example"></a>例

```csharp

[ProvideToolWindow(typeof(PersistedWindowPane), Style = MsVsShell.VsDockStyle.Tabbed, Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
[ProvideToolWindow(typeof(DynamicWindowPane), PositionX=250, PositionY=250, Width=160, Height=180, Transient=true)]
[ProvideToolWindowVisibility(typeof(DynamicWindowPane), /*UICONTEXT_SolutionExists*/"f1536ef8-92ec-443c-9ed7-fdadf150da82")]
[ProvideMenuResource(1000, 1)]
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("01069CDD-95CE-4620-AC21-DDFF6C57F012")]
public class PackageToolWindow : Package
{
```

 上記のコードでは、<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> によって `PersistedWindowPane` と `DynamicWindowPane` ツールウィンドウが Visual Studio に登録されます。 永続化されたツールウィンドウはドッキングされ、**ソリューションエクスプローラー**でタブが付けられます。また、動的ウィンドウには、既定の開始位置とサイズが指定されます。 動的ウィンドウは一時的に作成されます。これは、起動時に作成されないことを示します。 これにより、システムレジストリの `ToolWindows` キーに `DontForceCreate` 値が書き込まれます。 詳細については、「[ツールウィンドウの表示構成](/visualstudio/extensibility/tool-window-display-configuration?view=vs-2015)」を参照してください。
