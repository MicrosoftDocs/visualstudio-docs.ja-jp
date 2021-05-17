---
title: WPF と Entity Framework 6 を使用した単純なデータ アプリ
description: このチュートリアルでは、Windows Presentation Foundation (WPF) と Entity Framework 6 を使用して Visual Studio で単純なフォーム オーバー データ アプリを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/22/2017
ms.topic: conceptual
dev_langs:
- CSharp
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: e3432dd9a72fa71ea1e749dd28e80a3d55cce19c
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216060"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>WPF と Entity Framework 6 を使用して単純なデータ アプリケーションを作成する

このチュートリアルでは、Visual Studio で基本的な "フォーム オーバー データ" アプリケーションを作成する方法について説明します。 アプリでは、SQL Server LocalDB、Northwind データベース、(Entity Framework Core ではなく) Entity Framework 6、(.NET Core ではなく) .NET Framework 用の Windows Presentation Foundation を使用します。 ここでは、マスター ビューと詳細ビューで基本的なデータ バインドを実行する方法について説明します。また、 **[次に移動]** 、 **[前に戻る]** 、 **[先頭に移動]** 、 **[末尾に移動]** 、 **[更新]** 、 **[削除]** のボタンがあるカスタム バインド ナビゲーターもあります。

この記事では Visual Studio でのデータ ツールの使用に焦点を当てていますが、基になるテクノロジの詳細については説明しません。 XAML、Entity Framework、SQL に関する基本的な知識があることを前提としています。 また、この例では、WPF アプリケーションの標準である Model-View-ViewModel (MVVM) アーキテクチャについても説明しません。 ただし、いくつかの変更を加えれば、このコードを独自の MVVM アプリケーションにコピーできます。

## <a name="install-and-connect-to-northwind"></a>Northwind をインストールして接続する

