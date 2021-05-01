---
title: Visual Studio の XAML デザイナーでデザイン時のデータを使用する
description: XAML でデザイン時のデータを使用する方法について説明します。
ms.date: 11/17/2020
ms.topic: overview
author: alihamie
ms.author: tglee
manager: jmartens
monikerRange: vs-2019
ms.openlocfilehash: 915fe38da63f0b3994a809b20515fdc18e0790ce
ms.sourcegitcommit: 5fb684ff8729eb118aa91ce9f049c79eeb9747b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2021
ms.locfileid: "107913073"
---
# <a name="use-design-time-data-with-the-xaml-designer-in-visual-studio"></a>Visual Studio の XAML デザイナーでデザイン時のデータを使用する

一部のレイアウトでは、データなしで視覚化するのが困難です。 このドキュメントでは、デスクトップ プロジェクトで作業している開発者が XAML デザイナーでデータをモック化するために使用できる方法の 1 つを確認します。 この方法は、既存の無視が可能な “d:” 名前空間を使用して行います。 この方法によって、完全なモックのビュー モデルを作成する必要なく、デザイン時のデータをページまたはコントロールにすばやく追加できます。また、この変更によるリリース ビルドへの影響を心配することなく、プロパティの変更がアプリケーションに与える影響をテストすることもできます。 すべての d: データは XAML デザイナーでのみ使用され、無視が可能な名前空間の値がアプリケーションにコンパイルされることはありません。

> [!NOTE]
> Xamarin.Forms を使用している場合は、[Xamarin.Forms のデザイン時のデータ](/xamarin/xamarin-forms/xaml/xaml-previewer/design-time-data)に関する記事を参照してください。

## <a name="design-time-data-basics"></a>デザイン時のデータの基本

デザイン時のデータは、XAML デザイナーでのコントロールの視覚化を容易にするために設定するモック データです。 開始するには、次のコード行を XAML ドキュメントのヘッダーに追加します (まだ存在していない場合)。

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

名前空間を追加した後は、`d:` が実行時以外の XAML デザイナーにのみ表示されるように、これを属性またはコントロールの前に配置することができます。

たとえば、通常はデータがバインドされている TextBlock にテキストを追加できます。

```xml
<TextBlock Text="{Binding Name}" d:Text="Name!" />
```

