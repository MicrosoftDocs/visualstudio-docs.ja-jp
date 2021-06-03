---
title: キャッシュされたデータセットを使用してマスター/詳細関係を作成する
description: ワークシート上にマスター/詳細関係を作成して、ソリューションをオフラインで使用できるようにデータをキャッシュする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- master-detail tables [Office development in Visual Studio], walkthroughs
- data caching [Office development in Visual Studio], Master/Detail Relation
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 177b21e2278153693601adf7b7dc18b751cf184e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824849"
---
# <a name="walkthrough-create-a-master-detail-relation-using-a-cached-dataset"></a>チュートリアル: キャッシュされたデータセットを使用してマスター/詳細関係を作成する
  このチュートリアルでは、ワークシート上にマスター/詳細関係を作成して、ソリューションをオフラインで使用できるようにデータをキャッシュする方法について説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- ワークシートにコントロールを追加する。

- ワークシートにキャッシュするデータセットを設定する。

- レコードのスクロールを有効にするコードを追加する。

- プロジェクトをテストする。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプル データベースへのアクセス。 データベースは、開発用コンピューターまたはサーバー上に配置できます。

- SQL Server データベースに対する読み取りと書き込みのアクセス許可。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 この手順では、Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. Visual Basic または C# のいずれかを使用して、**My Master-Detail** という名前の Excel ブック プロジェクトを作成します。 **[新しいドキュメントの作成]** が選択されていることを確認してください。 詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

   Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Master-Detail** プロジェクトが **ソリューション エクスプローラー** に追加されます。

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

8. **Orders** テーブルと **Order Details** テーブルを選択します。

9. **[完了]** をクリックします。

   ウィザードによって、2 つのテーブルが **[データ ソース]** ウィンドウに追加されます。 また、**ソリューション エクスプローラー** に表示される、型指定されたデータセットがプロジェクトに追加されます。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 この手順では、名前付き範囲、リスト オブジェクト、および 2 つのボタンを最初のワークシートに追加します。 まず、 **[データ ソース]** ウィンドウから名前付き範囲とリスト オブジェクトを追加して、データ ソースに自動的にバインドされるようにします。 次に、**ツールボックス** からボタンを追加します。

### <a name="to-add-a-named-range-and-a-list-object"></a>名前付き範囲とリスト オブジェクトを追加するには

1. **My Master-Detail.xlsx** ブックが Visual Studio デザイナーで開かれ、**Sheet1** が表示されていることを確認します。

2. **[データ ソース]** ウィンドウを開き、 **[Orders]** ノードを展開します。

3. **[OrderID]** 列を選択し、表示されるドロップダウン矢印をクリックします。

4. ドロップダウン リストで **[NamedRange]** をクリックし、 **[OrderID]** 列をセル **A2** にドラッグします。

     `OrderIDNamedRange` という名前の <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールがセル **A2** に作成されます。 同時に、`OrdersBindingSource` という名前の <xref:System.Windows.Forms.BindingSource>、テーブル アダプター、および <xref:System.Data.DataSet> インスタンスがプロジェクトに追加されます。 コントロールは <xref:System.Windows.Forms.BindingSource> にバインドされ、さらにこれが <xref:System.Data.DataSet> インスタンスにバインドされます。

5. **Orders** テーブルの下にある列の末尾までスクロールします。 一覧の一番下に **Order Details** テーブルがあります。これは、**Orders** テーブルの子であるためです。 この **Order Details** テーブル (**Orders** テーブルと同じレベルにあるものではなく) を選択し、表示されるドロップダウン矢印をクリックします。

6. ドロップダウン リストで **[ListObject]** をクリックし、**OrderDetails** テーブルをセル **A6** にドラッグします。

7. **Order_DetailsListObject** という名前の <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールがセル **A6** に作成され、<xref:System.Windows.Forms.BindingSource> にバインドされます。

### <a name="to-add-two-buttons"></a>2 つのボタンを追加するには

