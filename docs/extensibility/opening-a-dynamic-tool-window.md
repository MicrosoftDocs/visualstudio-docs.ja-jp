---
title: 動的なツール ウィンドウを開く | Microsoft Docs
description: 特定の UI コンテキストが適用されるたびに開き、その UI コンテキストが適用されなくなったときに閉じる動的なツール ウィンドウについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 357644f67da9a3bbc468d708cf39e44f737dbf0f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090422"
---
# <a name="open-a-dynamic-tool-window"></a>動的なツール ウィンドウを開く
ツール ウィンドウは通常、メニューのコマンド、または同等のキーボード ショートカットから開かれます。 ただし、特定の UI コンテキストが適用されるたびに開き、その UI コンテキストが適用されなくなったときに閉じるツール ウィンドウが必要になる場合があります。 これらの種類のツール ウィンドウは、"*動的*" または "*自動表示*" と呼ばれます。

> [!NOTE]
> 定義済みの UI コンテキストの一覧については、「<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>」を参照してください。

 起動時に動的なツール ウィンドウを開くようにしたいが、その作成に失敗する可能性がある場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx> インターフェイスを実装し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A> メソッドでエラー状態をテストする必要があります。 起動時に開く必要のある動的なツール ウィンドウがあることをシェルで認識できるようにするには、パッケージの登録に (1 に設定された) `SupportsDynamicToolOwner` 値を追加する必要があります。 この値は標準の <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> に含まれていないため、これを追加するにはカスタム属性を作成する必要があります。 カスタム属性の詳細については、「[カスタム登録属性を使用して拡張機能を登録する](../extensibility/registering-and-unregistering-vspackages.md#using-a-custom-registration-attribute-to-register-an-extension)」を参照してください。

 ツール ウィンドウを開くには、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> を使用します。 ツール ウィンドウが必要に応じて作成されます。

> [!NOTE]
> 動的なツール ウィンドウは、ユーザーが閉じることができます。 ユーザーがツール ウィンドウを再度開くことができるようにメニュー コマンドを作成する場合は、そのメニュー コマンドを、ツール ウィンドウを開くのと同じ UI コンテキストでは有効にし、それ以外の場合は無効にする必要があります。

## <a name="to-open-a-dynamic-tool-window"></a>動的なツール ウィンドウを開くには

1. **DynamicToolWindow** という名前の VSIX プロジェクトを作成し、*DynamicWindowPane.cs* という名前のツール ウィンドウ項目テンプレートを追加します。 詳細については、[ツール ウィンドウ拡張機能での作成](../extensibility/creating-an-extension-with-a-tool-window.md)に関するページを参照してください。

2. *DynamicWindowPanePackage.cs* ファイルで、DynamicWindowPanePackage の宣言を見つけます。 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> および <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute> 属性を追加して、ツール ウィンドウを登録します。

    ```vb
    [ProvideToolWindow(typeof(DynamicWindowPane)]
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]
    [Guid(DynamicWindowPanePackage.PackageGuidString)]
    public sealed class DynamicWindowPanePackage : Package
    {. . .}
    ```

     上記の属性では、DynamicWindowPane という名前のツール ウィンドウを、Visual Studio が閉じられて再度開かれたときには保持されない一時的なウィンドウとして登録します。 DynamicWindowPane は、<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string> が適用されるたびに開かれ、それ以外の場合は閉じられます。

3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 ツール ウィンドウは表示されません。

4. 実験用インスタンスでプロジェクトを開きます。 ツール ウィンドウが表示されます。
