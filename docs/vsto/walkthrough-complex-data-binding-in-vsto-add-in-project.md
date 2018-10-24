---
title: 'チュートリアル: VSTO アドイン プロジェクトで複雑なデータ バインディング'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], Excel
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: da2ddc582c6555e8ec4567f4faace603f6f0f677
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872487"
---
# <a name="walkthrough-complex-data-binding-in-vsto-add-in-project"></a>チュートリアル: VSTO アドイン プロジェクトで複雑なデータ バインディング
  VSTO アドイン プロジェクトでは、ホスト コントロールと Windows フォーム コントロールにデータをバインドできます。 このチュートリアルでは、Microsoft Office Excel ワークシートにコントロールを追加して、そのコントロールを実行時にデータにバインドする方法を示します。

 [!INCLUDE[appliesto_xlallapp](../vsto/includes/appliesto-xlallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- 追加、<xref:Microsoft.Office.Tools.Excel.ListObject>コントロールをワークシートに実行時にします。

- コントロールをデータセットのインスタンスに接続する <xref:System.Windows.Forms.BindingSource> を作成する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

-   `AdventureWorksLT` サンプル データベースがアタッチされた SQL Server 2005 または SQL Server 2005 Express の実行中のインスタンスへのアクセス。 ダウンロードすることができます、`AdventureWorksLT`からデータベース、 [CodePlex web サイト](http://go.microsoft.com/fwlink/?LinkId=115611)します。 データベースをアタッチする方法について詳しくは、次のトピックをご覧ください。

    -   データベースをアタッチするには、SQL Server Management Studio または SQL Server Management Studio Express を使用して、参照してください。[方法: データベース (SQL Server Management Studio) をアタッチする](http://msdn.microsoft.com/b4efb0ae-cfe6-4d81-a4b4-6e4916885caa)します。

    -   コマンドラインを使用してデータベースをアタッチする、次を参照してください。[方法: SQL Server Express データベース ファイルを添付](http://msdn.microsoft.com/0f8e42b5-7a8c-4c30-8c98-7d2bdc8dcc68)。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 まず、Excel VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1.  Visual Basic または C# を使用して、 **Populating Worksheets from a Database**という名前の Excel VSTO アドイン プロジェクトを作成します。

     詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio により、 `ThisAddIn.vb` ファイルまたは `ThisAddIn.cs` ファイルが開かれ、 **Populating Worksheets from a Database** プロジェクトが **ソリューション エクスプローラー**に追加されます。

## <a name="create-a-data-source"></a>データ ソースの作成
 **[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-add-a-typed-dataset-to-the-project"></a>型指定されたデータセットをプロジェクトに追加するには

1. 場合、**データソース**ウィンドウが表示されない、メニュー バーで 表示することによって、**ビュー** > **その他の Windows**  >  **データ ソース**します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード**を開始します。

3. **[データベース]** をクリックして、 **[次へ]** をクリックします。

4. `AdventureWorksLT` データベースへの既存の接続がある場合は、その接続を選んで **[次へ]** をクリックします。

    それ以外の場合は、 **[新しい接続]** をクリックし、 **[接続の追加]** ダイアログ ボックスを使用して新しい接続を作成します。 詳細については、次を参照してください。[新しい接続を追加](../data-tools/add-new-connections.md)します。

5. **[アプリケーション構成ファイルへの接続文字列を保存]** ページで、 **[次へ]** をクリックします。

6. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、 **[Address (SalesLT)]** を選びます。

7. **[完了]** をクリックします。

    *AdventureWorksLTDataSet.xsd*ファイルに追加されます**ソリューション エクスプ ローラー**します。 このファイルでは、次の項目を定義します。

   - `AdventureWorksLTDataSet`という名前の型指定されたデータセット。 このデータセットは、AdventureWorksLT データベースの **Address (SalesLT)** テーブルの内容を表します。

   - という名前の TableAdapter`AddressTableAdapter`します。 この TableAdapter データを読み書きするために使用できます、`AdventureWorksLTDataSet`します。 詳細については、次を参照してください。 [TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)します。

     これらのオブジェクトは、どちらもこのチュートリアルの後半で使用します。

## <a name="create-controls-and-bind-controls-to-data"></a>コントロールを作成し、データ コントロールをバインド
 このチュートリアルでは、ユーザーがブックを開くとすぐに、事前に選んでおいたテーブル内のすべてのデータが <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールによって表示されます。 リスト オブジェクトは <xref:System.Windows.Forms.BindingSource> を使用してコントロールをデータベースに接続します。

 データ バインド コントロールの詳細については、次を参照してください。 [Office ソリューションでのコントロールにデータをバインド](../vsto/binding-data-to-controls-in-office-solutions.md)します。

### <a name="to-add-the-list-object-dataset-and-table-adapter"></a>リスト オブジェクト、データセット、テーブル アダプターを追加するには

1.  `ThisAddIn` クラスで、次のコントロールを宣言し、 `Address` データセットの `AdventureWorksLTDataSet` テーブルを表示するようにします。

     [!code-csharp[Trin_ExcelAddInDatabase#1](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_ExcelAddInDatabase#1](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#1)]

2.  `ThisAddIn_Startup` メソッドに次のコードを追加し、データセットを初期化して、そのデータセットに `AdventureWorksLTDataSet` データセットから得た情報を設定します。

     [!code-csharp[Trin_ExcelAddInDatabase#2](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#2)]
     [!code-vb[Trin_ExcelAddInDatabase#2](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#2)]

3.  `ThisAddIn_Startup` メソッドに次のコードを追加します。 これによりホスト項目が生成され、ワークシートの機能が拡張されます。 詳細については、次を参照してください。[拡張 Word 文書や Excel ブックを実行時に VSTO アドインで](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)します。

     [!code-csharp[Trin_ExcelAddInDatabase#3](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#3)]
     [!code-vb[Trin_ExcelAddInDatabase#3](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#3)]

4.  範囲を作成して <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを追加します。

     [!code-csharp[Trin_ExcelAddInDatabase#4](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#4)]
     [!code-vb[Trin_ExcelAddInDatabase#4](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#4)]

5.  `AdventureWorksLTDataSet` を使用して、リスト オブジェクトを <xref:System.Windows.Forms.BindingSource>にバインドします。 リスト オブジェクトにバインドする列の名前を渡します。

     [!code-csharp[Trin_ExcelAddInDatabase#5](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#5)]
     [!code-vb[Trin_ExcelAddInDatabase#5](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#5)]

## <a name="test-the-add-in"></a>アドインのテストします。
 Excel を開くと、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールにより `Address` データセットの `AdventureWorksLTDataSet` テーブルから得られるデータが表示されます。

### <a name="to-test-the-vsto-add-in"></a>VSTO アドインをテストするには

-   **F5**キーを押します。

     <xref:Microsoft.Office.Tools.Excel.ListObject> という名前の `addressListObject` コントロールがワークシートに作成されます。 同時に、 `adventureWorksLTDataSet` という名前のデータセット オブジェクトと、 <xref:System.Windows.Forms.BindingSource> という名前の `addressBindingSource` がプロジェクトに追加されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> が <xref:System.Windows.Forms.BindingSource>にバインドされ、さらにこれがデータセット オブジェクトにバインドされます。

## <a name="see-also"></a>関連項目

- [Office ソリューションにおけるデータ](../vsto/data-in-office-solutions.md)
- [Office ソリューションでのコントロールにデータをバインドします。](../vsto/binding-data-to-controls-in-office-solutions.md)
- [方法: データベースからデータをワークシートに読み込む](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [方法: データベースからデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [方法: データ サービスからドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)
- [方法: オブジェクトからのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [方法: ワークシート内のデータベース レコードをスクロール](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)
- [方法: ホスト コントロールからのデータでデータ ソースを更新](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [チュートリアル: ドキュメント レベルのプロジェクトでの単純なデータ バインディング](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
- [チュートリアル: ドキュメント レベルのプロジェクトで複雑なデータ バインディング](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
- [Office ソリューションの概要でのローカル データベース ファイルを使用します。](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Office ソリューションの概要でのローカル データベース ファイルを使用します。](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)