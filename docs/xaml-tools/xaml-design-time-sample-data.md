---
title: Visual Studio の XAML デザイナーでデザイン時のサンプル データを使用する
description: XAML でデザイン時のサンプル データを使用する方法について説明します。
ms.date: 06/01/2021
ms.topic: conceptual
author: alihamie
ms.author: tglee
manager: jmartens
monikerRange: '>=vs-2019'
ms.openlocfilehash: 66418d351280a0c067327716766725d22488131b
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760914"
---
# <a name="use-design-time-sample-data-with-the-xaml-designer-in-visual-studio"></a>Visual Studio の XAML デザイナーでデザイン時のサンプル データを使用する

ListView、ListBox、DataGrid などの一部のデータ依存コントロールは、データなしでは視覚化が難しい場合があります。 このドキュメントでは、新しいデザイナーを使用して **WPF .NET Core** プロジェクトまたは **WPF .NET Framework** プロジェクトで作業する開発者が、このようなコントロールでサンプル データを有効にできるようにする新しいアプローチについて確認します。 

## <a name="sample-data-feature-basics"></a>サンプル データ機能の基本

サンプル データはデザイン時の視覚化専用です。つまり、実行中のアプリではなく、XAML デザイナーにのみ表示されます。 そのため、これは ItemsSource プロパティ `d:ItemsSource` のデザイン時バージョンに適用されます。 サンプル データが機能するには、デザイン時の名前空間が必要です。 開始するには、次のコード行を XAML ドキュメントのヘッダーに追加します (まだ存在していない場合)。

> [!NOTE]
> XAML のデザイン時プロパティの詳細については、[XAML のデザイン時のプロパティ](../xaml-tools/xaml-designtime-data.md)に関する記事を参照してください。

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

名前空間を追加したら、`d:ItemsSource="{d:SampleData}"` を使用して ListView、Listbox、または DataGrid でサンプル データを有効にできます。 次に例を示します。

```xml
<DataGrid d:ItemsSource="{d:SampleData}"/>
```

[![DataGrid を使用したサンプル データ](media\xaml-sample-data-empty-datagrid.png "DataGrid で有効になっているサンプル データ")](media\xaml-sample-data-empty-datagrid.png#lightbox)

この例では、`d:ItemsSource="{d:SampleData}"` なしで XAML デザイナーに空の DataGrid が表示されます。 代わりに、`d:SampleData` で既定のサンプル データが生成されたことが表示されます。

既定では、5 つの項目が表示されます。 しかし、**ItemCount** プロパティを使用して、表示する項目の数を指定することができます。 たとえば、`d:ItemsSource="{d:SampleData ItemCount=2}"`

## <a name="sample-data-works-with-datatemplates"></a>datatemplate で動作するサンプル データ

サンプル データは、データ テンプレートを使用するときに ListBox、ListView、または DataGrid コントロールに対して機能します。 サンプル データ機能では、DataTemplate が分析され、それに対する適切なデータの生成が試みられます。 サンプル データは、バインドを使用する DataTemplate 内の要素に対してのみ生成されます。 バインドにソースがまだない場合でも、サンプル データが生成されます。
次に例を示します。

```xml
<ListView d:ItemsSource="{d:SampleData ItemCount=3}">
     <ListView.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
                <Image Width="50" Source="{Binding ProfilePicture}"/>
                <StackPanel Orientation="Vertical">
                    <TextBlock Text="{Binding FirstName}" Margin="5"/>
                    <Label Content="{Binding LastName}"/>
                </StackPanel>
            </StackPanel>
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>
```

[![サンプル データの DataTemplate を使用する ListView](media\xaml-sample-data-templated-listview.png "ListView で使用されるサンプル データ (DataTemplate を使用)")](media\xaml-sample-data-templated-listview.png#lightbox)

## <a name="enable-sample-data-with-suggested-actions"></a>推奨されるアクションを使用してサンプル データを有効にする

デザイナーからコントロールのサンプル データを簡単に有効または無効にするため、推奨されるアクションの機能を使用できます。 推奨されるアクションはデザイナーでコントロールを選択すると右上に電球で表示されます。 サンプル データを有効にするには、コントロールを選択し、電球をクリックして `Show Sample Data` をクリックします。 次に例を示します。

[![サンプル データの推奨されるアクション](media\xaml-sample-data-suggested-actions.png "推奨されるアクションを使用してサンプル データを有効にする")](media\xaml-sample-data-suggested-actions.png#lightbox)

## <a name="sample-data-with-ivalueconverters"></a>IValueConverter を使用したサンプル データ 

コンバーターは、サンプル データ機能では完全にはサポートされていません。 ただし、次のうち一方または両方を実行することで機能させることができます。
- 値が既に targetType であるシナリオを `Convert` 関数で処理できるようにする。

- 値を元の型に戻す `ConvertBack` 関数を実装する。 

## <a name="troubleshooting"></a>トラブルシューティング

サンプル データに何も表示されない、または正しい型が表示されない場合は、デザイナーを最新の情報に更新するか、ページを閉じ、もう一度開いてみてください。

このセクションに記載されていない、またはページを最新の情報に更新しても修正されない問題が発生した場合は、[[問題の報告]](../ide/how-to-report-a-problem-with-visual-studio.md) ツールを使用してお知らせください。

### <a name="requirements"></a>必要条件

- サンプル データには、Visual Studio 2019 バージョン [16.10](/visualstudio/releases/2019/release-notes-v16.10) 以降が必要です。

- 新しいデザイナーを使用する場合は .NET Core または .NET Framework の Windows Presentation Foundation (WPF) をターゲットにする Windows デスクトップ プロジェクトのサポート。 .NET Framework で新しいデザイナーを有効にするには、[ツール]、[オプション]、[環境]、[プレビュー機能] の順にアクセスし、[.NET Framework 向けの新しい WPF XAML デザイナー] を選択してから Visual Studio を再起動します。

## <a name="see-also"></a>関連項目

- [XAML デザイン時のプロパティ](../xaml-tools/xaml-designtime-data.md)
- [WPF アプリの XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP アプリの XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms アプリの XAML](/xamarin/xamarin-forms/xaml/)