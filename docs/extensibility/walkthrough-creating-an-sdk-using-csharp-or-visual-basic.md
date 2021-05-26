---
title: 'チュートリアル: C# または Visual Basic を使用して SDK を作成する | Microsoft Docs'
description: このチュートリアルでは、Visual C# を使用して単純な Math Library SDK を作成してから、その SDK を Visual Studio 拡張機能としてパッケージ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 5b44566e4a8df323af6132128a8881b54c6f493f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217295"
---
# <a name="walkthrough-create-an-sdk-using-c-or-visual-basic"></a>チュートリアル: C# または Visual Basic を使用して SDK を作成する
このチュートリアルでは、Visual C# を使用して単純な Math Library SDK を作成してから、その SDK を Visual Studio 拡張機能 (VSIX) としてパッケージ化する方法について説明します。 以下の手順を完了することになります。

- [SimpleMath Windows ランタイム コンポーネントを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)

- [SimpleMathVSIX 拡張機能プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)
- [クラス ライブラリを使用するサンプル アプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-simplemath-windows-runtime-component"></a><a name="createClassLibrary"></a> SimpleMath Windows ランタイム コンポーネントを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートの一覧で **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows ストア]** ノードを選択してから、 **[Windows ランタイム コンポーネント]** テンプレートを選択します。

3. **[名前]** ボックスで「**SimpleMath**」と指定してから、 **[OK]** ボタンを選択します。

4. **ソリューション エクスプローラー** で **[SimpleMath]** プロジェクト ノードのショートカット メニューを開いてから、 **[プロパティ]** を選択します。

5. **Class1** という名前を **Arithmetic.cs** に変更し、次のコードと一致するようにそれを更新します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmath/arithmetic.cs" id="Snippet3":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmath/arithmetic.vb" id="Snippet3":::

6. **ソリューション エクスプローラー** で、**ソリューションの [SimpleMath]** ノードのショートカット メニューを開いてから、 **[構成マネージャー]** を選択します。

    **[構成マネージャー]** ダイアログ ボックスが表示されます。

7. **[アクティブ ソリューション構成]** 一覧の **[リリース]** をクリックします。

8. **[構成]** 列で、 **[SimpleMath]** 行が **[リリース]** に設定されていることを確認してから、 **[閉じる]** をクリックして変更を受け入れます。

   > [!IMPORTANT]
   > SimpleMath コンポーネントの SDK に含まれる構成は 1 つだけです。 この構成はリリース ビルドである必要があります。そうでないと、このコンポーネントを使用するアプリが [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)] の認定に合格しません。

9. **ソリューション エクスプローラー** で **[SimpleMath]** プロジェクト ノードのショートカット メニューを開いてから、 **[ビルド]** を選択します。

## <a name="to-create-the-simplemathvsix-extension-project"></a><a name="createVSIX"></a> SimpleMathVSIX 拡張機能プロジェクトを作成するには

1. **ソリューションの [SimpleMath]** ノードのショートカット メニューで、 **[追加]**  >  **[新しいプロジェクト]** を選択します。

