---
title: WPF ツールボックス コントロールを作成する | Microsoft Docs
description: WPF ツールボックス コントロール テンプレートを使用して、他のユーザーに配布できるツールボックス コントロールを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- toolbox control
- toolbox
- wpf
ms.assetid: 9cc34db9-b0d1-4951-a02f-7537fbbb51ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1dccdeb09a938b3b0bbbab803faeed538001b825
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089252"
---
# <a name="create-a-wpf-toolbox-control"></a>WPF ツールボックス コントロールを作成する

WPF (Windows Presentation Framework) ツールボックス コントロール テンプレートを使用すると、拡張機能のインストール時に自動的に **ツールボックス** に追加される WPF コントロールを作成できます。 このチュートリアルでは、テンプレートを使用して、他のユーザーに配布できる **ツールボックス** コントロールを作成する方法について説明します。

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-toolbox-control"></a>ツールボックス コントロールを作成する

### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>WPF ツールボックス コントロールを使用して拡張機能を作成する

1. `MyToolboxControl` という名前の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. プロジェクトが開いたら、`MyToolboxControl` という名前の **WPF ツールボックス コントロール** 項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[拡張性]** に移動して、 **[WPF ツールボックス コントロール]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *MyToolboxControl.cs* に変更します。

    ソリューションには、**ツールボックス** にコントロールを追加し、デプロイ用の VSIX マニフェストに **Microsoft.VisualStudio.ToolboxControl** アセット エントリを追加するユーザー コントロール `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> が含まれるようになりました。

#### <a name="to-create-the-control-ui"></a>コントロール UI を作成するには

1. デザイナーで *MyToolboxControl.xaml* を開きます。

    デザイナーに、<xref:System.Windows.Controls.Button> コントロールを含む <xref:System.Windows.Controls.Grid> コントロールが表示されます。

2. グリッド レイアウトを配置します。 <xref:System.Windows.Controls.Grid> コントロールを選択すると、グリッドの上端と左端に青色のコントロール バーが表示されます。 グリッドに行と列を追加するには、バーをクリックします。

3. グリッドに子コントロールを追加します。 子コントロールは、**ツールボックス** からグリッドのセクションにドラッグするか、XAML で `Grid.Row` および `Grid.Column` 属性を設定することによって配置できます。 次の例では、グリッドの一番上の行に 2 つのラベルを追加し、2 番目の行にボタンを追加します。

    ```xaml
    <Grid>
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />
    </Grid>
    ```

## <a name="renaming-the-control"></a>コントロールの名前を変更する

 既定では、コントロールは、**MyToolboxControl.MyToolboxControl** という名前のグループの **MyToolboxControl** として **ツールボックス** に表示されます。 これらの名前は *MyToolboxControl.xaml.cs* ファイルで変更できます。

1. コード ビューで *MyToolboxControl.xaml.cs* を開きます。

2. `MyToolboxControl` クラスを見つけて、その名前を TestControl に変更します。 (これを行う最も早い方法は、クラスの名前を変更し、コンテキスト メニューから **[名前の変更]** を選択して、手順を完了することです。 ( **[名前の変更]** コマンドの詳細については、[名前の変更のリファクタリング (C#)](../ide/reference/rename.md) に関する記事を参照してください。)

3. `ProvideToolboxControl` 属性に移動し、最初のパラメーターの値を「**Test**」に変更します。 これは、**ツールボックス** のコントロールを含むグループの名前です。

    結果のコードは次のようになります。

    ```csharp
    [ProvideToolboxControl("Test", true)]
    public partial class TestControl : UserControl
    {
        public TestControl()
        {
            InitializeComponent();
        }
    }
    ```

## <a name="build-test-and-deployment"></a>ビルド、テスト、デプロイ

 プロジェクトをデバッグするときに、Visual Studio の実験用インスタンスの **ツールボックス** にコントロールがインストールされている必要があります。

### <a name="to-build-and-test-the-control"></a>コントロールをビルドおよびテストするには

1. プロジェクトをリビルドし、デバッグを開始します。

2. Visual Studio の新しいインスタンスで、WPF アプリケーション プロジェクトを作成します。 XAML デザイナーが開いていることを確認します。

3. **[ツールボックス]** で対象のコントロールを見つけて、デザイン画面にドラッグします。

4. WPF アプリケーションのデバッグを開始します。

5. コントロールが表示されることを確認します。

### <a name="to-deploy-the-control"></a>コントロールを配置するには

1. テストされたプロジェクトをビルドすると、プロジェクトの *\bin\debug\* フォルダーで *.vsix* ファイルを見つけることができます。

2. *.vsix* ファイルをダブルクリックし、インストール手順に従うことによって、ローカル コンピューターにそれをインストールすることができます。 コントロールをアンインストールするには、 **[ツール]**  >  **[拡張機能と更新プログラム]** に移動し、コントロールの拡張機能を見つけて、 **[アンインストール]** をクリックします。

3. *.vsix* ファイルをネットワークまたは Web サイトにアップロードします。

    ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードした場合、他のユーザーは Visual Studio の **[ツール]**  >  **[拡張機能と更新プログラム]** を使用し、コントロールをオンラインで見つけてインストールすることができます。
