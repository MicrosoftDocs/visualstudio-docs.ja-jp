---
title: ツール ウィンドウの登録 | Microsoft Docs
description: ProvideToolWindowAttribute と ProvideToolWindowVisibilityAttribute を使用して、ツール ウィンドウを Visual Studio に登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13c3035f089855f88d54ecc8b3c1e6434ac10e65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056585"
---
# <a name="register-a-tool-window"></a>ツール ウィンドウを登録する
ツール ウィンドウは、<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> と <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute> を使用して登録できます。

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

 上記のコードでは、<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> によって `PersistedWindowPane` と `DynamicWindowPane` ツール ウィンドウが Visual Studio に登録されます。 永続化されたツール ウィンドウはドッキングされ、**ソリューション エクスプローラー** でタブが付けられます。また、動的ウィンドウでは、既定の開始位置とサイズが指定されます。 動的ウィンドウは一時的に作成されます。これは、起動時に作成されないことを示します。 これにより、システム レジストリの `ToolWindows` キーに `DontForceCreate` 値が書き込まれます。 詳細については、「[ツール ウィンドウの表示の構成](/previous-versions/visualstudio/visual-studio-2015/extensibility/tool-window-display-configuration?preserve-view=true&view=vs-2015)」を参照してください。