2. テンプレートの一覧で **[Visual C#]** または **[Visual Basic]** を展開し、 **[機能拡張]** ノードを選択してから、 **[VSIX プロジェクト]** テンプレートを選択します。

3. **[名前]** ボックスで「**SimpleMathVSIX**」と指定してから、 **[OK]** ボタンを選択します。

4. **ソリューション エクスプローラー** で、 **[source.extension.vsixmanifest]** 項目を選択します。

5. メニュー バーで **[表示]**  >  **[コード]** の順に選択します。

6. 既存の XML を次の XML に置き換えます。

   ```xml
   <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
     <Metadata>
       <Identity Id="SimpleMath" Version="1.0" Language="en-US" Publisher="[YourName]" />
       <DisplayName>SimpleMath Library</DisplayName>
       <Description xml:space="preserve">Basic arithmetic operations in a WinRT-compatible library. Implemented in C#.</Description>
     </Metadata>
     <Installation Scope="Global" AllUsers="true">
       <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="SimpleMath" SdkVersion="1.0" />
     </Installation>
     <Prerequisites>
       <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[14.0,16.0]" />
     </Prerequisites>
     <Dependencies>
       <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="4.5" />
     </Dependencies>
     <Assets>
       <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
     </Assets>
   </PackageManifest>
   ```

7. **ソリューション エクスプローラー** で **[SimpleMathVSIX]** を選択します。

8. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

9. **[共通項目]** の一覧で、 **[データ]** を展開してから、 **[XML ファイル]** を選択します。

10. **[名前]** ボックスで「`SDKManifest.xml`」と指定してから、 **[追加]** ボタンを選択します。

11. **ソリューション エクスプローラー** で、`SDKManifest.xml` のショートカット メニューを開き、 **[プロパティ]** を選択します。次に、 **[VSIX に含める]** プロパティの値を **[True]** に変更します。

12. ファイルの内容を次の XML に置き換えます。

    **C#**

    ```xml
    <FileList
      DisplayName="WinRT Math Library (CS)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```

    **Visual Basic**

    ```xml
    <FileList
      DisplayName="WinRT Math Library (VB)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```

13. **ソリューション エクスプローラー** で、**SimpleMathVSIX** プロジェクトのショートカット メニューを開き、 **[追加]** を選択してから、 **[新しいフォルダー]** を選択します。

14. フォルダーの名前を `references` に変更します。

15. **[参照]** フォルダーのショートカット メニューを開き、 **[追加]** を選択してから、 **[新しいフォルダー]** を選択します。

16. サブフォルダーの名前を `commonconfiguration` に変更し、その中にサブフォルダーを作成して、そのサブフォルダーの名前を `neutral` にします。

17. 前の 4 つの手順を繰り返します。今度は、最初のフォルダーの名前を `redist` に変更します。

     これでプロジェクトに次のフォルダー構造が含まれるようになりました。

    ```xml
    references\commonconfiguration\neutral
    redist\commonconfiguration\neutral
    ```

18. **ソリューション エクスプローラー** で **[SimpleMath]** プロジェクトのショートカット メニューを開いてから、 **[エクスプローラーでフォルダーを開く]** を選択します。

19. **エクスプローラー** で *bin\Release* フォルダーに移動し、**SimpleMath.winmd** ファイルのショートカット メニューを開いてから、 **[コピー]** を選択します。

20. **ソリューション エクスプローラー** で、そのファイルを **SimpleMathVSIX** プロジェクトの *references\commonconfiguration\neutral* フォルダーに貼り付けます。

21. 前の手順を繰り返して、**SimpleMath.pri** ファイルを **SimpleMathVSIX** プロジェクトの *redist\commonconfiguration\neutral* フォルダーに貼り付けます。

22. **ソリューション エクスプローラー** で、 **[SimpleMath.winmd]** を選択します。

23. メニュー バーで、 **[表示]**  >  **[プロパティ]** を選択します (キーボード: **F4** キーを選択します)。

24. **[プロパティ]** ウィンドウで、 **[ビルド アクション]** プロパティを **[コンテンツ]** に変更してから、 **[VSIX に含める]** プロパティを **[True]** に変更します。

25. **ソリューション エクスプローラー** で、 **[SimpleMath.pri]** に対してこのプロセスを繰り返します。

26. **ソリューション エクスプローラー** で **[SimpleMathVSIX]** を選択します。

27. メニュー バーで、 **[ビルド]**  >  **[SimpleMathVSIX のビルド]** を選択します。

28. **ソリューション エクスプローラー** で **[SimpleMathVSIX]** プロジェクトのショートカット メニューを開いてから、 **[エクスプローラーでフォルダーを開く]** を選択します。

29. **エクスプローラー** で *\bin\Release* フォルダーに移動してから、*SimpleMathVSIX.vsix* を実行してそれをインストールします。

30. **[インストール]** ボタンをクリックし、インストールが完了するのを待ちます。次に、Visual Studio を再起動します。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a> クラス ライブラリを使用するサンプル アプリを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートの一覧で **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Windows ストア]** ノードを選択します。

3. **[空のアプリケーション]** テンプレートを選択し、プロジェクトに **ArithmeticUI** という名前を付けてから、 **[OK]** ボタンを選択します。

4. **ソリューション エクスプローラー** で、 **[ArithmeticUI]** プロジェクトのショートカット メニューを開いて、 **[追加]**  >  **[参照]** を選択します。

5. 参照の種類の一覧で、 **[Windows]** を展開してから、 **[拡張機能]** を選択します。

6. 詳細ペインで、 **[WinRT Math Library]** 拡張機能を選択します。

    SDK に関する追加の情報が表示されます。 このチュートリアルで前に SDKManifest.xml ファイルで指定したように、 **[詳細情報]** リンクを選択して https://msdn.microsoft.com/ を開くことができます。

7. **[参照マネージャー]** ダイアログ ボックスで **[WinRT Math Library]** チェック ボックスを選択してから、 **[OK]** ボタンを選択します。

