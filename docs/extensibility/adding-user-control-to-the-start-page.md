---
title: スタート ページへのユーザー コントロールの追加 | Microsoft Docs
description: Visual Studio のスタート ページに Windows Presentation Foundation (WPF) ユーザー コントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- start page dll
- custom start page
- start page assembly
ms.assetid: 5b7997db-af6f-4fa9-a128-bceb42bddaf1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 1e5305927ceb634c64e52bb64ce57197f1b6be4c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097605"
---
# <a name="add-user-control-to-the-start-page"></a>スタート ページにユーザー コントロールを追加する

このチュートリアルでは、DLL 参照をカスタムのスタート ページに追加する方法について説明します。 この例では、ソリューションにユーザー コントロールを追加し、ユーザー コントロールをビルドしてから、ビルドされたアセンブリをスタート ページの *.xaml* ファイルから参照します。 新しいタブには、基本的な Web ブラウザーとして機能するユーザー コントロールがホストされます。

同じプロセスを使用して、 *.xaml* ファイルから呼び出すことができるアセンブリを追加できます。

## <a name="add-a-wpf-user-control-to-the-solution"></a>ソリューションに WPF ユーザー コントロールを追加する

まず、Windows Presentation Foundation (WPF) ユーザー コントロールをスタート ページ ソリューションに追加します。

1. [カスタムのスタート ページの作成](../extensibility/creating-a-custom-start-page.md)に関するページで作成したものを使用してスタート ページを作成します。

2. **ソリューション エクスプローラー** で該当ソリューションを右クリックして **[追加]** をクリックし、 **[新しいプロジェクト]** をクリックします。

3. **[新しいプロジェクト]** ダイアログ ボックスの左側のペインで、**Visual Basic** または **Visual C#** のいずれかのノードを展開し、 **[Windows]** をクリックします。 中央のペインで、 **[WPF ユーザー コントロール ライブラリ]** を選択します。

4. コントロールに `WebUserControl` という名前を付け、 **[OK]** をクリックします。

## <a name="implement-the-user-control"></a>ユーザー コントロールを実装する

WPF ユーザー コントロールを実装するには、XAML でユーザー インターフェイス (UI) を構築してから、コードビハインド イベントを C# または別の .NET 言語で記述します。

### <a name="to-write-the-xaml-for-the-user-control"></a>ユーザー コントロールの XAML を記述するには

1. ユーザー コントロールの XAML ファイルを開きます。 `<Grid>` 要素で、次の行定義をコントロールに追加します。

    ```vb
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    ```

2. メインの `<Grid>` 要素に次の新しい `<Grid>` 要素を追加します。これには、Web アドレスを入力するためのテキスト ボックスと、新しいアドレスを設定するためのボタンが含まれています。

    ```xml
    <Grid Grid.Row="0">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <TextBox x:Name="UserSource" Grid.Column="0" />
        <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
    </Grid>
    ```

3. ボタンとテキストボックスを含む `<Grid>` 要素の直後にある最上位の `<Grid>` 要素に次のフレームを追加します。

    ```vb
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
    ```

4. ユーザー コントロールの完成した XAML を次の例に示します。

    ```xml
    <UserControl x:Class="WebUserControl.UserControl1"
                 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
                 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
                 mc:Ignorable="d"
                 d:DesignHeight="300" d:DesignWidth="300">
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*" />
            </Grid.RowDefinitions>
            <Grid Grid.Row="0">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <TextBox x:Name="UserSource" Grid.Column="0" />
                <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
            </Grid>
            <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
        </Grid>
    </UserControl>

    ```

### <a name="to-write-the-code-behind-events-for-the-user-control"></a>ユーザー コントロールのコードビハインド イベントを記述するには

1. XAML デザイナーで、コントロールに追加した **[Set Address]\(アドレスの設定\)** ボタンをダブルクリックします。

    コード エディターで *UserControl1.cs* ファイルが開きます。

