---
title: データセットの作成と構成
description: Visual Studio でデータセットを作成して構成します。 データセットとは、DB からのデータをメモリに格納し、そのデータに対する CRUD 操作をサポートする一連のオブジェクトです。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: how-to
helpviewer_keywords:
- typed datasets, creating
- datasets, creating
- datasets, configuring
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: f625b17841fe63b0c42dcfb82c2e859d6406e776
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859126"
---
# <a name="how-to-create-and-configure-datasets-in-visual-studio"></a>方法: Visual Studio でデータセットを作成して構成する

データセットとは、データベースからのデータをメモリに格納し、データベースに常に接続していなくても、そのデータに対する作成、読み取り、更新、削除 (CRUD) 操作を可能にするための変更追跡をサポートする一連のオブジェクトです。 データセットは、単純な "*フォーム オーバー データ*" ビジネス アプリケーション向けに設計されています。 新しいアプリケーションの場合は、Entity Framework を使用して、データをメモリに格納し、モデル化することを検討してください。 データセットを操作するには、データベースの概念に関する基本的な知識が必要です。

Visual Studio の **データ ソース構成ウィザード** を使用して、型指定された <xref:System.Data.DataSet> クラスをデザイン時に作成できます。 プログラムによってデータセットを作成する方法については、[データセットの作成 (ADO.NET)](/dotnet/framework/data/adonet/dataset-datatable-dataview/creating-a-dataset) に関する記事を参照してください。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>データ ソース構成ウィザードを使用して新しいデータセットを作成する

1. Visual Studio で自分のプロジェクトを開き、 **[プロジェクト]**  >  **[新しいデータ ソースの追加]** の順に選択して、**データ ソース構成ウィザード** を開始します。

2. 接続先となるデータ ソースの種類を選択します。

     ![データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)

3. データセットのデータ ソースとなる 1 つまたは複数のデータベースを選択します。

     ![データ ソースの接続の選択](../data-tools/media/data-source-choose-a-connection.png)

4. データセットで表示する、データベースのテーブル (または個々の列)、ストアド プロシージャ、関数、ビューを選択します。

     ![データベース オブジェクトの選択](../data-tools/media/raddata-chose-objects.png)

5. **[完了]** をクリックします。

   データセットは、**ソリューション エクスプローラー** にノードとして表示されます。

   ![ソリューション エクスプローラー内のデータセット](../data-tools/media/dataset-in-solution-explorer.png)

6. **ソリューション エクスプローラー** でデータセット ノードをクリックして、**データセット デザイナー** でデータセットを開きます。 データセット内の各テーブルには、`TableAdapter` オブジェクトが関連付けられています。これは下部に表示されます。 テーブル アダプターは、データセットを設定し、必要に応じて、データベースにコマンドを送信するために使用されます。

   ![データセット デザイナー](../data-tools/media/dataset-designer.png)

7. テーブルを関連付けるリレーションシップ線は、データベースで定義されているテーブル リレーションシップを表します。 既定では、データベースの外部キー制約はリレーションシップとしてのみ表され、更新と削除のルールはなしに設定されています。 通常はこれが求められています。 ただし、線をクリックして **[リレーションシップ]** ダイアログを表示し、階層更新の動作を変更することもできます。 詳細については、[データセットのリレーションシップ](../data-tools/relationships-in-datasets.md)に関する記事および「[階層更新](../data-tools/hierarchical-update.md)」を参照してください。

     ![データセットの [リレーションシップ] ダイアログ](../data-tools/media/raddata-relation-dialog.png)

8. テーブル、テーブル アダプター、またはテーブルの列名をクリックして、 **[プロパティ]** ウィンドウにプロパティを表示します。 ここで一部の値を変更できます。 変更するのはソース データベースではなく、データセットであることに注意してください。

     ![データセットの列のプロパティ](../data-tools/media/dataset-column-properties.png)

9. **[ツールボックス]** タブから項目をドラッグして、データセットに新しいテーブルやテーブル アダプターを追加したり、既存のテーブル アダプターの新しいクエリを追加したりできます。また、テーブル間の新しいリレーションシップを指定することもできます。このタブは、**データセット デザイナー** にフォーカスがあるときに表示されます。

     ![データセットの [ツールボックス]](../data-tools/media/raddata-dataset-toolbox.png)

次に、データセットにデータを設定する方法を指定できます。 そのためには、**TableAdapter 構成ウィザード** を使用します。 詳細については、「[TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)」を参照してください。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>データベース テーブルまたは他のオブジェクトを既存のデータセットに追加する

この手順では、最初にデータセットを作成するときに使用したのと同じデータベースからテーブルを追加する方法を示します。

1. **ソリューション エクスプローラー** でデータセット ノードをクリックして、**データセット デザイナー** にフォーカスを移します。

2. Visual Studio の左の余白にある **[データ ソース]** タブをクリックするか、検索ボックスに「**データ ソース**」と入力します。

3. データセット ノードを右クリックし、 **[ウィザードでデータ ソースを構成]** を選択します。

     ![データ ソースのコンテキスト メニュー](../data-tools/media/data-source-context-menu.png)

4. ウィザードを使用して、データセットに追加するテーブル、ストアド プロシージャ、または他のデータベース オブジェクトを指定します。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>スタンドアロンのデータ テーブルをデータセットに追加する

1. **データセット デザイナー** でご自分のデータセットを開きます。

2. **[ツールボックス]** の **[データセット]** タブから **データセット デザイナー** に、<xref:System.Data.DataTable> クラスをドラッグします。

3. 列を追加してデータ テーブルを定義します。 テーブルを右クリックし、 **[追加]**  >  **[列]** の順に選択します。 **[プロパティ]** ウィンドウを使用して、列のデータ型と、必要に応じてキーを設定します。

スタンドアロンのテーブルでは、データを入力できるように、テーブルに `Fill` ロジックを実装する必要があります。 スタンドアロンのデータ テーブルへの入力については、「[DataAdapter からの DataSet の読み込み](/dotnet/framework/data/adonet/populating-a-dataset-from-a-dataadapter)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [データセットのリレーションシップ](../data-tools/relationships-in-datasets.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
