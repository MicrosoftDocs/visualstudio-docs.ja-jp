---
title: VSPackage を使用した拡張機能の作成 | Microsoft Docs
description: メッセージ ボックスを表示するために、VSIX プロジェクトを作成し、VSPackage を使用して VSPackage プロジェクト項目を追加し、UI シェル サービスを取得する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a6c93d90771eeffbfe28ae91781403019743afa9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089148"
---
# <a name="create-an-extension-with-a-vspackage"></a>VSPackage を使用した拡張機能の作成

このチュートリアルでは、VSIX プロジェクトを作成し、VSPackage プロジェクト項目を追加する方法について説明します。 メッセージ ボックスを表示するために、VSPackage を使用して UI シェル サービスを取得します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-vspackage"></a>VSPackage を作成する

1. **FirstPackage** という名前の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. プロジェクトが開いたら、**FirstPackage** という名前の Visual Studio パッケージ項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[機能拡張]** の順にアクセスし、 **[Visual Studio パッケージ]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *FirstPackage.cs* に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

    Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、「[実験用インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

4. 実験用インスタンスで、 **[ツール]**  >  **[拡張機能と更新プログラム]** ウィンドウを開きます。 **FirstPackage** 拡張機能がここに表示されます (Visual Studio の作業インスタンスで **[拡張機能と更新プログラム]** を開いた場合、**FirstPackage** は表示されません)。

## <a name="load-the-vspackage"></a>VSPackage を読み込む

この時点では、読み込む理由となるものがないため、拡張機能は読み込まれません。 通常、拡張機能を読み込むには、UI を操作する (メニュー コマンドをクリックするか、ツール ウィンドウを開く) か、または VSPackage が特定の UI コンテキストで読み込まれるように指定します。 VSPackage と UI コンテキストの読み込みの詳細については、[VSPackage の読み込み](../extensibility/loading-vspackages.md)に関するページを参照してください。 この手順では、ソリューションを開くときに VSPackage を読み込む方法について説明します。

1. *FirstPackage.cs* ファイルを開きます。 `FirstPackage` クラスの宣言を探します。 既存の属性を次の属性に置き換えます。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid(FirstPackage.PackageGuidString)]
    public sealed class FirstPackage : Package
    ```

2. VSPackage が読み込まれたことを知らせるメッセージを追加してみましょう。 VSPackage が配置されないと Visual Studio サービスを取得できないため、VSPackage の `Initialize()` メソッドを使用します (サービスの取得の詳細については、「[方法: サービスを取得する](../extensibility/how-to-get-a-service.md)」を参照してください)。`FirstPackage` の `Initialize()` メソッドを、<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> サービスを取得し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスを取得して、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A> メソッドを呼び出すコードに置き換えます。

    ```csharp
    protected override void Initialize()
    {
        base.Initialize();

        IVsUIShell uiShell = (IVsUIShell)GetService(typeof(SVsUIShell));
        Guid clsid = Guid.Empty;
        int result;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(uiShell.ShowMessageBox(
            0,
            ref clsid,
            "FirstPackage",
             string.Format(CultureInfo.CurrentCulture, "Inside {0}.Initialize()", this.GetType().FullName),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result));
    }
    ```

3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

4. 実験用インスタンスでソリューションを開きます。 「**First Package Inside Initialize()** 」というメッセージ ボックスが表示されます。
