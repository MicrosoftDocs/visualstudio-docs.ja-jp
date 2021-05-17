---
title: データセット デザイナーを使ってデータセットを作成する
description: このチュートリアルでは、データセット デザイナーを使用してデータセットを作成します。 新しいプロジェクトを作成し、そのプロジェクトに新しい Dataset 項目を追加するプロセスを理解します。
ms.custom: SEO-VS-2020
ms.date: 09/11/2017
ms.topic: conceptual
helpviewer_keywords:
- datasets [Visual Basic], walkthroughs
- XML schemas, creating datasets
- data [Visual Studio], Dataset Designer
- Dataset Designer, walkthroughs
- datasets [Visual Basic], creating
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: b1fe1d75673dc47f423cf398118230cd1530def0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866230"
---
# <a name="walkthrough-create-a-dataset-with-the-dataset-designer"></a>チュートリアル: データセット デザイナーを使用してデータセットを作成する

このチュートリアルでは、**データセット デザイナー** を使用してデータセットを作成します。 この記事では、新しいプロジェクトを作成し、そのプロジェクトに新しい **Dataset** 項目を追加します。 ウィザードを使用しないで、データベース内のテーブルに基づいてテーブルを作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 Visual Studio インストーラーでは、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクト エクスプローラーは、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-new-windows-forms-application-project"></a>新しい Windows フォーム アプリケーション プロジェクトを作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[Windows フォーム アプリ]** プロジェクト タイプを選択します。

4. プロジェクトに **DatasetDesignerWalkthrough** という名前を付け、 **[OK]** を選択します。

     Visual Studio によって **ソリューション エクスプローラー** にプロジェクトが追加され、デザイナーに新しいフォームが表示されます。

## <a name="add-a-new-dataset-to-the-application"></a>アプリケーションへの新しいデータセットの追加

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. 左側のウィンドウで、 **[データ]** を選択し、中央のペインで **[データセット]** を選択します。

3. データセットに **NorthwindDataset** という名前を付け、 **[追加]** をクリックします。

     Visual Studio によってプロジェクトに **NorthwindDataset.xsd** という名前のファイルが追加され、**データセット デザイナー** でこのファイルが開かれます。

## <a name="create-a-data-connection-in-server-explorer"></a>サーバー エクスプローラーでのデータ接続の作成

1. **[表示]** メニューの **[サーバー エクスプローラー]** をクリックします。

2. **サーバー エクスプローラー** で、**[データベースへの接続]** をクリックします。

3. Northwind サンプル データベースへの接続を作成します。

## <a name="create-the-tables-in-the-dataset"></a>データセットへのテーブルの作成

ここでは、データセットにテーブルを追加する方法について説明します。

### <a name="to-create-the-customers-table"></a>Customers テーブルを作成するには

1. **サーバー エクスプローラー** で作成したデータ接続を展開し、**[テーブル]** ノードを展開します。

2. **サーバー エクスプローラー** から **データセット デザイナー** に **Customers** テーブルをドラッグします。

     **Customers** データ テーブルと **CustomersTableAdapter** がデータセットに追加されます。

### <a name="to-create-the-orders-table"></a>Orders テーブルを作成するには

- **サーバー エクスプローラー** から **データセット デザイナー** に **Orders** テーブルをドラッグします。

     **Orders** データ テーブル、**OrdersTableAdapter**、および **Customers** テーブルと **Orders** テーブル間のリレーションシップが、データセットに追加されます。

### <a name="to-create-the-orderdetails-table"></a>OrderDetails テーブルを作成するには

- **サーバー エクスプローラー** から **データセット デザイナー** に **Order Details** テーブルをドラッグします。

     **Order Details** データ テーブル、**OrderDetailsTableAdapter**、および **Orders** テーブルと **OrderDetails** テーブル間のリレーションシップが、データセットに追加されます。

## <a name="next-steps"></a>次の手順

- データセットを保存します。

- **[データ ソース]** ウィンドウの項目を選択し、フォームにドラッグします。 詳細については、[Visual Studio で Windows フォーム コントロールをデータにバインドする](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)方法に関するページを参照してください。

- TableAdapter に他のクエリを追加します。

- データセット内のデータ テーブルの <xref:System.Data.DataTable.ColumnChanging> イベントまたは <xref:System.Data.DataTable.RowChanging> イベントに検証ロジックを追加します。 詳細については、「[データセットのデータの検証](../data-tools/validate-data-in-datasets.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でデータセットを作成および構成する](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [データの検証](../data-tools/validate-data-in-datasets.md)
