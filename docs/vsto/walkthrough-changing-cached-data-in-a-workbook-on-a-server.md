---
title: 'チュートリアル: サーバー上のブックのキャッシュされたデータを変更する'
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks [Office development in Visual Studio], changing server data
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 06fb2532a128384369a9f3617166c9f340f21030
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551337"
---
# <a name="walkthrough-change-cached-data-in-a-workbook-on-a-server"></a>チュートリアル: サーバー上のブックのキャッシュされたデータを変更する
  このチュートリアルでは、 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>クラスを使用して excel を起動せずに Microsoft Office excel ブックにキャッシュされているデータセットを変更する方法について説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 このチュートリアルでは、次の作業について説明します。

- AdventureWorksLT データベースのデータを含むデータセットを定義する。

- Excel ブックプロジェクトとコンソールアプリケーションプロジェクトでデータセットのインスタンスを作成する。

- ブックの<xref:Microsoft.Office.Tools.Excel.ListObject>データセットにバインドされたを作成し、ブックを<xref:Microsoft.Office.Tools.Excel.ListObject>開いたときににデータを設定します。

- ブック内のデータセットをデータキャッシュに追加します。

- Excel を起動せずに、コンソールアプリケーションでコードを実行して、キャッシュされたデータセット内のデータ列を変更する。

  このチュートリアルでは、開発用コンピューターでコードを実行していることを前提としていますが、このチュートリアルで示すコードは、Excel がインストールされていないサーバーで使用できます。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- AdventureWorksLT サンプルデータベースがアタッチされている Microsoft SQL Server または Microsoft SQL Server Express の実行中のインスタンスへのアクセス。 AdventureWorksLT データベースは、 [CodePlex の web サイト](http://go.microsoft.com/fwlink/?linkid=87843)からダウンロードできます。 データベースをアタッチする方法について詳しくは、次のトピックをご覧ください。

  - SQL Server Management Studio または SQL Server Management Studio Express を使用してデータベースをアタッチ[する方法については、「」を参照してください。データベースをアタッチします (](/sql/relational-databases/databases/attach-a-database)SQL Server Management Studio)。

  - コマンドラインを使用してデータベースをアタッチする方法[については、「」を参照してください。SQL Server Express](/previous-versions/sql/)にデータベースファイルをアタッチします。

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>データセットを定義するクラスライブラリプロジェクトを作成する
 Excel ブックプロジェクトとコンソールアプリケーションで同じデータセットを使用するには、これらのプロジェクトの両方によって参照される別のアセンブリにデータセットを定義する必要があります。 このチュートリアルでは、クラスライブラリプロジェクトにデータセットを定義します。

### <a name="to-create-the-class-library-project"></a>クラスライブラリプロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. [テンプレート] ペインで、 **[ C#ビジュアル**] または [ **Visual Basic**] を展開し、[ **Windows**] をクリックします。

4. プロジェクトテンプレートの一覧で [**クラスライブラリ**] を選択します。

5. [**名前**] ボックスに「 **AdventureWorksDataSet**」と入力します。

6. [**参照**] をクリックし、 *%UserProfile%\My ドキュメント*(windows XP 以前の場合) または *%UserProfile%\Documents* (windows Vista の場合) フォルダーに移動して、[**フォルダーの選択**] をクリックします。

7. [**新しいプロジェクト**] ダイアログボックスで、[**ソリューションのディレクトリを作成**する] チェックボックスがオフになっていることを確認します。

8. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**AdventureWorksDataSet**プロジェクトを**ソリューションエクスプローラー**に追加し、 **Class1.cs**または**Class1**コードファイルを開きます。

9. **ソリューションエクスプローラー**で、 **Class1.cs**または**Class1**を右クリックし、[**削除**] をクリックします。 このチュートリアルでは、このファイルは必要ありません。

## <a name="define-a-dataset-in-the-class-library-project"></a>クラスライブラリプロジェクトでのデータセットの定義
 SQL Server 2005 の AdventureWorksLT データベースのデータを含む、型指定されたデータセットを定義します。 このチュートリアルの後半では、Excel ブックプロジェクトとコンソールアプリケーションプロジェクトからこのデータセットを参照します。

 データセットは、AdventureWorksLT データベースの Product テーブルのデータを表す、*型指定*されたデータセットです。 型指定されたデータセットの詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

### <a name="to-define-a-typed-dataset-in-the-class-library-project"></a>クラスライブラリプロジェクトで型指定されたデータセットを定義するには

1. **ソリューションエクスプローラー**で、 **AdventureWorksDataSet**プロジェクトをクリックします。

2. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [**他の Windows** > **データソース**の**表示** > ] をクリックして表示します。

3. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード**を開始します。

4. **[データベース]** をクリックして、 **[次へ]** をクリックします。

5. AdventureWorksLT データベースへの既存の接続がある場合は、この接続を選択し、[**次へ**] をクリックします。

    それ以外の場合は、 **[新しい接続]** をクリックし、 **[接続の追加]** ダイアログ ボックスを使用して新しい接続を作成します。 詳細については、「[新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

6. **[アプリケーション構成ファイルへの接続文字列を保存]** ページで、 **[次へ]** をクリックします。

7. [**データベースオブジェクトの選択**] ページで、[**テーブル**] を展開し、[ **Product (saleslt)** ] を選択します。

8. **[完了]** をクリックします。

    *Adventureworksltdataset.xsd*ファイルが**AdventureWorksDataSet**プロジェクトに追加されます。 このファイルでは、次の項目を定義します。

   - `AdventureWorksLTDataSet`という名前の型指定されたデータセット。 このデータセットは、AdventureWorksLT データベース内の Product テーブルの内容を表します。

   - という名前`ProductTableAdapter`の TableAdapter。 この TableAdapter を使用して、の`AdventureWorksLTDataSet`データの読み取りと書き込みを行うことができます。 詳細については、「 [TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)」を参照してください。

     これらのオブジェクトは、どちらもこのチュートリアルの後半で使用します。

9. **ソリューションエクスプローラー**で、[ **AdventureWorksDataSet** ] を右クリックし、[**ビルド**] をクリックします。

     プロジェクトのビルドでエラーが発生しないことを確認します。

## <a name="create-an-excel-workbook-project"></a>Excel ブックプロジェクトを作成する
 データへのインターフェイスの Excel ブックプロジェクトを作成します。 このチュートリアルの後半では、データを<xref:Microsoft.Office.Tools.Excel.ListObject>表示するを作成し、データセットのインスタンスをブックのデータキャッシュに追加します。

### <a name="to-create-the-excel-workbook-project"></a>Excel ブックプロジェクトを作成するには

1. **ソリューションエクスプローラー**で、 **AdventureWorksDataSet**ソリューションを右クリックし、[**追加**] をポイントして、[**新しいプロジェクト**] をクリックします。

2. [テンプレート] ペインで、 **[ C#ビジュアル**] または [ **Visual Basic**] を展開し、[ **Office**] を展開します。

3. 展開された**Office**ノードの下で、[ **2010** ] ノードを選択します。

4. プロジェクトテンプレートの一覧で、Excel ブックプロジェクトを選択します。

5. [**名前**] ボックスに「 **AdventureWorksReport**」と入力します。 場所は変更しないでください。

6. **[OK]** をクリックします。

     **Visual Studio Tools for Office プロジェクト ウィザード** が開きます。

7. [**新しいドキュメントを作成**する] が選択されていることを確認し、[ **OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]デザイナーで**AdventureWorksReport**ブックを開き、**ソリューションエクスプローラー**に**AdventureWorksReport**プロジェクトを追加します。

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>Excel ブックプロジェクトのデータソースにデータセットを追加する
 Excel ブックでデータセットを表示するには、まず、Excel ブックプロジェクトのデータソースにデータセットを追加する必要があります。

### <a name="to-add-the-dataset-to-the-data-sources-in-the-excel-workbook-project"></a>Excel ブックプロジェクトのデータソースにデータセットを追加するには

1. **ソリューションエクスプローラー**で、 **AdventureWorksReport**プロジェクトの下にある**Sheet1.cs**または**Sheet1**をダブルクリックします。

     デザイナーでブックが開きます。

2. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

     **データ ソース構成ウィザード**が開きます。

3. [**オブジェクト**] をクリックし、[**次へ**] をクリックします。

4. [**バインド先のオブジェクトを選択**してください] ページで、[**参照の追加**] をクリックします。

5. [**プロジェクト**] タブで、[ **AdventureWorksDataSet** ] をクリックし、[ **OK**] をクリックします。

6. **AdventureWorksDataSet**アセンブリの**AdventureWorksDataSet**名前空間で、[ **adventureworksltdataset.xsd** ] をクリックし、[**完了**] をクリックします。

     [**データソース**] ウィンドウが開き、 **adventureworksltdataset.xsd**がデータソースの一覧に追加されます。

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>データセットのインスタンスにバインドされた ListObject を作成する
 ブックにデータセットを表示するには、 <xref:Microsoft.Office.Tools.Excel.ListObject>データセットのインスタンスにバインドされたを作成します。 コントロールをデータにバインドする方法の詳細については、「[データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

### <a name="to-create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>データセットのインスタンスにバインドされた ListObject を作成するには

1. [**データソース**] ウィンドウで、[ **AdventureWorksDataSet**] の下の [ **adventureworksltdataset.xsd** ] ノードを展開します。

2. **Product**ノードを選択し、表示されるドロップダウン矢印をクリックして、ドロップダウンリストで [ **ListObject** ] を選択します。

     ドロップダウン矢印が表示されない場合は、ブックがデザイナーで開かれていることを確認します。

3. **Product**テーブルをセル A1 にドラッグします。

     という名前`productListObject`のコントロールがワークシートに作成され、セルA1から開始されます。<xref:Microsoft.Office.Tools.Excel.ListObject> 同時に、 `adventureWorksLTDataSet` という名前のデータセット オブジェクトと、 <xref:System.Windows.Forms.BindingSource> という名前の `productBindingSource` がプロジェクトに追加されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> が <xref:System.Windows.Forms.BindingSource>にバインドされ、さらにこれがデータセット オブジェクトにバインドされます。

## <a name="add-the-dataset-to-the-data-cache"></a>データセットをデータキャッシュに追加する
 Excel ブックプロジェクトの外部にあるコードで、ブック内のデータセットにアクセスできるようにするには、データセットをデータキャッシュに追加する必要があります。 データキャッシュの詳細については、「[ドキュメントレベルのカスタマイズでのキャッシュデータ](../vsto/cached-data-in-document-level-customizations.md)」と「[データのキャッシュ](../vsto/caching-data.md)」を参照してください。

### <a name="to-add-the-dataset-to-the-data-cache"></a>データセットをデータキャッシュに追加するには

1. デザイナーで、[ **adventureworksltdataset.xsd**] をクリックします。

2. [**プロパティ**] ウィンドウで、[**修飾子**] プロパティを [**パブリック**] に設定します。

3. **CacheInDocument**プロパティを**True**に設定します。

## <a name="initialize-the-dataset-in-the-workbook"></a>ブック内のデータセットを初期化します
 コンソールアプリケーションを使用してキャッシュされたデータセットからデータを取得するには、まず、キャッシュされたデータセットにデータを設定する必要があります。

### <a name="to-initialize-the-dataset-in-the-workbook"></a>ブック内のデータセットを初期化するには

1. **ソリューションエクスプローラー**で、 **Sheet1.cs**ファイルまたは**Sheet1**ファイルを右クリックし、[**コードの表示**] をクリックします。

2. `Sheet1_Startup` イベント ハンドラーを次のコードで置き換えます。 このコードでは、 **AdventureWorksDataSet**プロジェクト`ProductTableAdapter`で定義されているクラスのインスタンスを使用して、キャッシュされたデータセットにデータが格納されます (現在空の場合)。

     [!code-csharp[Trin_CachedDataWalkthroughs#8](../vsto/codesnippet/CSharp/AdventureWorksDataSet/AdventureWorksReport/Sheet1.cs#8)]
     [!code-vb[Trin_CachedDataWalkthroughs#8](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/AdventureWorksReport/Sheet1.vb#8)]

## <a name="checkpoint"></a>チェックポイント
 Excel ブックプロジェクトをビルドして実行し、エラーなしでコンパイルおよび実行されることを確認します。 この操作では、キャッシュされたデータセットがいっぱいになり、ブックにデータが保存されます。

### <a name="to-build-and-run-the-project"></a>プロジェクトをビルドして実行するには

1. **ソリューションエクスプローラー**で、 **AdventureWorksReport**プロジェクトを右クリックし、[**デバッグ**]、[**新しいインスタンスを開始**] の順にクリックします。

     プロジェクトがビルドされ、Excel でブックが開きます。 次のことを検証します。

    - は<xref:Microsoft.Office.Tools.Excel.ListObject>データを格納します。

    - の<xref:Microsoft.Office.Tools.Excel.ListObject>最初の行の**ListPrice**列の値は1431.5 です。 このチュートリアルの後半では、コンソールアプリケーションを使用して、 **ListPrice**列の値を変更します。

2. ブックを保存します。 ファイル名やブックの場所は変更しないでください。

3. Excel を終了します。

## <a name="create-a-console-application-project"></a>コンソールアプリケーションプロジェクトの作成
 ブック内のキャッシュされたデータセットのデータを変更するために使用するコンソールアプリケーションプロジェクトを作成します。

### <a name="to-create-the-console-application-project"></a>コンソールアプリケーションプロジェクトを作成するには

1. **ソリューションエクスプローラー**で、 **AdventureWorksDataSet**ソリューションを右クリックし、[**追加**] をポイントして、[**新しいプロジェクト**] をクリックします。

2. [**プロジェクトの種類**] ペインで、[  **C#ビジュアル**] または [ **Visual Basic**] を展開し、[ **Windows**] をクリックします。

3. [**テンプレート**] ペインで、[**コンソールアプリケーション**] を選択します。

4. [**名前**] ボックスに「 **datawriter**」と入力します。 場所は変更しないでください。

5. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**Datawriter**プロジェクトを**ソリューションエクスプローラー**に追加し、 **Program.cs**または module1.vb コードファイルを開きます。

## <a name="change-data-in-the-cached-dataset-by-using-the-console-application"></a>コンソールアプリケーションを使用してキャッシュされたデータセットのデータを変更する
 コンソールアプリケーションの`AdventureWorksLTDataSet` クラスを使用して、ローカルオブジェクトにデータを読み取り、このデータを変更して、キャッシュされたデータセットに保存し<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>直します。

### <a name="to-change-data-in-the-cached-dataset"></a>キャッシュされたデータセットのデータを変更するには

1. **ソリューションエクスプローラー**で、 **datawriter**プロジェクトを右クリックし、[**参照の追加**] をクリックします。

2. [ **.Net** ] タブで、[ **VisualStudio**] を選択します。

3. **[OK]** をクリックします。

4. **ソリューションエクスプローラー**で、 **datawriter**プロジェクトを右クリックし、[**参照の追加**] をクリックします。

5. [**プロジェクト**] タブで [ **AdventureWorksDataSet**] を選択し、[ **OK**] をクリックします。

6. コードエディターで*Program.cs*ファイルまたは module1.vb ファイルを開きます。

7. コードファイルの先頭に、 C#次の using (for) または**Imports** (for Visual Basic) ステートメント**を**追加します。

    [!code-csharp[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#1)]
    [!code-vb[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#1)]

8. `Main` メソッドに次のコードを追加します。 このコードは、次のオブジェクトを宣言します。

   - AdventureWorksDataSet プロジェクトで定義`AdventureWorksLTDataSet`されている型のインスタンス。

   - **AdventureWorksReport**プロジェクトの build フォルダー内の AdventureWorksReport ブックへのパス。

   - ブック内のデータキャッシュへのアクセスに使用するオブジェクト。<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>

     > [!NOTE]
     > 次のコードは、 *.xlsx*ファイル拡張子を持つブックを使用していることを前提としています。 プロジェクト内のブックのファイル拡張子が異なる場合は、必要に応じてパスを変更します。

     [!code-csharp[Trin_CachedDataWalkthroughs#6](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#6)]
     [!code-vb[Trin_CachedDataWalkthroughs#6](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#6)]

9. 前の手順で追加し`Main`たコードの後に、次のコードをメソッドに追加します。 このコードは次のタスクを実行します。

   - このメソッドは<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 、 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument>クラスのプロパティを使用して、ブック内のキャッシュされたデータセットにアクセスします。

   - キャッシュされたデータセットからローカルデータセットにデータを読み取ります。

   - これにより`ListPrice` 、データセットの product テーブル内の各製品の値が変更されます。

   - キャッシュされたデータセットへの変更をブックに保存します。

     [!code-csharp[Trin_CachedDataWalkthroughs#7](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#7)]
     [!code-vb[Trin_CachedDataWalkthroughs#7](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#7)]

10. **ソリューションエクスプローラー**で、 **datawriter**プロジェクトを右クリックして [**デバッグ**] をポイントし、[**新しいインスタンスを開始**] をクリックします。

     コンソールアプリケーションは、キャッシュされたデータセットをローカルデータセットに読み取り中にメッセージを表示し、ローカルデータセットの製品価格を変更して、キャッシュされたデータセットに新しい値を保存します。 Enterキーを押してアプリケーションを終了します。

## <a name="test-the-workbook"></a>ブックをテストする
 ブックを開くと、キャッシュさ<xref:Microsoft.Office.Tools.Excel.ListObject>れたデータセットのデータ`ListPrice`列に加えた変更がに表示されます。

### <a name="to-test-the-workbook"></a>ブックをテストするには

1. まだ開いている場合は、Visual Studio デザイナーで AdventureWorksReport ブックを閉じます。

2. **AdventureWorksReport**プロジェクトの build フォルダーにある AdventureWorksReport ブックを開きます。 既定では、ビルドフォルダーは次のいずれかの場所にあります。

    - *%UserProfile%\My Documents\AdventureWorksReport\bin\Debug*(Windows XP およびそれ以前のバージョンの場合)

    - *%UserProfile%\Documents\AdventureWorksReport\bin\Debug*(Windows Vista の場合)

3. の<xref:Microsoft.Office.Tools.Excel.ListObject>最初の行の**ListPrice**列の値が1574.65 になっていることを確認します。

4. ブックを閉じます。

## <a name="see-also"></a>関連項目

- [チュートリアル: サーバー上のブックにデータを挿入する](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)
