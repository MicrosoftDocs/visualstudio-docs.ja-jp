---
title: エディター拡張機能から DTE オブジェクトにアクセスする
description: このチュートリアルのコード例を使用して、エディター拡張機能から DTE オブジェクトにアクセスする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/24/2019
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7035842f608428f149dd2c0965b4792afa25db67
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062071"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>チュートリアル: エディター拡張機能から DTE オブジェクトにアクセスする

VSPackage では、DTE オブジェクトの型を使用して <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> メソッドを呼び出すと、DTE オブジェクトを取得できます。 Managed Extensibility Framework (MEF) 拡張機能では、<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> をインポートしてから、<xref:EnvDTE.DTE> の型使用して <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> メソッドを呼び出すことができます。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="get-the-dte-object"></a>DTE オブジェクトを取得する

1. C# VSIX プロジェクトを作成し、**DTETest** という名前を付けます。 **エディター分類子** 項目テンプレートを追加し、**DTETest** という名前を付けます。

   詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

::: moniker range=">=vs-2019"

2. 次のアセンブリ参照をプロジェクトに追加します。

    - Microsoft.VisualStudio.Shell.Framework
    - Microsoft.VisualStudio.Shell.Immutable.10.0

3. *DTETestProvider.cs* ファイルで、次の `using` ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. `DTETestProvider` クラスで、<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> をインポートします。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. `GetClassifier()` メソッドで、`return` ステートメントの前に次のコードを追加します。

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. 次のアセンブリ参照をプロジェクトに追加します。

   - EnvDTE
   - Microsoft.VisualStudio.Shell.Framework

3. *DTETestProvider.cs* ファイルで、次の `using` ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. `DTETestProvider` クラスで、<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> をインポートします。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. `GetClassifier()` メソッドで、`return` ステートメントの前に次のコードを追加します。

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>関連項目

- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
- [DTE を使って Visual Studio を起動する](launch-visual-studio-dte.md)
