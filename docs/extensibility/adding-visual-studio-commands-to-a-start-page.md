---
title: Visual Studio コマンドのスタート ページへの追加 | Microsoft Docs
description: Visual Studio のコマンドを、Visual Studio のカスタム スタート ページの XAML オブジェクトにバインドするさまざまな方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 4e2ec238d3cb8c2e7d843018fc45e97207c6d5f4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097527"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>スタート ページに Visual Studio コマンドを追加する

カスタム スタート ページを作成するときには、そこに Visual Studio のコマンドを追加できます。 このドキュメントでは、スタート ページの XAML オブジェクトに Visual Studio コマンドをバインドするさまざまな方法について説明します。

XAML のコマンドの詳細については、「[コマンド実行の概要](/dotnet/framework/wpf/advanced/commanding-overview)」を参照してください。

## <a name="add-commands-from-the-command-well"></a>コマンド ウェルからコマンドを追加する

[カスタム スタート ページの作成](../extensibility/creating-a-custom-start-page.md)に関するページで作成したスタート ページには、次のように、<xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> 名前空間と <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> 名前空間が追加されています。

```xml
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

アセンブリ *Microsoft.VisualStudio.Shell.Immutable.11.0.dll* から、Microsoft.VisualStudio.Shell のための別の名前空間を追加します。 (このアセンブリへの参照をプロジェクトに追加する必要が生じる場合があります。)

```xml
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"
```

`vscom:` エイリアスを使用して、コントロールの <xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A> プロパティを `vscom:VSCommands.ExecuteCommand` に設定すると、Visual Studio のコマンドをページ上の XAML コントロールにバインドできます。 その後、次の例に示すように、<xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A> プロパティを、実行するコマンドの名前に設定できます。

```xml
<Button Name="btnNewProj" Content="New Project"
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
    CommandParameter="File.NewProject" >
</Button>
```

> [!NOTE]
> すべてのコマンドの先頭に、XAML スキーマを参照する `x:` エイリアスが必要です。

 `Command` プロパティの値は、**コマンド** ウィンドウからアクセスできる任意のコマンドに設定できます。 使用可能なコマンドの一覧については、「[Visual Studio コマンドのエイリアス](../ide/reference/visual-studio-command-aliases.md)」を参照してください。

 追加するコマンドに追加のパラメーターが必要な場合は、それを `CommandParameter` プロパティの値に追加できます。 次の例に示すように、スペースを使用してコマンドとパラメーターを分けます。

```xml
<Button Content="Web Search"
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"
        CommandParameter="View.WebBrowser www.bing.com" />
```

### <a name="call-extensions-from-the-command-well"></a>コマンド ウェルから拡張機能を呼び出す
 他の Visual Studio コマンドを呼び出すために使用されるのと同じ構文を使用して、登録されている VSPackage からコマンドを呼び出すことができます。 たとえば、インストールされている VSPackage によって、 **[表示]** メニューに **[ホーム ページ]** コマンドを追加する場合、`CommandParameter` を `View.HomePage` に設定することで、そのコマンドを呼び出せます。

> [!NOTE]
> VSPackage に関連付けられているコマンドを呼び出す場合は、コマンドが呼び出されるときにそのパッケージを読み込む必要があります。

## <a name="add-commands-from-assemblies"></a>アセンブリからコマンドを追加する
 アセンブリからコマンドを呼び出したり、メニュー コマンドに関連付けられていない VSPackage 内のコードにアクセスしたりするには、アセンブリのエイリアスを作成し、そのエイリアスを呼び出す必要があります。

### <a name="to-call-a-command-from-an-assembly"></a>アセンブリからコマンドを呼び出すには

1. ソリューション内に、アセンブリへの参照を追加します。

2. 次の例に示すように、*StartPage.xaml* ファイルの先頭に、そのアセンブリの名前空間ディレクティブを追加します。

    ```xml
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
    ```

3. 次の例に示すように、XAML オブジェクトの `Command` プロパティを設定してコマンドを呼び出します。

     Xaml

    ```
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>
    ```

> [!NOTE]
> アセンブリをコピーし、*..\\{Visual Studio インストール フォルダー}\Common7\IDE\PrivateAssemblies\* に貼り付けて、呼び出される前に確実に読み込まれるようにする必要があります。

## <a name="add-commands-with-the-dte-object"></a>DTE オブジェクトを使用してコマンドを追加する
 マークアップ内とコード内のどちらでも、開始ページの DTE オブジェクトにアクセスできます。

 マークアップ内では、[バインドのマークアップ拡張機能](/dotnet/framework/wpf/advanced/binding-markup-extension)の構文を使用して <xref:EnvDTE.DTE> オブジェクトを呼び出すことで、それにアクセスできます。 この方法は、コレクションを返すような単純なプロパティにバインドするためには使用できますが、メソッドやサービスへのバインドはできません。 次の例は、<xref:EnvDTE._DTE.Name%2A> プロパティにバインドされる <xref:System.Windows.Controls.TextBlock> コントロールと、<xref:EnvDTE._DTE.Windows%2A> プロパティによって返されるコレクションの <xref:EnvDTE.Window.Caption%2A> プロパティを列挙する <xref:System.Windows.Controls.ListBox> コントロールを示しています。

```xml
<TextBlock Text="{Binding Path=DTE.Name}" FontSize="12" HorizontalAlignment="Center"/>
<ListBox ItemsSource="{Binding Path=DTE.Windows}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding Path=Caption}"/>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox
```

 例については、「[チュートリアル: スタート ページのユーザー設定の保存](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [スタート ページへのユーザー コントロールの追加](../extensibility/adding-user-control-to-the-start-page.md)
