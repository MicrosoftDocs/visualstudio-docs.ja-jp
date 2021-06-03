---
title: 'チュートリアル: スタート ページのユーザー設定の保存 | Microsoft Docs'
description: このチュートリアルでは、レジストリに設定を保存して、スタート ページのユーザー設定を永続化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 2f7dddfca06d7bc475286c73087828305464daa5
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217217"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>チュートリアル: スタート ページのユーザー設定を保存する

スタートページのユーザー設定を永続化できます。 このチュートリアルを進めていくと、ユーザーがボタンをクリックしたときにレジストリに設定を保存し、その後、スタート ページが読み込まれるたびにその設定を取得するコントロールを作成できます。 スタート ページ プロジェクト テンプレートには、カスタマイズ可能なユーザー コントロールが含まれており、既定のスタート ページ XAML でそのコントールが呼び出されるので、スタート ページ自体を変更する必要はありません。

このチュートリアルでインスタンス化される設定ストアは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore> インターフェイスのインスタンスであり、呼び出されると、次のレジストリの場所で読み取りと書き込みが行われます: **HKCU\Software\Microsoft\VisualStudio\14.0\\\<CollectionName>**

Visual Studio の実験用インスタンスで実行している場合は、設定ストアの読み取りと書き込みは **HKCU\Software\Microsoft\VisualStudio\14.0Exp\\\<CollectionName> で行われます。**

