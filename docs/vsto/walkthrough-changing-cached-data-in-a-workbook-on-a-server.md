---
title: 'チュートリアル: サーバー上のブックでキャッシュされたデータを変更する'
description: ServerDocument クラスを使って、Microsoft Excel を起動することなく、Excel ブック内のキャッシュされたデータセットを変更する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f03175abb843abefe5266724890457c795369d63
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824433"
---
# <a name="walkthrough-change-cached-data-in-a-workbook-on-a-server"></a>チュートリアル: サーバー上のブックでキャッシュされたデータを変更する
  このチュートリアルでは、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使って、Microsoft Office Excel を起動することなく、Excel ブック内のキャッシュされたデータセットを変更する方法について説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 このチュートリアルでは、次の作業について説明します。

- AdventureWorksLT データベースのデータを格納したデータセットを定義する。

- Excel ブック プロジェクトとコンソール アプリケーション プロジェクトで、データセットのインスタンスを作成する。

- ブック内のデータセットにバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject> を作成し、ブックが開かれたときに <xref:Microsoft.Office.Tools.Excel.ListObject> にデータを設定する。

- ブック内のデータセットをデータ キャッシュに追加する。

- Excel を起動することなく、コンソール アプリケーション内でコードを実行して、キャッシュされたデータセット内のデータの列を変更する。

  このチュートリアルでは、開発用コンピューターでコードを実行することを前提としていますが、このチュートリアルで示すコードは、Excel がインストールされていないサーバーでも使用できます。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