2. 次のように SetButton_Click イベント ハンドラーに入力します。

    ```csharp
    private void SetButton_Click(object sender, RoutedEventArgs e)
    {
        try
        {
            this.WebFrame.Source = new Uri(this.UserSource.Text, UriKind.Absolute);
        }
        catch (Exception error)
        {
            MessageBox.Show(error.Message);
        }
    }
    ```

    このコードにより、テキスト ボックスに入力された Web アドレスが Web ブラウザーのターゲットとして設定されます。 アドレスが有効でない場合、コードにより、エラーがスローされます。

3. WebFrame_Navigated イベントも処理する必要があります。

    ```csharp
    private void WebFrame_Navigated(object sender, EventArgs e)
    { }
    ```

4. ソリューションをビルドします。

## <a name="add-the-user-control-to-the-start-page"></a>スタート ページにユーザー コントロールを追加する

このコントロールをスタート ページ プロジェクトで使用できるようにするには、スタート ページ プロジェクト ファイルに、新しいコントロール ライブラリへの参照を追加します。 これで、コントロールをスタート ページの XAML マークアップに追加できるようになります。

1. **ソリューション エクスプローラー** で、スタート ページ プロジェクトの **[参照]** を右クリックし、 **[参照の追加]** をクリックします。

2. **[プロジェクト]** タブで **[WebUserControl]** を選択し、 **[OK]** をクリックします。

3. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

    ソリューションをビルドすると、ソリューション内の他のファイルのユーザー コントロールを IntelliSense で使用できるようになります。

    コントロールをスタート ページの XAML マークアップに追加するには、アセンブリに名前空間参照を追加してから、コントロールをページに配置します。

### <a name="to-add-the-control-to-the-markup"></a>コントロールをマークアップに追加するには

1. **ソリューション エクスプローラー** でスタート ページの *.xaml* ファイルを開きます。

2. **[XAML]** ペインで、次の名前空間宣言を最上位の <xref:System.Windows.Controls.Grid> 要素に追加します。

   ```xml
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
   ```

3. **[XAML]** ペインで、\<Grid> セクションまでスクロールします。

    このセクションには、<xref:System.Windows.Controls.Grid> 要素に <xref:System.Windows.Controls.TabControl> 要素が含まれています。

4. ユーザー コントロールへの参照を含む \<TabItem> を含む \<TabControl> 要素を追加します。

    ```xml

    <TabItem Header="Web" Height="Auto">
        <vsc:UserControl1 />
    </TabItem>

    ```

    これで、コントロールをテストできるようになりました。

## <a name="test-a-manually-created-custom-start-page"></a>手動で作成されたカスタム スタート ページをテストする

1. XAML ファイルと、すべてのサポートするテキスト ファイルまたはマークアップ ファイルを *%USERPROFILE%\My Documents\Visual Studio 2015\StartPages\\* フォルダーにコピーします。

2. スタート ページで、Visual Studio によってインストールされていないアセンブリ内のコントロールまたは型が参照されている場合は、そのアセンブリをコピーし、 _<Visual Studio のインストール フォルダー>_ **\Common7\IDE\PrivateAssemblies\\** に貼り付けます。

3. Visual Studio のコマンド プロンプトで「**devenv /rootsuffix Exp**」と入力して、Visual Studio の実験用インスタンスを開きます。

4. 実験用インスタンスで、 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[スタートアップ]** ページにアクセスし、 **[スタート ページのカスタマイズ]** ドロップダウンから XAML ファイルを選択します。

5. **[表示]** メニューの **[スタート ページ]** をクリックします。

    カスタム スタート ページが表示されます。 ファイルを変更する場合は、実験用インスタンスを閉じて変更を加え、変更されたファイルをコピーして貼り付けてから、実験用インスタンスを再度開いて変更内容を表示する必要があります。

## <a name="see-also"></a>こちらもご覧ください

- [WPF コンテナー コントロール](/previous-versions/bb675291(v=vs.110))
- [チュートリアル: カスタム XAML をスタート ページに追加する](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)