設定の永続化方法の詳細については、「[ユーザー設定とオプションを拡張する](../extensibility/extending-user-settings-and-options.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

> [!NOTE]
> このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。
>
> スタート ページ プロジェクト テンプレートは、**拡張機能マネージャー** を使用してダウンロードできます。

## <a name="set-up-the-project"></a>プロジェクトのセットアップ

1. 「[カスタム スタート ページの作成](creating-a-custom-start-page.md)」の説明に従って、スタート ページ プロジェクトを作成します。 プロジェクトに **SaveMySettings** という名前を付けます。

2. **ソリューション エクスプローラー** で、次のアセンブリ参照を StartPageControl プロジェクトに追加します。

    - EnvDTE

    - EnvDTE80

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.Shell.Interop.11.0

3. *MyControl.xaml* を開きます。

4. XAML ペインの最上位の <xref:System.Windows.Controls.UserControl> 要素定義で、名前空間の宣言の後に、次のイベント宣言を追加します。

    ```xml
    Loaded="OnLoaded"
    ```

5. デザイン ペインで、コントロールのメイン領域をクリックし、**Delete** キーを押します。

     この手順では、<xref:System.Windows.Controls.Border> 要素とその中のすべてが削除され、最上位の <xref:System.Windows.Controls.Grid> 要素だけが残されます。

6. **[ツールボックス]** から、<xref:System.Windows.Controls.StackPanel> コントロールをグリッドにドラッグします。

7. ここで、<xref:System.Windows.Controls.TextBlock>、<xref:System.Windows.Controls.TextBox>、ボタンを <xref:System.Windows.Controls.StackPanel> にドラッグします。

8. 次の例に示すように、<xref:System.Windows.Controls.TextBox> には **x:Name** 属性を、<xref:System.Windows.Controls.Button> には `Click` イベントを追加します。

    ```xml
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />
        <Button Click="Button_Click" Width="100">Save My Setting</Button>
    </StackPanel>
    ```

## <a name="implement-the-user-control"></a>ユーザー コントロールを実装する

1. XAML ペインで、<xref:System.Windows.Controls.Button> 要素の `Click` 属性を右クリックし、 **[イベント ハンドラーへ移動]** をクリックします。

     この手順では、*MyControl.xaml.cs* を開き、`Button_Click` イベントのスタブ ハンドラーを作成します。

2. 次の `using` ディレクティブをファイルの先頭に追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/startpagedte/cs/startpagecontrol/mycontrol.xaml.cs" id="Snippet11":::

3. 次の例で示すように、プライベート `SettingsStore` プロパティを追加します。

    ```csharp
    private IVsWritableSettingsStore _settingsStore = null;
    private IVsWritableSettingsStore SettingsStore
    {
        get
        {
            if (_settingsStore == null)
            {
                // Get a reference to the DTE from the DataContext.
                var typeDescriptor = DataContext as ICustomTypeDescriptor;
                var propertyCollection = typeDescriptor.GetProperties();
                var dte = propertyCollection.Find("DTE", false).GetValue(
                    DataContext) as DTE2;

                // Get the settings manager from the DTE.
                var serviceProvider = new ServiceProvider(
                    (Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
                var settingsManager = serviceProvider.GetService(
                    typeof(SVsSettingsManager)) as IVsSettingsManager;

                // Write the user settings to _settingsStore.
                settingsManager.GetWritableSettingsStore(
                    (uint)__VsSettingsScope.SettingsScope_UserSettings,
                    out _settingsStore);
            }
            return _settingsStore;
        }
    }
    ```

     このプロパティは、まず、オートメーション オブジェクト モデルを含む <xref:EnvDTE80.DTE2> インターフェイスへの参照をユーザー コントロールの <xref:System.Windows.FrameworkElement.DataContext%2A> から取得し、次に DTE を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> インターフェイスのインスタンスを取得します。 次に、そのインスタンスを使用して、現在のユーザー設定を返します。

4. 次のように `Button_Click` イベントを入力します。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {
        int exists = 0;
        SettingsStore.CollectionExists("MySettings", out exists);
        if (exists != 1)
        {
            SettingsStore.CreateCollection("MySettings");
        }
        SettingsStore.SetString("MySettings", "MySetting", txtblk.Text);
    }
    ```

     これにより、テキスト ボックスの内容が、レジストリの "Mysetting" コレクションの "MySetting" フィールドに書き込まれます。 コレクションが存在しない場合は、作成されます。

5. ユーザー コントロールの `OnLoaded` イベントに対して、次のハンドラーを追加します。

    ```csharp
    private void OnLoaded(Object sender, RoutedEventArgs e)
    {
        string value;
        SettingsStore.GetStringOrDefault(
            "MySettings", "MySetting", "", out value);
        txtblk.Text = value;
    }
    ```

     このコードにより、テキスト ボックスのテキストが "MySetting" の現在の値に設定されます。

6. ユーザー コントロールをビルドします。

7. **ソリューション エクスプローラー** で、*source.extension.vsixmanifest* を開きます。

8. マニフェスト エディターで、 **[製品名]** を **[個人用設定スタート ページの保存]** に設定します。

     この機能は、スタート ページの名前を、 **[オプション]** ダイアログ ボックスの **[スタート ページのカスタマイズ]** ボックスの一覧で表示されるとおりに設定します。

9. *StartPage.xaml* をビルドします。

## <a name="test-the-control"></a>コントロールをテストする

1. **F5** キーを押します。

     Visual Studio の実験用インスタンスが開きます。

2. 実験用インスタンスで、 **[ツール]** メニューの **[オプション]** をクリックします。

3. **[環境]** ノードで、 **[スタートアップ]** をクリックし、 **[スタート ページのカスタマイズ]** ボックスの一覧の **[[インストールされた拡張機能] 個人用設定スタート ページの保存]** を選択します。

     **[OK]** をクリックします。

4. スタート ページが開いている場合は閉じて、 **[表示]** メニューで **[スタート ページ]** をクリックします。

5. スタート ページで、 **[MyControl]** タブをクリックします。

6. テキスト ボックスに「**Cat**」と入力し、 **[個人用設定の保存]** をクリックします。

7. スタート ページを閉じてから、もう一度開きます。

     テキスト ボックスに "Cat" という語が表示されるはずです。

8. "Cat" という語を "Dog" という語に置き換えます。 ボタンはクリックしないでください。

9. スタート ページを閉じてから、もう一度開きます。

     設定を保存しなかった場合でも、テキスト ボックスに "Dog" という語が表示されるはずですが、ツール ウィンドウが閉じられた場合でも、Visual Studio 自体が閉じられるまでは、ツール ウィンドウがメモリに保持されるためです。

10. Visual Studio の実験用インスタンスを終了します。

11. **F5** キーを押して、実験用インスタンスを再び開きます。

12. テキスト ボックスに "Cat" という語が表示されるはずです。

## <a name="next-steps"></a>次のステップ

さまざまなイベント ハンドラーの異なる値を使用して `SettingsStore` プロパティを取得し設定して、任意の数のカスタム設定を保存および取得するように、このユーザー コントロールを変更できます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A> の呼び出しごとに異なる `propertyName` パラメーターを使用している限り、レジストリ内で値が相互に上書きされることはありません。

## <a name="see-also"></a>関連項目

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [Visual Studio コマンドのスタート ページへの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
