---
title: データセットへの WPF コントロールのバインド
description: Visual Studio でデータバインド コントロールを含む WPF アプリケーションを作成します。これらのコントロールは、データセットにカプセル化された製品レコードにバインドされます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 177420b9-568b-4dad-9d16-1b0e98a24d71
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: b67e70792f6e7864749b603f30ab868ef177336a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215566"
---
# <a name="bind-wpf-controls-to-a-dataset"></a>データセットへの WPF コントロールのバインド

このチュートリアルでは、データバインド コントロールを含む WPF アプリケーションを作成します。 コントロールは、データセットでカプセル化された製品レコードにバインドされます。 また、製品を参照するためのボタンの追加と、製品レコードへの変更の保存も行います。

このチュートリアルでは、次の作業について説明します。

- WPF アプリケーションと、AdventureWorksLT サンプル データベースのデータから生成されるデータセットを作成する。

- **[データ ソース]** ウィンドウから WPF デザイナーのウィンドウにデータ テーブルをドラッグして、一連のデータ バインド コントロールを作成する。

- 製品レコード間を前後に移動するためのボタンを作成する。

- ユーザーが製品レコードに加えた変更を、データ テーブルおよび基になるデータ ソースに保存するボタンを作成する。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio

- AdventureWorks Light (AdventureWorksLT) サンプル データベースがアタッチされた、SQL Server または SQL Server Express の実行中のインスタンスへのアクセス権。 AdventureWorksLT データベースは、[CodePlex アーカイブ](https://archive.codeplex.com/?p=awlt2008dbscript)からダウンロードできます。

次の概念に関する知識があると役立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- データセットおよび TableAdapter。 詳細については、[Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)および[TableAdapters](../data-tools/create-and-configure-tableadapters.md) に関するページを参照してください。

- WPF データ バインディング。 詳しくは、「 [データ バインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)」をご覧ください。

## <a name="create-the-project"></a>プロジェクトを作成する

製品レコードを表示する新しい WPF プロジェクトを作成します。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

2. **[ファイル]** メニューの **[新規]** > **[プロジェクト]** を選択します。

3. **[Visual Basic]** または **[Visual C#]** を展開し、**[Windows]** を選択します。

4. **[WPF アプリケーション]** プロジェクト テンプレートを選択します。

5. **[名前]** ボックスに「**AdventureWorksProductsEditor**」と入力して、 **[OK]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. C# の **[WPF アプリケーション]** プロジェクト テンプレートを検索し、手順に従ってプロジェクトを作成し、プロジェクトに **AdventureWorksProductsEditor** という名前を付けます。

::: moniker-end

   Visual Studio によって AdventureWorksProductsEditor プロジェクトが作成されます。

## <a name="create-a-dataset-for-the-application"></a>アプリケーション用のデータセットを作成する

データ バインド コントロールを作成するには、まず、アプリケーション用のデータ モデルを定義し、**[データ ソース]** ウィンドウに追加する必要があります。 このチュートリアルでは、データ モデルとして使用するデータセットを作成します。

1. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

   **[データ ソース]** ウィンドウが開きます。

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

   **データ ソース構成** ウィザードが開きます。

3. **[データソースの種類を選択]** ページで、**[データベース]** を選択し、**[次へ]** をクリックします。

4. **[データベース モデルの選択]** ページで、**[データセット]** を選択し、**[次へ]** をクリックします。

5. **[データ接続の選択]** ページで、次のいずれかのオプションを選択します。

   - AdventureWorksLT サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これを選択し、**[次へ]** をクリックします。

   - **[新しい接続]** をクリックして、AdventureWorksLT データベースへの接続を作成します。

6. **[接続文字列をアプリケーション構成ファイルに保存する]** ページで、**[次の名前で接続を保存する]** チェック ボックスをオンにし、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** を展開し、**Product (SalesLT)** テーブルを選択します。

8. **[完了]** をクリックします。

   Visual Studio によって、新しい `AdventureWorksLTDataSet.xsd` ファイルがプロジェクトに追加されます。また、対応する **AdventureWorksLTDataSet** 項目が **[データ ソース]** ウィンドウに追加されます。 `AdventureWorksLTDataSet.xsd` ファイルには、`AdventureWorksLTDataSet` という名前の型指定されたデータセットと、`ProductTableAdapter` という名前の TableAdapter が定義されます。 このチュートリアルの後半で、`ProductTableAdapter` を使用してデータセットにデータを読み込み、変更をデータベースに保存します。

9. プロジェクトをビルドします。

## <a name="edit-the-default-fill-method-of-the-tableadapter"></a>TableAdapter の既定の Fill メソッドを編集する

データセットにデータを読み込むには、`Fill` の `ProductTableAdapter` メソッドを使用します。 既定では、`Fill` メソッドによって、`ProductDataTable` の `AdventureWorksLTDataSet` に Product テーブルのすべてのデータ行が読み込まれます。 このメソッドは、行のサブセットのみを返すように変更できます。 このチュートリアルでは、写真付きの製品の行のみを返すように `Fill` メソッドを変更します。

1. **ソリューション エクスプローラー** で、*AdventureWorksLTDataSet.xsd* ファイルをダブルクリックします。

     データセット デザイナーが開きます。

2. デザイナーで、**[Fill**, **GetData()]** クエリを右クリックし、**[構成]** を選択します。

     **TableAdapter 構成** ウィザードが開きます。

3. **[SQL ステートメントの入力]** ページのテキスト ボックスで、`SELECT` ステートメントの後に次の WHERE 句を追加します。

    ```sql
    WHERE ThumbnailPhotoFileName <> 'no_image_available_small.gif'
    ```

4. **[完了]** をクリックします。

## <a name="define-the-user-interface"></a>ユーザー インターフェイスを定義する

WPF デザイナーで XAML を変更して、いくつかのボタンをウィンドウに追加します。 これらのボタンを使用して製品レコード間をスクロールしたり、製品レコードへの変更を保存したりできるようにするコードは、このチュートリアルで後で追加します。

1. **ソリューション エクスプローラー** で、*MainWindow.xaml* をダブルクリックします。

    **WPF デザイナー** でウィンドウが開きます。

2. デザイナーの [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] ビューで、`<Grid>` タグの間に次のコードを追加します。

   ```xaml
   <Grid.RowDefinitions>
       <RowDefinition Height="75" />
       <RowDefinition Height="625" />
   </Grid.RowDefinitions>
   <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75">&lt;</Button>
   <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">&gt;</Button>
   <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>
   ```

3. プロジェクトをビルドします。

## <a name="create-data-bound-controls"></a>データ バインド コントロールを作成する

顧客レコードを表示するコントロールを作成するには、 **[データ ソース]** ウィンドウから WPF デザイナーに `Product` テーブルをドラッグします。

1. **[データ ソース]** ウィンドウで、**[Product]** ノードのドロップダウン メニューをクリックし、**[詳細]** を選択します。

2. **[Product]** ノードを展開します。

3. この例ではいくつかのフィールドを非表示にするために、次のノードの横のドロップダウン メニューをクリックして **[なし]** を選択します。

    - ProductCategoryID

    - ProductModelID

    - ThumbnailPhotoFileName

    - rowguid

    - ModifiedDate

4. **[ThumbNailPhoto]** ノードの横にあるドロップダウン メニューをクリックし、**[イメージ]** を選択します。

    > [!NOTE]
    > 既定では、画像を表す **[データ ソース]** ウィンドウ内の項目は、既定のコントロールが **[なし]** に設定されています。 これは、画像がデータベース内でバイト配列として格納されているためです。バイト配列には、単純なバイト配列から大規模なアプリケーションの実行可能ファイルまで、あらゆるデータを格納できます。

5. **[データ ソース]** ウィンドウから、ボタンがある行の下のグリッド行に **[Product]** ノードをドラッグします。

     Visual Studio によって、**Product** テーブルのデータにバインドされるコントロール セットを定義する XAML が生成されます。 また、データを読み込むコードも生成されます。 生成される XAML およびコードの詳細については、「[Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

6. デザイナーで、**[Product ID]** ラベルの横のテキスト ボックスをクリックします。

7. **[プロパティ]** ウィンドウで、**IsReadOnly** プロパティの横のチェック ボックスをオンにします。

## <a name="navigate-product-records"></a>製品レコードの移動

ユーザーが **\<** and **>** ボタンを使用して製品レコード間をスクロールできるようにするコードを追加します。

1. デザイナーで、ウィンドウ サーフェイスの **[<]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`backButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `Window_Loaded` イベント ハンドラーを変更して、`ProductViewSource`、`AdventureWorksLTDataSet`、`AdventureWorksLTDataSetProductTableAdapter` がメソッドの外部になり、フォーム全体からアクセスできるようにします。 次のように、フォームに対してこれらのみをグローバルとして宣言し、`Window_Loaded` イベント ハンドラー内でそれらを割り当てます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet1":::

3. `backButton_Click` イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet2":::

4. デザイナーに戻り、 **[>]** をダブルクリックします。

5. `nextButton_Click` イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet3":::

## <a name="save-changes-to-product-records"></a>製品レコードに変更を保存する

ユーザーが **[変更の保存]** ボタンを使用して製品レコードへの変更を保存できるようにするコードを追加します。

1. デザイナーで、**[変更の保存]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`saveButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `saveButton_Click` イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb" id="Snippet4":::

    > [!NOTE]
    > この例では、`Save` の `TableAdapter` メソッドを使用して変更を保存します。 このチュートリアルでは、データ テーブルが 1 つのみ変更されるため、この方法が適しています。 複数のデータ テーブルへの変更を保存する必要がある場合は、Visual Studio によってデータセットと共に生成される `UpdateAll` の `TableAdapterManager` メソッドを使用することもできます。 詳細については、[TableAdapter](../data-tools/create-and-configure-tableadapters.md) に関するページを参照してください。

## <a name="test-the-application"></a>アプリケーションをテストする

アプリケーションをビルドして実行します。 製品レコードを表示および更新できることを確認します。

1. **F5** キーを押します。

     アプリケーションがビルドされ、実行されます。 次の点を確認します。

    - テキスト ボックスに、写真付きの製品の先頭のレコードのデータが表示されること。 この製品の製品 ID は 713 で、製品名は **Long-Sleeve Logo Jersey, S** です。

    - **[>]** または **[<]** をクリックして、他の製品レコードに移動できること。

2. いずれかの製品レコードで **[サイズ]** の値を変更し、**[変更の保存]** をクリックします。

3. アプリケーションを終了し、Visual Studio で **F5** キーを押してアプリケーションを再起動します。

4. 変更した製品レコードに移動し、変更が保持されていることを確認します。

5. アプリケーションを終了します。

## <a name="next-steps"></a>次のステップ

このチュートリアルを完了した後、関連する次のタスクを試してみることができます。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールをその他の種類のデータ ソースにバインドする方法について学習します。 詳細については、「[WCF Data Service への WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)」を参照してください。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールでの関連するデータ (つまり、親子関係にあるデータ) を表示する方法について学習します。 詳細については、チュートリアル「[WPF アプリケーションで関連データを表示する](../data-tools/display-related-data-in-wpf-applications.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [データ バインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)
