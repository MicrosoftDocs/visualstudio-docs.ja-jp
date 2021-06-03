---
title: 'チュートリアル: ドキュメント レベルのプロジェクトでの複合データ バインディング'
description: Microsoft Excel ワークシートの複数のセルを Northwind SQL Server データベースのフィールドにバインドする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
- multiple column data binding [Office development in Visual Studio]
- data binding [Office development in Visual Studio], multiple columns
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a85f46cf9c234ad662966372a8d014ae0f98be84
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826370"
---
# <a name="walkthrough-complex-data-binding-in-a-document-level-project"></a>チュートリアル: ドキュメント レベルのプロジェクトでの複合データ バインディング
  このチュートリアルでは、ドキュメント レベルのプロジェクトにおける複合データ バインディングの基本について説明します。 Microsoft Office Excel ワークシートの複数のセルを Northwind SQL Server データベースのフィールドにバインドできます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- ブック プロジェクトにデータ ソースを追加する。

- ワークシートにデータ バインドされたコントロールを追加する。

- データの変更を取得元のデータベースに保存する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプル データベースがあるサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みのアクセス許可。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 まず、Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Complex Data Binding** という名前で Excel ブック プロジェクトを作成します。 ウィザードで、 **[新しいドキュメントの作成]** を選択します。

     詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Complex Data Binding** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="create-the-data-source"></a>データ ソースを作成する
 **[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. **[データ ソース]** ウィンドウが表示されていない場合は、メニュー バーで **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. **[データベース]** を選択し、 **[次へ]** をクリックします。

4. SQL Server の Northwind サンプル データベースへのデータ接続を選択するか、または **[新しい接続]** ボタンを使用して新しい接続を追加します。

5. 接続を選択または作成したら、 **[次へ]** をクリックします。

6. 接続を保存するオプションがオンになっている場合は、それをオフにして、 **[次へ]** をクリックします。

7. **[データベース オブジェクト]** ウィンドウで、 **[Tables]** ノードを展開します。

8. **Employees** テーブルの隣にあるチェック ボックスをオンにします。

9. **[完了]** をクリックします。

   ウィザードによって、**Employees** テーブルが **[データ ソース]** ウィンドウに追加されます。 また、**ソリューション エクスプローラー** に表示される、型指定されたデータセットがプロジェクトに追加されます。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 ブックを開くと、ワークシートに **Employees** テーブルが表示されます。 ユーザーは、データに変更を加えた後、ボタンをクリックすることによって、変更をデータベースに保存し直すことができます。

 ワークシートをテーブルに自動的にバインドするには、 **[データ ソース]** ウィンドウからワークシートに <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを追加します。 変更を保存するためのオプションをユーザーに付与するには、**ツールボックス** から <xref:System.Windows.Forms.Button> コントロールを追加します。

#### <a name="to-add-a-list-object"></a>リスト オブジェクトを追加するには

1. **My Complex Data Binding.xlsx** ブックが Visual Studio デザイナーで開かれ、**Sheet1** が表示されていることを確認します。

2. **[データ ソース]** ウィンドウを開き、 **[Employees]** ノードを選択します。

3. 表示されるドロップダウン矢印をクリックします。

4. ドロップダウン リストで **[ListObject]** を選択します。

5. **Employees** テーブルをセル **A6** にドラッグします。

     `EmployeesListObject` という名前の <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールがセル **A6** に作成されます。 同時に、`EmployeesBindingSource` という名前の <xref:System.Windows.Forms.BindingSource>、テーブル アダプター、および <xref:System.Data.DataSet> インスタンスがプロジェクトに追加されます。 コントロールは <xref:System.Windows.Forms.BindingSource> にバインドされ、さらにこれが <xref:System.Data.DataSet> インスタンスにバインドされます。

### <a name="to-add-a-button"></a>ボタンを追加するには

1. **[ツールボックス]** の **[コモン コントロール]** タブから、<xref:System.Windows.Forms.Button> コントロールをワークシートのセル **A4** に追加します。

   次の手順では、ワークシートが開いたときにボタンにテキストを追加します。

## <a name="initialize-the-control"></a>コントロールを初期化する
 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベント ハンドラーのボタンにテキストを追加します。

### <a name="to-initialize-the-control"></a>コントロールを初期化するには

1. **ソリューション エクスプローラー** で **Sheet1.vb** または **Sheet1.cs** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. 次のコードを `Sheet1_Startup` メソッドに追加して、b`utton` のテキストを設定します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs" id="Snippet8":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb" id="Snippet8":::

3. C# の場合のみ、<xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを `Sheet1_Startup` メソッドに追加します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs" id="Snippet9":::

   次に、ボタンの <xref:System.Windows.Forms.Control.Click> イベントを処理するコードを追加します。

## <a name="save-changes-to-the-database"></a>変更をデータベースに保存する
 データに加えられた変更は、明示的にデータベースに保存し直されるまで、ローカル データセットにのみ存在します。

### <a name="to-save-changes-to-the-database"></a>変更をデータベースに保存するには

1. `button` の <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを追加し、次のコードを追加して、データセットに加えられたすべての変更をコミットしてデータベースに戻します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb" id="Snippet10":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ブックをテストして、データが想定どおりに表示されること、およびリスト オブジェクト内のデータを操作できることを確認しましょう。

### <a name="to-test-the-data-binding"></a>データ バインディングをテストするには

- **F5** キーを押します。

     ブックが開いたときに、リスト オブジェクトに **Employees** テーブルのデータが格納されていることを確認します。

### <a name="to-modify-data"></a>データを変更するには

1. セル **B7** をクリックします。**Davolio** という名前が含まれているはずです。

2. **Anderson** という名前を入力し、**Enter** キーを押します。

### <a name="to-modify-a-column-header"></a>列ヘッダーを変更するには

1. **LastName** という列ヘッダーが含まれているセルをクリックします。

2. 2 つの単語の間にスペースを含めて「**Last Name**」と入力し、**Enter** キーを押します。

### <a name="to-save-data"></a>データを保存するには

1. ワークシート上の **[保存]** をクリックします。

2. Excel を終了します。 加えた変更を保存するかどうかを確認するメッセージが表示されたら、 **[いいえ]** をクリックします。

3. **F5** キーを押してプロジェクトをもう一度実行します。

     リスト オブジェクトには、**Employees** テーブルのデータが格納されています。

4. セル **B7** の名前は **Anderson** のままであることに注目してください。これは、変更を加えてデータベースに保存し直したデータです。 列ヘッダー **LastName** は、スペースを含まない元の形式に戻っています。これは、列ヘッダーがデータベースにバインドされておらず、ワークシートに加えた変更の保存も行わなかったためです。

### <a name="to-add-new-rows"></a>新しい行を追加するには

1. リスト オブジェクト内のセルを選択します。

    新しい行がリストの一番下に表示され、新しい行の最初のセルにアスタリスク ( **\*** ) が付いています。

2. 空の行に次の情報を追加します。

   |EmployeeID|LastName|FirstName|タイトル|
   |----------------|--------------|---------------|-----------|
   |10|Ito|Shu|営業マネージャー|

### <a name="to-delete-rows"></a>行を削除するには

- ワークシートの左端にある番号 16 (行 16) を右クリックし、 **[削除]** をクリックします。

### <a name="to-sort-the-rows-in-the-list"></a>リスト内の行を並べ替えるには

1. リスト内のセルを選択します。

     各列ヘッダーに矢印ボタンが表示されます。

2. **Last Name** 列ヘッダーの矢印ボタンをクリックします。

3. **[昇順で並べ替え]** をクリックします。

     姓のアルファベット順に行が並べ替えられます。

### <a name="to-filter-information"></a>情報をフィルター処理するには

1. リスト内のセルを選択します。

2. **Title** 列ヘッダーの矢印ボタンをクリックします。

3. **[Sales Representative]** をクリックします。

     リストには、**Title** 列に "**Sales Representative**" と表示されている行のみが表示されます。

4. **Title** 列ヘッダーの矢印ボタンをもう一度クリックします。

5. **[(すべて)]** をクリックします。

     フィルター処理が削除され、すべての行が表示されます。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、データベースのテーブルをリスト オブジェクトにバインドする方法の基本について説明しました。 ここでは、次の作業を行います。

- データをキャッシュして、オフラインで使用できるようにする。 詳細については、「[方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)」を参照してください。

- ソリューションを展開する。 詳細については、「[Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)」を参照してください。

- フィールドとテーブルの間にマスター/詳細関係を作成する。 詳細については、「[チュートリアル: キャッシュされたデータセットを使用してマスター詳細関係を作成する](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office ソリューションにおけるデータ](../vsto/data-in-office-solutions.md)
- [チュートリアル: ドキュメント レベルのプロジェクトでの単純データ バインディング](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
