---
title: カスタム スタート ページの作成 | Microsoft Docs
description: カスタム スタート ページの作成方法を説明します。 空白のスタート ページから開始し、コントロールを空の UserControl 要素に追加して、ページをテストします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: f76451ca2a650283125cc7659d0053ef984115fc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089382"
---
# <a name="creating-a-custom-start-page"></a>カスタム スタート ページの作成

このドキュメントの手順に従って、カスタム スタート ページを作成できます。

## <a name="create-a-blank-start-page"></a>空白のスタート ページを作成する

最初に、Visual Studio が認識するタグ構造を持つ *.xaml* ファイルを作成して、空のスタート ページを作成します。 次に、マークアップと分離コードを追加して、必要な外観と機能を生成します。

1. **WPF アプリケーション** の種類の新しいプロジェクトを作成します ( **[Visual C#]**  >  **[Windows デスクトップ]** )。

2. `Microsoft.VisualStudio.Shell.14.0` への参照を追加します。

3. XML エディターで XAML ファイルを開き、名前空間宣言を削除せずに最上位の \<Window> 要素を \<UserControl> 要素に変更します。

4. 最上位の要素から `x:Class` 宣言を削除します。 これにより、スタート ページをホストする Visual Studio ツール ウィンドウと XAML コンテンツとの互換性が確保されます。

5. 最上位の \<UserControl> 要素に次の名前空間宣言を追加します。

    ```vb
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
    ```

     これらの名前空間を使用すると、Visual Studio のコマンド、コントロール、UI 設定にアクセスできます。 詳細については、「[スタート ページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)」を参照してください。

     次の例では、空のスタート ページの *.xaml* ファイルのマークアップを示します。 カスタム コンテンツは、内側の <xref:System.Windows.Controls.Grid> 要素に含まれている必要があります。

    ```vb
    <UserControl
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:MyNamespace="clr-namespace:ManualStartPage;assembly=ManualStartPage"
        xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
                xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
        xmlns:local="clr-namespace:StartPageHost"
        mc:Ignorable="d"
         Height="350" Width="525">
        <Grid>
        <!--Add content here.-->
        </Grid>
    </UserControl>
    ```

6. 空の \<UserControl> 要素にコントロールを追加して、カスタム スタート ページに入力します。 Visual Studio に固有の機能を追加する方法の詳細については、「[スタート ページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)」を参照してください。

## <a name="test-and-apply-the-custom-start-page"></a>カスタム スタート ページのテストと適用

Visual Studio がクラッシュしないことを確認するまでは、Visual Studio のプライマリ インスタンスを設定してカスタム スタート ページを実行しないでください。 代わりに、実験用インスタンスでテストします。

### <a name="to-test-a-manually-created-custom-start-page"></a>手動で作成されたカスタム スタート ページをテストするには

1. XAML ファイルと、サポートするテキスト ファイルまたはマークアップ ファイルを *%USERPROFILE%\My Documents\Visual Studio 2015\StartPages\\* フォルダーにコピーします。

2. スタート ページで、Visual Studio によってインストールされていないアセンブリ内のコントロールまたは型が参照されている場合は、そのアセンブリをコピーし、 *{Visual Studio のインストール フォルダー}\Common7\IDE\PrivateAssemblies\\* に貼り付けます。

3. Visual Studio のコマンド プロンプトで「**devenv /rootsuffix Exp**」と入力して、Visual Studio の実験用インスタンスを開きます。

4. 実験用インスタンスで、 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[スタートアップ]** ページにアクセスし、 **[スタート ページのカスタマイズ]** ドロップダウンから XAML ファイルを選択します。

5. **[表示]** メニューの **[スタート ページ]** をクリックします。

     カスタム スタート ページが表示されます。 ファイルを変更する場合は、実験用インスタンスを閉じて変更を加え、変更されたファイルをコピーして貼り付けてから、実験用インスタンスを再度開いて変更内容を表示する必要があります。

### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>Visual Studio のプライマリ インスタンスにカスタム スタート ページを適用するには

- スタート ページをテストし、安定していることがわかったら、 **[オプション]** ダイアログ ボックスの **[スタート ページのカスタマイズ]** オプションを使用して、Visual Studio のプライマリ インスタンスのスタート ページとして選択します。

## <a name="see-also"></a>関連項目

- [チュートリアル: カスタム XAML をスタート ページに追加する](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
- [スタート ページにユーザー コントロールを追加する](../extensibility/adding-user-control-to-the-start-page.md)
- [スタート ページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
- [チュートリアル: スタート ページのユーザー設定の保存](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)
- [カスタム スタート ページを配置する](../extensibility/deploying-custom-start-pages.md)