[![TextBlock 内のテキストを含むデザイン時のデータ](media\xaml-design-time-textblock.png "Label 内のテキストを含むデザイン時のデータ")](media\xaml-design-time-textblock.png#lightbox)

この例で、`d:Text` がない場合、XAML デザイナーの TextBlock には何も表示されません。 代わりに、"Name!" と表示され、 TextBlock には実行時の実際のデータが含まれます。

`d:` は、色、フォント サイズ、間隔など、任意の UWP または WPF .NET Core コントロールの属性と共に使用できます。 また、コントロール自体に追加することもできます。

```xml
<d:Button Content="Design Time Button" />
```

[![ボタン コントロールを使用したデザイン時のデータ](media\xaml-design-time-button.png "ボタン コントロールを使用したデザイン時のデータ")](media\xaml-design-time-button.png#lightbox)

この例では、ボタンはデザイン時にのみ表示されます。 このメソッドを使用して、カスタム コントロールのプレースホルダーを配置するか、別のコントロールを試します。 `d:` のすべての属性とコントロールは、実行時に無視されます。

## <a name="preview-images-at-design-time"></a>デザイン時に画像をプレビューする

ページにバインドされている、または動的に読み込まれた画像に対して、デザイン時のソースを設定できます。 XAML デザイナーに表示する画像をプロジェクトに追加します。 これで、デザイン時にその画像を XAML デザイナーに表示できます。

```xml
<Image Source={Binding ProfilePicture} d:Source="DesignTimePicture.jpg" />
```

> [!NOTE]
> この例の画像は、ソリューション内に存在している必要があります。

## <a name="design-time-data-for-listviews"></a>ListView のデザイン時のデータ

ListView は、デスクトップ アプリにデータを表示するための一般的な方法です。 ただし、データなしに視覚化することは困難です。 この機能を使用して、デザイン時のインライン データ ItemSource または項目を作成できます。 XAML デザイナーには、デザイン時の ListView の配列の内容が表示されます。

### <a name="wpf-net-core--example"></a>WPF .NET Core の例
system:String 型を使用するには、XAML ヘッダーに `xmlns:system="clr-namespace:System;assembly=mscorlib` が含まれていることを確認してください。

```xml
<StackPanel>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type system:String}">
                <system:String>Item One</system:String>
                <system:String>Item Two</system:String>
                <system:String>Item Three</system:String>
            </x:Array>
        </d:ListView.ItemsSource>
    <ListView.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding ItemName}" d:Text="{Binding .}" />
        </DataTemplate>
    </ListView.ItemTemplate>
   </ListView>
</StackPanel>
```

[![ListView を使用したデザイン時のデータ](media\xaml-design-time-listview-strings.png "ListView を使用したデザイン時のデータ")](media\xaml-design-time-listview-strings.png#lightbox)

前の例は、XAML デザイナーの 3 つの Textblock がある ListView を示しています。

また、データ オブジェクトの配列を作成することもできます。 たとえば、`City` データ オブジェクトのパブリック プロパティは、デザイン時のデータとして構築できます。

```csharp
namespace Cities.Models
{
    public class City
    {
        public string Name { get; set; }
        public string Country { get; set; }
    }
}
```

XAML でクラスを使用するには、ルート ノードで名前空間をインポートする必要があります。

```xaml
xmlns:models="clr-namespace:Cities.Models"
```

```xml
<StackPanel>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type models:City}">
                <models:City Name="Seattle" Country="United States"/>
                <models:City Name="London" Country="United Kingdom"/>
                <models:City Name="Panama City" Country="Panama"/>
            </x:Array>
        </d:ListView.ItemsSource>
        <ListView.ItemTemplate>
            <DataTemplate>
                 <StackPanel Orientation="Horizontal" >
                    <TextBlock Text="{Binding Name}" Margin="0,0,5,0" />
                    <TextBlock Text="{Binding Country}" />
                 </StackPanel>
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>
</StackPanel>
```

[![ListView を使用したデザイン時のデータの実際のモデル](media\xaml-design-time-listview-models.png "ListView を使用したデザイン時のデータの実際のモデル")](media\xaml-design-time-listview-models.png#lightbox)

ここでのベネフィットは、コントロールをモデルのデザイン時の静的なバージョンにバインドできることです。

### <a name="uwp-example"></a>UWP の例 

UWP では x:Array がサポートされていません。 そのため、代わりに `<d:ListView.Items>` を使用できます。 system:String 型を使用するには、XAML ヘッダーに `http://schemas.microsoft.com/winfx/2009/xaml` が含まれていることを確認してください。

```xml
    <StackPanel>
        <ListView>
            <d:ListView.Items>
                <system:String>Item One</system:String>
                <system:String>Item Two</system:String>
                <system:String>Item Three</system:String>
            </d:ListView.Items>
        </ListView>
    </StackPanel>
```

## <a name="use-design-time-data-with-custom-types-and-properties"></a>カスタム型とプロパティと共にデザイン時データを使用する

この機能は既定では、プラットフォームのコントロールとプロパティでのみ動作します。 このセクションでは、Visual Studio 2019 バージョン [16.8](/visualstudio/releases/2019/release-notes/) 以降をご利用のお客様が使える新機能、デザイン時コントロールとして独自のカスタム コントロールを使用できるようにするために必要な手順を確認します。 これを可能にするには、次の 3 つの要件があります。

- カスタム xmlns 名前空間

    ```xml
    xmlns:myControls="http://MyCustomControls"
    ```

- 名前空間のデザイン時バージョン。 これは末尾に /design を追加するだけで達成できます。

     ```xml
    xmlns:myDesignTimeControls="http://MyCustomControls/design"
    ```

- mc:Ignorable にデザイン時プレフィックスを追加する

    ```xml
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d myDesignTimeControls"
    ```

以上の手順をすべて実行したら、`myDesignTimeControls` プレフィックスを使用し、デザイン時コントロールを作成できます。

```xml
<myDesignTimeControls:MyButton>I am a design time Button</myDesignTimeControls:MyButton>
```

### <a name="creating-a-custom-xmlns-namespace"></a>カスタム xmlns 名前空間を作成する

WPF .NET Core でカスタム xmlns 名前空間を作成するには、コントロールが入っている CLR 名前空間にカスタム XML 名前空間をマッピングする必要があります。 これを行うには、`AssemblyInfo.cs` ファイルで `XmlnsDefinition` アセンブリレベル属性を追加します。 ファイルはプロジェクトのルート階層にあります。

   ```C#
[assembly: XmlnsDefinition("http://MyCustomControls", "MyViews.MyButtons")]
   ```

## <a name="troubleshooting"></a>トラブルシューティング

このセクションに記載されていない問題が発生した場合は、[[問題の報告]](../ide/how-to-report-a-problem-with-visual-studio.md) ツールを使用してお知らせください。

### <a name="requirements"></a>要件

- デザイン時のデータには、Visual Studio 2019 バージョン [16.7](/visualstudio/releases/2019/release-notes-v16.7) 以降が必要です。

- .NET Core および UWP 用の Windows Presentation Foundation (WPF) を対象とする Windows デスクトップ プロジェクトがサポートされていること。 この機能は、.NET Framework の[プレビュー チャネル](/visualstudio/releases/2019/release-notes-preview)でも利用できます。 これを有効にするには、 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[プレビュー機能]** にアクセスし、 **[.NET Framework 用の新しい WPF XAML デザイナー]** を選択してから Visual Studio を再起動します。

- Visual Studio 2019 バージョン 16.7 以降では、この機能は、WPF および UWP のフレームワークのすべての組み込みコントロールで動作します。 [16.8 リリース](/visualstudio/releases/2019/release-notes/)では、サードパーティ製コントロールのサポートが提供されるようになりました。

### <a name="the-xaml-designer-stopped-working"></a>XAML デザイナーの動作が停止した

XAML ファイルを閉じて再度開き、プロジェクトのクリーンアップとリビルドを試してみてください。

## <a name="see-also"></a>関連項目

- [Xamarin.Forms プレビューアーを使用したデザイン時のデータ](/xamarin/xamarin-forms/xaml/xaml-Designer/design-time-data/)
- [WPF アプリの XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP アプリの XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms アプリの XAML](/xamarin/xamarin-forms/xaml/)