1. **[ツールボックス]** の **[コモン コントロール]** タブから、<xref:System.Windows.Forms.Button> コントロールをワークシートのセル **A3** に追加します。

    このボタンには `Button1` という名前が付けられます。

2. ワークシートのセル **B3** に別の <xref:System.Windows.Forms.Button> コントロールを追加します。

    このボタンには `Button2` という名前が付けられます。

   次に、ドキュメントにキャッシュするデータセットをマークします。

## <a name="cache-the-dataset"></a>データセットをキャッシュする
 データセットをパブリックにして、**CacheInDocument** プロパティを設定することにより、ドキュメントにキャッシュするデータセットをマークします。

### <a name="to-cache-the-dataset"></a>データセットをキャッシュするには

1. コンポーネント トレイ内の **NorthwindDataSet** を選択します。

2. **[プロパティ]** ウィンドウで、**Modifiers** プロパティを **Public** に変更します。

    キャッシュを有効にする前にデータセットをパブリックにする必要があります。

3. **CacheInDocument** プロパティを **True** に変更します。

   次の手順では、ボタンにテキストを追加します。また、C# の場合は、イベント ハンドラーをフックするコードも追加します。

## <a name="initialize-the-controls"></a>コントロールを初期化する
 ボタン テキストを設定し、<xref:Microsoft.Office.Tools.Excel.Workbook.Startup> イベントの際のイベント ハンドラーを追加します。

### <a name="to-initialize-the-data-and-the-controls"></a>データとコントロールを初期化するには

1. **ソリューション エクスプローラー** で **Sheet1.vb** または **Sheet1.cs** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. 次のコードを `Sheet1_Startup` メソッドに追加して、ボタンのテキストを設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet15":::

3. C# の場合のみ、ボタン クリック イベントのイベント ハンドラーを `Sheet1_Startup` メソッドに追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet16":::

## <a name="add-code-to-enable-scrolling-through-the-records"></a>レコードのスクロールを有効にするコードを追加する
 レコード間を移動するためのコードを、各ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに追加します。

### <a name="to-scroll-through-the-records"></a>レコードをスクロールするには

1. `Button1` の <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを追加し、レコード間を後方に移動するための次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb" id="Snippet17":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet17":::

2. `Button2` の <xref:System.Windows.Forms.Control.Click> イベントのイベント ハンドラーを追加し、レコード間を前方に移動するための次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs" id="Snippet18":::

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ブックをテストして、データが想定どおりに表示されること、およびソリューションをオフラインで使用できることを確認しましょう。

### <a name="to-test-the-data-caching"></a>データ キャッシュをテストするには

1. **F5** キーを押します。

2. 名前付き範囲とリスト オブジェクトに、データ ソースからのデータが格納されていることを確認します。

3. ボタンをクリックして、レコードの一部をスクロールします。

4. ブックを保存し、ブックと Visual Studio を閉じます。

5. データベースへの接続を無効にします。 データベースがサーバーに配置されている場合は、自分のコンピューターからネットワーク ケーブルを抜きます。または、データベースが自分の開発用コンピューター上にある場合は、SQL Server サービスを停止します。

6. Excel を開き、 *\bin* ディレクトリ (Visual Basic では *\My Master-Detail\bin*、C# では *\My Master-Detail\bin\debug*) から **My Master-Detail.xlsx** を開きます。

7. レコードの一部をスクロールして、接続が切断されているときにワークシートが正常に動作することを確認します。

8. データベースに再度接続します。 データベースがサーバーに配置されている場合は、自分のコンピューターをネットワークに再度接続します。または、データベースが自分の開発用コンピューター上にある場合は、SQL Server サービスを開始します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、ワークシート上にマスター/詳細データ関係を作成し、データセットをキャッシュする方法の基本について説明しました。 ここでは、次の作業を行います。

- ソリューションを展開する。 詳細については、「[Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office ソリューションにおけるデータ](../vsto/data-in-office-solutions.md)
- [キャッシュ データ](../vsto/caching-data.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