この例では SQL Server Express LocalDB と Northwind サンプル データベースを使用します。 その製品の ADO.NET データ プロバイダーが Entity Framework をサポートしている場合は、他の SQL データベース製品でも同様に機能します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** で、**.NET デスクトップ開発** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (**SQL Server オブジェクト エクスプローラー** は、**Visual Studio インストーラー** の **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

3. Northwind に対して[新しい接続を追加します](../data-tools/add-new-connections.md)。

## <a name="configure-the-project"></a>プロジェクトを構成する

1. Visual Studio で、新しい C# **WPF アプリ** プロジェクトを作成します。

2. Entity Framework 6 の NuGet パッケージを追加します。 **ソリューション エクスプローラー** でプロジェクト ノードを選択します。 メイン メニューで、 **[プロジェクト]**  >  **[NuGet パッケージの管理]** の順に選択します。

     ![[NuGet パッケージの管理] メニュー項目](../data-tools/media/raddata_vs2015_manage_nuget_packages.png)

3. **NuGet パッケージ マネージャー** で、 **[参照]** リンクをクリックします。 通常、Entity Framework は一覧の最上位のパッケージです。 右側のペインで **[インストール]** をクリックし、画面の指示に従います。 インストールが完了すると、[出力] ウィンドウに通知されます。

     ![Entity Framework NuGet パッケージ](../data-tools/media/raddata_vs2015_nuget_ef.png)

4. これで、Visual Studio を使用して、Northwind データベースに基づくモデルを作成できるようになりました。

## <a name="create-the-model"></a>モデルを作成する

1. **ソリューション エクスプローラー** でプロジェクト ノードを右クリックし、 **[追加]**  >  **[新しい項目]** を選択します。 左側のペインの [C#] ノードで **[データ]** を選択し、中央のペインで **[ADO.NET Entity Data Model]** を選択します。

   ![Entity Framework Model の新しい項目](../data-tools/media/raddata-ef-new-project-item.png)

2. モデル `Northwind_model` を呼び出し、 **[OK]** を選択します。 **Entity Data Model ウィザード** が開きます。 **[データベースの EF デザイナー]** を選択し、 **[次へ]** をクリックします。

   ![データベースからの EF モデル](../data-tools/media/raddata-ef-model-from-database.png)

3. 次の画面で、LocalDB Northwind 接続 (たとえば、(localdb)\MSSQLLocalDB) を入力または選択し、Northwind データベースを指定して、 **[次へ]** をクリックします。

4. ウィザードの次のページで、Entity Framework モデルに含めるテーブル、ストアド プロシージャ、およびその他のデータベース オブジェクトを選択します。 ツリー ビューで dbo ノードを展開し、 **[Customers]** 、 **[Orders]** 、 **[Order Details]** を選択します。 既定値をオンのままにして、 **[完了]** をクリックします。

    ![モデルのデータベース オブジェクトを選択する](../data-tools/media/raddata-choose-ef-objects.png)

5. このウィザードでは、Entity Framework モデルを表す C# クラスが生成されます。 クラスは単純な従来の C# クラスであり、WPF ユーザー インターフェイスにデータをバインドします。 *.edmx* ファイルには、クラスをデータベース内のオブジェクトに関連付けるリレーションシップとその他のメタデータが記述されています。 *.tt* ファイルは、モデルで動作するコードを生成し、変更内容をデータベースに保存する T4 テンプレートです。 これらのファイルはすべて、Northwind_model ノードの下の **ソリューション エクスプローラー** に表示されます。

      ![EF モデル ファイルのソリューション エクスプローラー](../data-tools/media/raddata-solution-explorer-ef-model-files.png)

    *.edmx* ファイルのデザイナー画面を使用すると、モデル内のいくつかのプロパティとリレーションシップを変更できます。 このチュートリアルでは、デザイナーを使用しません。

6. *.tt* ファイルは汎用的なものであるため、ObservableCollection を必要とする WPF データ バインドを使用するには、そのうちの 1 つを調整する必要があります。 **ソリューション エクスプローラー** で、*Northwind_model.tt* が見つかるまで Northwind_model ノードを展開します ( *.Context.tt* ファイル内にいないことを確認してください。これは *.edmx* ファイルの直下にあります)。

   - 2 つの <xref:System.Collections.ICollection> を <xref:System.Collections.ObjectModel.ObservableCollection%601> に置き換えます。

   - 51 行目あたりにある最初に見つかった <xref:System.Collections.Generic.HashSet%601> を <xref:System.Collections.ObjectModel.ObservableCollection%601> に置き換えます。 2 番目に見つかった HashSet は置き換えないでください。

   - 431 行目あたりで見つかった <xref:System.Collections.Generic> を <xref:System.Collections.ObjectModel> に置き換えます。

7. **Ctrl**+**Shift**+**B** キーを押して、プロジェクトをビルドします。 ビルドが完了すると、モデル クラスがデータ ソース ウィザードに表示されます。

これで、データを表示、ナビゲーション、変更できるように、このモデルを XAML ページにフックする準備ができました。

## <a name="databind-the-model-to-the-xaml-page"></a>モデルを XAML ページにデータ バインドする

独自のデータ バインド コードを記述することもできますが、Visual Studio で簡単に実行できます。

1. メイン メニューから、 **[プロジェクト]**  >  **[新しいデータ ソースの追加]** の順に選択し、**データ ソース構成ウィザード** を起動します。 データベースではなくモデル クラスにバインドするので、 **[オブジェクト]** を選択します。

     ![オブジェクト ソースを含むデータ ソース構成ウィザード](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png)

2. プロジェクトのノードを展開し、 **[Customer]** を選択します (Orders のソースは、Customer の Orders ナビゲーション プロパティから自動的に生成されます)。

     ![エンティティ クラスをデータ ソースとして追加する](../data-tools/media/raddata-add-entity-classes-as-data-sources.png)

3. **[完了]** をクリックします。

4. コード ビューで *MainWindow.xaml* に移動します。 この例では、XAML を単純なものにしています。 MainWindow のタイトルをわかりやすいものに変更し、高さと幅を 600 x 800 に増やします。 これは後でいつでも変更できます。 ここで、次の 3 つの行定義をメイン グリッドに追加します。1 つはナビゲーション ボタンの行、1 つは顧客の詳細の行、もう 1 つは注文を表示するグリッドの行です。

    ```xaml
        <Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ```

5. ここで、*MainWindow.xaml* を開いてデザイナーで表示します。 これにより、 **[データ ソース]** ウィンドウが、**ツールボックス** の横にある Visual Studio ウィンドウの余白にオプションとして表示されます。 タブをクリックしてウィンドウを開くか、**Shift**+**Alt**+**D** キーを押すか、 **[ビュー]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** の順に選択します。 個々のテキスト ボックスに Customers クラスの各プロパティを表示します。 まず、 **[Customers]** コンボ ボックスの矢印をクリックし、 **[詳細]** を選択します。 次に、デザイナーで中央の行に移動できるように、デザイン サーフェイスの中央部分にノードをドラッグします。 場所を間違えた場合は、XAML で後から行を手動で指定できます。 既定では、コントロールはグリッド要素に垂直方向に配置されますが、この時点では、フォーム上に任意に配置することができます。 たとえば、住所の上に **[名前]** テキスト ボックスを配置した方がよい場合があります。 この記事のサンプル アプリケーションでは、フィールドを並べ替え、2 つの列に再配置します。

     ![個々のコントロールに対する Customers データ ソースのバインド](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png)

     コード ビューで、親グリッドの行 1 (中央の行) に新しい `Grid` 要素が表示されるようになりました。 親グリッドには、`Windows.Resources` 要素に追加された CollectionViewSource を参照する `DataContext` 属性があります。 そのデータ コンテキストでは、最初のテキスト ボックスが **[Address]** にバインドされると、その名前は CollectionViewSource 内の現在の `Customer` オブジェクトの `Address` プロパティにマップされます。

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. ウィンドウの上半分に顧客が表示されている場合は、下半分に注文を表示します。 1 つのグリッド ビュー コントロールに注文を表示します。 マスター/詳細データ バインドが想定どおりに動作するには、個別の Orders ノードではなく、Customers クラスの Orders プロパティにバインドすることが重要です。 Customers クラスの Orders プロパティをフォームの下半分にドラッグして、デザイナーで行 2 に配置されるようにします。

     ![Orders クラスをグリッドとしてドラッグする](../data-tools/media/raddata-drag-orders-classes-as-grid.png)

7. Visual Studio で、UI コントロールをモデル内のイベントに接続するすべてのバインド コードが生成されました。 いくつかのデータを表示するために必要なのは、モデルを作成するためのコードを記述することだけです。 まず、*MainWindow.xaml.cs* に移動し、データ コンテキストの MainWindow クラスにデータ メンバーを追加します。 生成されたこのオブジェクトは、モデル内の変更とイベントを追跡するコントロールのように機能します。 また、顧客と注文の CollectionViewSource データ メンバーと、関連するコンストラクター初期化ロジックも追加します。 クラスの先頭は次のようになります。

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet1":::

     Load 拡張メソッドをスコープに取り込むために、System.Data.Entity に対する `using` ディレクティブを追加します。

     ```csharp
     using System.Data.Entity;
     ```

     次に、下にスクロールして、`Window_Loaded` イベント ハンドラーを見つけます。 Visual Studio によって CollectionViewSource オブジェクトが追加されていることに注意してください。 これは、モデルの作成時に選択した NorthwindEntities オブジェクトを表します。 これは既に追加されているので、ここでは必要ありません。 ここでは、メソッドが次のようになるように、`Window_Loaded` のコードを置き換えます。

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet2":::


8. **F5** キーを押します。 最初に取得された顧客の詳細が CollectionViewSource に表示されます。 また、データ グリッドにも注文が表示されます。 書式設定はあまり良くないので、修正しましょう。 また、他のレコードを表示し、基本的な CRUD 操作を実行する方法を作成することもできます。

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>ページ デザインを調整し、新しい顧客と注文のグリッドを追加する

Visual Studio によって生成される既定の配置はこのアプリケーションには適していないため、ここでコードにコピーする最後の XAML を提供します。 また、ユーザーが新しい顧客または注文を追加できるようにするために、"フォーム" (実際にはグリッド) が必要です。 新しい顧客と注文を追加できるようにするには、`CollectionViewSource` にデータ バインドされていない別のテキスト ボックスのセットが必要です。 任意の時点でユーザーに表示されるグリッドを制御するには、ハンドラー メソッドで Visible プロパティを設定します。 最後に、[Orders] グリッドの各行に [削除] ボタンを追加して、ユーザーが個々の注文を削除できるようにします。

まず、次のスタイルを *MainWindow.xaml* の `Windows.Resources` 要素に追加します。

```xaml
<Style x:Key="Label" TargetType="{x:Type Label}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="23"/>
</Style>
<Style x:Key="CustTextBox" TargetType="{x:Type TextBox}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Right"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="26"/>
    <Setter Property="Width" Value="120"/>
</Style>
```

次に、外側のグリッド全体をこのマークアップに置き換えます。

```xaml
<Grid>
     <Grid.RowDefinitions>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="*"/>
     </Grid.RowDefinitions>
     <Grid x:Name="existingCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" Margin="5" Visibility="Visible" VerticalAlignment="Top" Background="AntiqueWhite" DataContext="{StaticResource customerViewSource}">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type Window}}, Path=newCustomer, UpdateSourceTrigger=Explicit}" Visibility="Collapsed" Background="CornflowerBlue">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true }"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newOrderGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding Path=newOrder, Mode=TwoWay}" Visibility="Collapsed" Background="LightGreen">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="New Order Form" FontWeight="Bold"/>
         <Label Content="Employee ID:"  Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_employeeIDTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding EmployeeID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Order Date:"  Grid.Row="2" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_orderDatePicker" Grid.Row="2"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Required Date:" Grid.Row="3" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_requiredDatePicker" Grid.Row="3" HorizontalAlignment="Right" Width="120"
                  SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Shipped Date:"  Grid.Row="4"  Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_shippedDatePicker"  Grid.Row="4"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Ship Via:"  Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_ShipViaTextBox"  Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding ShipVia, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Freight"  Grid.Row="6" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_freightTextBox" Grid.Row="6" Style="{StaticResource CustTextBox}"
                  Text="{Binding Freight, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <DataGrid x:Name="ordersDataGrid" SelectionUnit="Cell" SelectionMode="Single" AutoGenerateColumns="False" CanUserAddRows="false" IsEnabled="True" EnableRowVirtualization="True" Width="auto" ItemsSource="{Binding Source={StaticResource customerOrdersViewSource}}" Margin="10,10,10,10" Grid.Row="2" RowDetailsVisibilityMode="VisibleWhenSelected">
         <DataGrid.Columns>
             <DataGridTemplateColumn>
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <Button Content="Delete" Command="{StaticResource DeleteOrderCommand}" CommandParameter="{Binding}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="customerIDColumn" Binding="{Binding CustomerID}" Header="Customer ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="employeeIDColumn" Binding="{Binding EmployeeID}" Header="Employee ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="freightColumn" Binding="{Binding Freight}" Header="Freight" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="orderDateColumn" Header="Order Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="orderIDColumn" Binding="{Binding OrderID}" Header="Order ID" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="requiredDateColumn" Header="Required Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipAddressColumn" Binding="{Binding ShipAddress}" Header="Ship Address" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCityColumn" Binding="{Binding ShipCity}" Header="Ship City" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCountryColumn" Binding="{Binding ShipCountry}" Header="Ship Country" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipNameColumn" Binding="{Binding ShipName}" Header="Ship Name" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="shippedDateColumn" Header="Shipped Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipPostalCodeColumn" Binding="{Binding ShipPostalCode}" Header="Ship Postal Code" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipRegionColumn" Binding="{Binding ShipRegion}" Header="Ship Region" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipViaColumn" Binding="{Binding ShipVia}" Header="Ship Via" Width="SizeToHeader"/>
         </DataGrid.Columns>
     </DataGrid>
 </Grid>
```

## <a name="add-buttons-to-navigate-add-update-and-delete"></a>ナビゲーション、追加、更新、削除のボタンを追加する

Windows フォーム アプリケーションでは、データベース内の行を移動して基本的な CRUD 操作を実行するためのボタンを持つ BindingNavigator オブジェクトを取得します。 WPF には BindingNavigator が用意されていませんが、簡単に作成できます。 この操作は、水平方向の StackPanel 内のボタンを使用して行い、分離コード内のメソッドにバインドされているコマンドにボタンを関連付けます。

コマンド ロジックには、(1) コマンド、(2) バインド、(3) ボタン、(4) 分離コード内のコマンド ハンドラーの 4 つの部分があります。

### <a name="add-commands-bindings-and-buttons-in-xaml"></a>XAML にコマンド、バインド、ボタンを追加する

1. 最初に、`Windows.Resources` 要素内に *MainWindow.xaml* ファイル内のコマンドを追加します。

    ```xaml
    <RoutedUICommand x:Key="FirstCommand" Text="First"/>
    <RoutedUICommand x:Key="LastCommand" Text="Last"/>
    <RoutedUICommand x:Key="NextCommand" Text="Next"/>
    <RoutedUICommand x:Key="PreviousCommand" Text="Previous"/>
    <RoutedUICommand x:Key="DeleteCustomerCommand" Text="Delete Customer"/>
    <RoutedUICommand x:Key="DeleteOrderCommand" Text="Delete Order"/>
    <RoutedUICommand x:Key="UpdateCommand" Text="Update"/>
    <RoutedUICommand x:Key="AddCommand" Text="Add"/>
    <RoutedUICommand x:Key="CancelCommand" Text="Cancel"/>
    ```

2. CommandBinding では、`RoutedUICommand` イベントを分離コード内のメソッドにマップします。 `Windows.Resources` 終了タグの後に次の `CommandBindings` 要素を追加します。

    ```xaml
    <Window.CommandBindings>
        <CommandBinding Command="{StaticResource FirstCommand}" Executed="FirstCommandHandler"/>
        <CommandBinding Command="{StaticResource LastCommand}" Executed="LastCommandHandler"/>
        <CommandBinding Command="{StaticResource NextCommand}" Executed="NextCommandHandler"/>
        <CommandBinding Command="{StaticResource PreviousCommand}" Executed="PreviousCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteCustomerCommand}" Executed="DeleteCustomerCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteOrderCommand}" Executed="DeleteOrderCommandHandler"/>
        <CommandBinding Command="{StaticResource UpdateCommand}" Executed="UpdateCommandHandler"/>
        <CommandBinding Command="{StaticResource AddCommand}" Executed="AddCommandHandler"/>
        <CommandBinding Command="{StaticResource CancelCommand}" Executed="CancelCommandHandler"/>
    </Window.CommandBindings>
    ```

3. 次に、ナビゲーション、追加、削除、更新の各ボタンを `StackPanel` に追加します。 まず、次のスタイルを `Windows.Resources` に追加します。

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     次に、XAML ページの上部に向かって、外側の `Grid` 要素の `RowDefinitions` の直後に次のコードを貼り付けます。

    ```xaml
    <StackPanel Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">
        <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnPrev" Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnNext" Content="►" Command="{StaticResource NextCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnLast" Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>
        <Button Name="btnAdd" Content="New Customer" Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>
        <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="Cancel" Name="btnCancel" Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
    </StackPanel>
    ```

### <a name="add-command-handlers-to-the-mainwindow-class"></a>MainWindow クラスにコマンド ハンドラーを追加する

追加メソッドと削除メソッドを除き、分離コードは最小限です。 ナビゲーションは、CollectionViewSource の View プロパティでメソッドを呼び出すことによって実行されます。 `DeleteOrderCommandHandler` では、注文に対して連鎖削除を実行する方法を示します。 最初に、関連付けられている Order_Details を削除する必要があります。 `UpdateCommandHandler` では、新しい顧客または注文をコレクションに追加します。それ以外の場合は、ユーザーがテキスト ボックスで行った変更を使用して、既存の顧客または注文を更新します。

これらのハンドラー メソッドを *MainWindow.xaml.cs* の MainWindow クラスに追加します。 Customers テーブルの CollectionViewSource に別の名前が付いている場合は、次の各メソッドで名前を調整する必要があります。

:::code language="csharp" source="../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs" id="Snippet3":::


## <a name="run-the-application"></a>アプリケーションの実行

デバッグを開始するには、**F5** キーを押します。 顧客データと注文データがグリッドに表示され、ナビゲーション ボタンは期待どおりに動作します。 データの入力後に **[コミット]** をクリックすると、新しい顧客または注文がモデルに追加されます。 **[キャンセル]** をクリックすると、データを保存せずに、新しい顧客フォームまたは新しい注文フォームから戻ることができます。 テキスト ボックスで既存の顧客や注文を直接編集することができ、それらの変更は自動的にモデルに書き込まれます。

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Entity Framework ドキュメント](/ef/)