- AdventureWorksLT サンプル データベースがアタッチされた、Microsoft SQL Server または Microsoft SQL Server Express の実行中のインスタンスへのアクセス権。 AdventureWorksLT データベースは、[SQL Server Samples GitHub リポジトリ](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)からダウンロードできます。 データベースをアタッチする方法について詳しくは、次のトピックをご覧ください。

  - SQL Server Management Studio または SQL Server Management Studio Express を使用してデータベースをアタッチする場合は、「[データベースをアタッチする方法 (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database)」を参照してください。

  - コマンド ラインを使用してデータベースをアタッチする場合は、「[データベース ファイルを SQL Server Express にアタッチする方法](/previous-versions/sql/)」を参照してください。

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>データセットを定義するクラス ライブラリ プロジェクトを作成する
 Excel ブック プロジェクトとコンソール アプリケーションで同じデータセットを使用するには、これら両方のプロジェクトによって参照される別のアセンブリにデータセットを定義する必要があります。 このチュートリアルでは、クラス ライブラリ プロジェクトにデータセットを定義します。

### <a name="to-create-the-class-library-project"></a>クラス ライブラリ プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows]** をクリックします。

4. プロジェクト テンプレートの一覧で **[クラス ライブラリ]** を選択します。

5. **[名前]** ボックスに「**AdventureWorksDataSet**」と入力します。

6. **[参照]** をクリックし、 *%UserProfile%\My Documents* (Windows XP 以前の場合) または *%UserProfile%\Documents* (Windows Vista の場合) フォルダーに移動して、 **[フォルダーの選択]** をクリックします。

7. **[新しいプロジェクト]** ダイアログ ボックスで、 **[ソリューションのディレクトリを作成する]** チェック ボックスがオフになっていることを確認します。

8. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**AdventureWorksDataSet** プロジェクトが **ソリューション エクスプローラー** に追加され、**Class1.cs** または **Class1.vb** コード ファイルが開きます。

9. **ソリューション エクスプローラー** で、**Class1.cs** または **Class1.vb** を右クリックし、 **[削除]** をクリックします。 このファイルは、このチュートリアルでは必要ありません。

## <a name="define-a-dataset-in-the-class-library-project"></a>クラス ライブラリ プロジェクトでデータセットを定義する
 SQL Server 2005 用の AdventureWorksLT データベースのデータを格納する、型指定されたデータセットを定義します。 このチュートリアルの後の方で、Excel ブック プロジェクトとコンソール アプリケーション プロジェクトから、このデータセットを参照します。

 このデータセットは、AdventureWorksLT データベースの Product テーブルのデータを表す、"*型指定されたデータセット*" です。 型指定されたデータセットの詳細については、「[Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

### <a name="to-define-a-typed-dataset-in-the-class-library-project"></a>クラス ライブラリ プロジェクトで型指定されたデータセットを定義するには

1. **ソリューション エクスプローラー** で、**AdventureWorksDataSet** プロジェクトをクリックします。

2. **[データ ソース]** ウィンドウが表示されていない場合は、メニュー バーで **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** をクリックして表示します。

3. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

4. **[データベース]** をクリックして、 **[次へ]** をクリックします。

5. AdventureWorksLT データベースへの既存の接続がある場合は、その接続を選んで **[次へ]** をクリックします。

    それ以外の場合は、 **[新しい接続]** をクリックし、 **[接続の追加]** ダイアログ ボックスを使用して新しい接続を作成します。 詳細については、「[新しい接続を追加する](../data-tools/add-new-connections.md)」を参照してください。

6. **[アプリケーション構成ファイルへの接続文字列を保存]** ページで、 **[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、 **[Product (SalesLT)]** を選びます。

8. **[完了]** をクリックします。

    *AdventureWorksLTDataSet.xsd* ファイルが **AdventureWorksDataSet** プロジェクトに追加されます。 このファイルでは、次の項目を定義します。

   - `AdventureWorksLTDataSet`という名前の型指定されたデータセット。 このデータセットは、AdventureWorksLT データベースの Product テーブルの内容を表します。

   - `ProductTableAdapter` という名前の TableAdapter。 この TableAdapter は、`AdventureWorksLTDataSet` 内のデータの読み取りと書き込みに使用できます。 詳細については、「[TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)」を参照してください。

     これらのオブジェクトは、どちらもこのチュートリアルの後半で使用します。

9. **ソリューション エクスプローラー** で、**AdventureWorksDataSet** を右クリックし、 **[ビルド]** をクリックします。

     プロジェクトのビルドでエラーが発生しないことを確認します。

## <a name="create-an-excel-workbook-project"></a>Excel ブック プロジェクトを作成する
 データへのインターフェイス用の Excel ブック プロジェクトを作成します。 このチュートリアルの後の方で、データを表示する <xref:Microsoft.Office.Tools.Excel.ListObject> を作成し、データセットのインスタンスをブックのデータ キャッシュに追加します。

### <a name="to-create-the-excel-workbook-project"></a>Excel ブック プロジェクトを作成するには

1. **ソリューション エクスプローラー** で、**AdventureWorksDataSet** ソリューションを右クリックし、 **[追加]** をポイントして、 **[新しいプロジェクト]** をクリックします。

2. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office]** を展開します。

3. 展開した **[Office]** ノードの下で、 **[2010]** ノードを選択します。

4. プロジェクト テンプレートのリストで、[Excel ブック] プロジェクトを選択します。

5. **[名前]** ボックスに「**AdventureWorksReport**」と入力します。 場所は変更しないでください。

6. **[OK]** をクリックします。

     **Visual Studio Tools for Office プロジェクト ウィザード** が開きます。

7. **[新しいドキュメントの作成]** が選択されていることを確認し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**AdventureWorksReport** ブックがデザイナーで開かれ、**AdventureWorksReport** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>Excel ブック プロジェクトのデータ ソースにデータセットを追加する
 Excel ブックでデータセットを表示するには、まず、Excel ブック プロジェクトのデータ ソースにデータセットを追加する必要があります。

### <a name="to-add-the-dataset-to-the-data-sources-in-the-excel-workbook-project"></a>Excel ブック プロジェクトのデータ ソースにデータセットを追加するには

1. **ソリューション エクスプローラー** で、**AdventureWorksReport** プロジェクトの **Sheet1.cs** または **Sheet1.vb** をダブルクリックします。

     デザイナーでブックが開きます。

2. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

     **データ ソース構成ウィザード** が開きます。

3. **[オブジェクト]** をクリックし、 **[次へ]** をクリックします。

4. **[バインド先のオブジェクトを選択します]** ページで、 **[参照の追加]** をクリックします。

5. **[プロジェクト]** タブで、**AdventureWorksDataSet** をクリックし、 **[OK]** をクリックします。

6. **AdventureWorksDataSet** アセンブリの **AdventureWorksDataSet** 名前空間で、**AdventureWorksLTDataSet** をクリックし、 **[完了]** をクリックします。

     **[データ ソース]** ウィンドウが開き、**AdventureWorksLTDataSet** がデータ ソースの一覧に追加されます。

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>データセットのインスタンスにバインドされた ListObject を作成する
 ブックにデータセットを表示するには、データセットのインスタンスにバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject> を作成します。 コントロールをデータにバインドする操作の詳細については、「[Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

### <a name="to-create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>データセットのインスタンスにバインドされた ListObject を作成するには

1. **[データ ソース]** ウィンドウで、 **[AdventureWorksDataSet]** の下の **[AdventureWorksLTDataSet]** ノードを展開します。

2. **[Product]** ノードを選択し、表示されるドロップダウン矢印をクリックして、ドロップダウン リストから **[ListObject]** を選択します。

     ドロップダウン矢印が表示されない場合は、デザイナーでブックが開かれていることを確認します。

3. **Product** テーブルをセル A1 にドラッグします。

     `productListObject` という名前の <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールがワークシートに作成されます (開始位置は セル A1)。 同時に、 `adventureWorksLTDataSet` という名前のデータセット オブジェクトと、 <xref:System.Windows.Forms.BindingSource> という名前の `productBindingSource` がプロジェクトに追加されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> が <xref:System.Windows.Forms.BindingSource>にバインドされ、さらにこれがデータセット オブジェクトにバインドされます。

## <a name="add-the-dataset-to-the-data-cache"></a>データセットをデータ キャッシュに追加する
 Excel ブック プロジェクトの外部にあるコードからブック内のデータセットにアクセスできるようにするには、データセットをデータ キャッシュに追加する必要があります。 データ キャッシュの詳細については、「[ドキュメント レベルのカスタマイズのキャッシュ データ](../vsto/cached-data-in-document-level-customizations.md)」と「[キャッシュ データ](../vsto/caching-data.md)」を参照してください。

### <a name="to-add-the-dataset-to-the-data-cache"></a>データセットをデータ キャッシュに追加するには

1. デザイナーで、 **[adventureWorksLTDataSet]** をクリックします。

2. **[プロパティ]** ウィンドウで、**Modifiers** プロパティを **Public** に設定します。

3. **CacheInDocument** プロパティを **True** に設定します。

## <a name="initialize-the-dataset-in-the-workbook"></a>ブック内のデータセットを初期化する
 コンソール アプリケーションを使用してキャッシュされたデータセットからデータを取得するには、まず、キャッシュされたデータセットにデータを設定する必要があります。

### <a name="to-initialize-the-dataset-in-the-workbook"></a>ブック内のデータセットを初期化するには

1. **ソリューション エクスプローラー** で、**Sheet1.cs** または **Sheet1.vb** ファイルを右クリックし、 **[コードの表示]** をクリックします。

2. `Sheet1_Startup` イベント ハンドラーを次のコードで置き換えます。 このコードでは、**AdventureWorksDataSet** プロジェクトで定義されている `ProductTableAdapter` クラスのインスタンスを使って、キャッシュされたデータセットにデータが格納されます (現在空の場合)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/AdventureWorksReport/Sheet1.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/AdventureWorksReport/Sheet1.vb" id="Snippet8":::

## <a name="checkpoint"></a>Checkpoint
 Excel ブック プロジェクトをビルドして実行し、エラーなくコンパイルされて実行されることを確認します。 この操作により、キャッシュされたデータセットにデータが設定され、データがブックに保存されます。

### <a name="to-build-and-run-the-project"></a>プロジェクトをビルドして実行するには

1. **ソリューション エクスプローラー** で、**AdventureWorksReport** プロジェクトを右クリックし、 **[デバッグ]** を選択して、 **[新しいインスタンスを開始]** をクリックします。

     プロジェクトがビルドされ、Excel でブックが開きます。 次の点を確認します。

    - <xref:Microsoft.Office.Tools.Excel.ListObject> にデータが設定されている。

    - <xref:Microsoft.Office.Tools.Excel.ListObject> の最初の行の **ListPrice** 列の値が 1431.5 である。 このチュートリアルの後の方で、コンソール アプリケーションを使って **ListPrice** 列の値を変更します。

2. ブックを保存します。 ファイル名やブックの場所は変更しないでください。

3. Excel を終了します。

## <a name="create-a-console-application-project"></a>コンソール アプリケーション プロジェクトを作成する
 ブック内のキャッシュされたデータセットのデータを変更するために使用する、コンソール アプリケーション プロジェクトを作成します。

### <a name="to-create-the-console-application-project"></a>コンソール アプリケーション プロジェクトを作成するには

1. **ソリューション エクスプローラー** で、**AdventureWorksDataSet** ソリューションを右クリックし、 **[追加]** をポイントして、 **[新しいプロジェクト]** をクリックします。

2. **[プロジェクトの種類]** ペインで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows]** をクリックします。

3. **[テンプレート]** ペインで **[コンソール アプリケーション]** をクリックします。

4. **[名前]** ボックスに「**DataWriter**」と入力します。 場所は変更しないでください。

5. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**DataWriter** プロジェクトが **ソリューション エクスプローラー** に追加され、**Program.cs** または **Module1.vb** コード ファイルが開かれます。

## <a name="change-data-in-the-cached-dataset-by-using-the-console-application"></a>コンソール アプリケーションを使用してキャッシュされたデータセットのデータを変更する
 コンソール アプリケーションの <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使用して、ローカルの `AdventureWorksLTDataSet` オブジェクトにデータを読み込み、このデータを変更してから、キャッシュされたデータセットに保存し直します。

### <a name="to-change-data-in-the-cached-dataset"></a>キャッシュされたデータセットのデータを変更するには

1. **ソリューション エクスプローラー** で、**DataWriter** プロジェクトを右クリックし、 **[参照の追加]** をクリックします。

2. **[.NET]** タブで、**Microsoft.VisualStudio.Tools.Applications** を選択します。

3. **[OK]** をクリックします。

4. **ソリューション エクスプローラー** で、**DataWriter** プロジェクトを右クリックし、 **[参照の追加]** をクリックします。

5. **[プロジェクト]** タブで、**AdventureWorksDataSet** を選択し、 **[OK]** をクリックします。

6. コード エディターで、*Program.cs* または *Module1.vb* ファイルを開きます。

7. コード ファイルの先頭に、次の **using** (C# の場合) または **Imports** (Visual Basic の場合) ステートメントを追加します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet1":::

8. `Main` メソッドに次のコードを追加します。 このコードでは、次のオブジェクトを宣言しています。

   - **AdventureWorksDataSet** プロジェクトで定義されている `AdventureWorksLTDataSet` 型のインスタンス。

   - **AdventureWorksReport** プロジェクトのビルド フォルダー内にある AdventureWorksReport ブックへのパス。

   - ブック内のデータ キャッシュへのアクセスに使用する <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> オブジェクト。

     > [!NOTE]
     > 次のコードでは、ファイル拡張子が *.xlsx* のブックを使用していることを前提としています。 プロジェクト内のブックのファイル拡張子が異なる場合は、必要に応じてパスを変更してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet6":::

9. `Main` メソッド (前の手順で追加したコードの後) に、次のコードを追加します。 このコードは、以下のタスクを実行します。

   - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスの <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> プロパティを使用して、ブック内のキャッシュされたデータセットにアクセスします。

   - キャッシュされたデータセットからローカル データセットにデータを読み取ります。

   - データセットの Product テーブル内の各製品の `ListPrice` 値を変更します。

   - ブック内のキャッシュされたデータセットに変更を保存します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet7":::

10. **ソリューション エクスプローラー** で、**DataWriter** プロジェクトを右クリックし、 **[デバッグ]** をポイントして、 **[新しいインスタンスを開始]** をクリックします。

     コンソール アプリケーションは、キャッシュされたデータセットをローカル データセットに読み込み、ローカル データセットの製品価格を変更し、キャッシュされたデータセットに新しい値を保存するときに、メッセージを表示します。 **Enter** キーを押してアプリケーションを閉じます。

## <a name="test-the-workbook"></a>ブックをテストする
 これで、ブックを開いたときに、キャッシュされたデータセットのデータの `ListPrice` 列に加えた変更が <xref:Microsoft.Office.Tools.Excel.ListObject> に表示されるようになりました。

### <a name="to-test-the-workbook"></a>ブックをテストするには

1. Visual Studio デザイナーで AdventureWorksReport ブックを閉じます (まだ開いている場合)。

2. **AdventureWorksReport** プロジェクトのビルド フォルダー内にある AdventureWorksReport ブックを開きます。 既定では、ビルド フォルダーは次のいずれかの場所にあります。

    - *%UserProfile%\My Documents\AdventureWorksReport\bin\Debug* (Windows XP 以前の場合)

    - *%UserProfile%\Documents\AdventureWorksReport\bin\Debug* (Windows Vista の場合)

3. <xref:Microsoft.Office.Tools.Excel.ListObject> の最初の行の **ListPrice** 列の値が 1574.65 になっていることを確認します。

4. ブックを閉じます。

## <a name="see-also"></a>関連項目

- [チュートリアル: サーバー上のブックにデータを挿入する](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)