8. メニュー バーで、 **[表示]**  >  **[オブジェクト ブラウザー]** を選択します。

9. **[参照]** の一覧で、 **[Simple Math]** を選択します。

     これで SDK の内容を確認できるようになりました。

10. **ソリューション エクスプローラー** で **[MainPage.xaml]** を開き、その内容を次の XAML に置き換えます。

    **C#**

    ```xml
    <Page
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```

    **Visual Basic**

    ```xml
    <Page
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```

11. 次のコードに一致するように **MainPage.xaml.cs** を更新します。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Windows.Foundation;
using Windows.Foundation.Collections;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Primitives;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238

namespace ArithmeticUI
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        public static string operation = null;

        public MainPage()
        {
            this.InitializeComponent();
        }

        /// <summary>
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.  The Parameter
        /// property is typically used to configure the page.</param>
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
        }

        /// <summary>
        /// Sets the operator chosen by the user
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void OnOperatorClick(object sender, RoutedEventArgs e)
        {
            operation = (sender as Button).Content.ToString();
        }

        /// <summary>
        /// Calls the SimpleMath SDK to do simple arithmetic
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void OnResultsClick(object sender, RoutedEventArgs e)
        {
            try
            {
                float firstNumber = float.Parse(this._firstNumber.Text);
                float secondNumber = float.Parse(this._secondNumber.Text);

                SimpleMath.Arithmetic math = new SimpleMath.Arithmetic();

                switch (operation)
                {
                    case "+":
                        this._result.Text = (math.add(firstNumber, secondNumber)).ToString();
                        break;
                    case "-":
                        this._result.Text = (math.subtract(firstNumber, secondNumber)).ToString();
                        break;
                    case "*":
                        this._result.Text = (math.multiply(firstNumber, secondNumber)).ToString();
                        break;
                    case "/":
                        this._result.Text = (math.divide(firstNumber, secondNumber)).ToString();
                        break;
                    default:
                        this._result.Text = "Choose operator";
                        break;
                }
            }
            catch
            {
                this._result.Text = "Enter valid #";
            }
        }
    }
}
```

```vb
' The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238

''' <summary>
''' An empty page that can be used on its own or navigated to within a Frame.
''' </summary>
Public NotInheritable Class MainPage
    Inherits Page

    ''' <summary>
    ''' Invoked when this page is about to be displayed in a Frame.
    ''' </summary>
    ''' <param name="e">Event data that describes how this page was reached.  The Parameter
    ''' property is typically used to configure the page.</param>
    Protected Overrides Sub OnNavigatedTo(e As Navigation.NavigationEventArgs)
    
    End Sub

    Public Shared operation As String = Nothing

    ''' <summary>
    ''' Sets the operator chosen by the user
    ''' </summary>
    ''' <param name="sender"></param>
    ''' <param name="e"></param>
    Private Sub OnOperatorClick(ByVal sender As Object, ByVal e As RoutedEventArgs)
        operation = If(TypeOf sender Is Button, CType(sender, Button), Nothing).Content.ToString()
    End Sub


    ''' <summary>
    ''' Calls the SimpleMath SDK to do simple arithmetic
    ''' </summary>
    ''' <param name="sender"></param>
    ''' <param name="e"></param>
    Private Sub OnResultsClick(ByVal sender As Object, ByVal e As RoutedEventArgs)

        Try

            Dim firstNumber As Single = Single.Parse(Me._firstNumber.Text)
            Dim secondNumber As Single = Single.Parse(Me._secondNumber.Text)

            Dim math As New SimpleMath.Arithmetic()

            Select Case (operation)

                Case "+"
                    Me._result.Text = (math.Add(firstNumber, secondNumber)).ToString()

                Case "-"
                    Me._result.Text = (math.Subtract(firstNumber, secondNumber)).ToString()
                Case "*"
                    Me._result.Text = (math.Multiply(firstNumber, secondNumber)).ToString()
                Case "/"
                    Me._result.Text = (math.Divide(firstNumber, secondNumber)).ToString()
                Case Else
                    Me._result.Text = "Choose operator"

            End Select

        Catch
            Me._result.Text = "Enter valid #"
        End Try
    End Sub
End Class
```

12. **F5** キーを押してアプリを実行します。

13. アプリで任意の 2 つの数値を入力し、操作を選択してから、 **[=]** ボタンを選択します。

     正しい結果が表示されます。

    拡張機能 SDK を正しく作成して使用しました。

## <a name="see-also"></a>関連項目
- [チュートリアル: C++ を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [チュートリアル: JavaScript を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-javascript.md)
- [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
