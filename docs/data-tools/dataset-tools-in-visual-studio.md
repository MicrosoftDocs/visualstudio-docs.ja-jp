---
title: データセットのツール
description: Visual Studio で提供されているデータセット ツールについて確認します。 データセット ワークフロー、データセットと N 層アーキテクチャ、データセットと XML について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: conceptual
f1_keywords:
- vs.data.DataSet
helpviewer_keywords:
- untyped datasets
- datasets [Visual Basic], extended properties
- typed datasets
- current record in dataset
- XML [Visual Basic], datasets
- DataSet class, about datasets
- unique constraints (datasets)
- data relationships
- parent records in datasets
- extended properties, in typed datasets
- datasets [Visual Basic]
- schemas [Visual Basic], datasets
- datasets [Visual Basic], msprop
- master-detail tables, datasets
- databases [Visual Basic], updating
- msprop
- foreign keys, datasets
- DataSet class
- datasets [Visual Basic], filling
- case sensitivity, datasets
- constraints [Visual Basic], datasets
- child records
- related tables, datasets
- updating datasets, about dataset updates
- data caching, datasets
- DataRelation object, datasets
- untyped datasets, compared to typed datasets
- cache [Visual Studio], datasets
- datasets [Visual Basic], relationships
- related tables
- XML schemas, about XML schemas and datasets
- relationships, datasets
- typed datasets, compared to untyped datasets
- datasets [Visual Basic], populating
- datasets [Visual Basic], namespace
- data adapters, populating datasets
ms.assetid: ee57f4f6-9fe1-4e0a-be9a-955c486ff427
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 4e711d60010117f3a5081470ab8e6e656a7e6e90
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866997"
---
# <a name="dataset-tools-in-visual-studio"></a>Visual Studio のデータセット ツール

> [!NOTE]
> データセットと関連クラスは、アプリケーションがデータベースから切断されている間にアプリケーションがメモリ内のデータを操作できるようにする、2000 年代初期のレガシ .NET テクノロジです。 これらが特に役立つのは、ユーザーがデータを変更し、変更をデータベースに戻して保持できるようにするアプリケーションです。 データセットは非常に優れたテクノロジであることが証明されていますが、新しい .NET アプリケーションでは Entity Framework を使用することをお勧めします。 Entity Framework には、オブジェクト モデルとして表形式データを操作する、より自然な方法が用意されており、よりシンプルなプログラミング インターフェイスが備わっています。

`DataSet` オブジェクトは、本質的に小型データベースである、メモリ内オブジェクトです。 これには、開いた接続を維持しなくても 1 つ以上のデータベースのデータを格納し、変更することができるオブジェクトの `DataTable`、`DataColumn`、`DataRow` が含まれてます。 データセットではデータに対する変更についての情報が保持されるため、更新内容を追跡し、アプリケーションが再接続した状態になったときにデータベースに送り返すことができます。

データセットと関連クラスは、.NET API の <xref:System.Data?displayProperty=fullName> 名前空間で定義されています。 データセットは、ADO.NET を使用して、コード内で動的に作成したり変更したりすることができます。 このセクションのドキュメントでは、Visual Studio デザイナーを使用してデータセットを操作する方法を示しています。 デザイナーで作成されるデータセットでは、**TableAdapter** オブジェクトを使用してデータベースとやり取りします。 プログラムによって作成されるデータセットでは、**DataAdapter** オブジェクトを使用します。 プログラムによるデータセットの作成については、「[DataAdapters と DataReaders](/dotnet/framework/data/adonet/dataadapters-and-datareaders)」を参照してください。

アプリケーションで行う必要があるのはデータベースからのデータの読み取りのみで、更新、追加、削除を実行しない場合は、`DataReader` オブジェクトを使用して汎用の `List` オブジェクトまたは別のコレクション オブジェクト内にデータを取得すれば、通常はパフォーマンスを向上させることができます。 データを表示しようとしている場合は、ユーザー インターフェイスをそのコレクションにデータバインドすることができます。

## <a name="dataset-workflow"></a>データセット ワークフロー

Visual Studio には、データセットの操作を簡略化するためのツールが用意されています。 基本的なエンドツーエンドのワークフローは以下のとおりです。

- [[データ ソース]](add-new-data-sources.md#data-sources-window) ウィンドウを使用して、1 つ以上のデータ ソースから新しいデータセットを作成します。 **データセット デザイナー** を使用して、データセットを構成し、そのプロパティを設定します。 たとえば、データ ソースのどのテーブルを含めるかと、各テーブルのどの列を含めるかを指定する必要があります。 慎重に選択して、データセットに必要なメモリの量を節約します。 詳細については、[データセットの作成と構成](../data-tools/create-and-configure-datasets-in-visual-studio.md)に関するページを参照してください。

- 外部キーが正しく処理されるように、テーブル間のリレーションシップを指定します。 詳細については、「[TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)」を参照してください。

- **TableAdapter 構成ウィザード** を使用して、データセットにデータを格納するクエリまたはストアド プロシージャと、どのデータベース操作 (更新、削除など) を実装するかを指定します。 詳細については、以下のトピックを参照してください。

  - [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)

  - [データセットのデータの編集](../data-tools/edit-data-in-datasets.md)

  - [データセットのデータの検証](../data-tools/validate-data-in-datasets.md)

  - [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)

- データセット内のデータのクエリを行って検索します。 詳細については、「[データセットのクエリ](../data-tools/query-datasets.md)」を参照してください。 [!INCLUDE[linq_dataset](../data-tools/includes/linq_dataset_md.md)] を使用すると、[ オブジェクト内のデータに対して <xref:System.Data.DataSet>LINQ (統合言語クエリ)](/dotnet/csharp/linq/) が有効になります。 詳細については、「[LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)」を参照してください。

- **[データ ソース]** ウィンドウを使用して、ユーザー インターフェイス コントロールをデータセットまたはその個々の列にバインドし、どの列はユーザーが編集可能であるかを指定します。 詳細については、「[Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。

## <a name="datasets-and-n-tier-architecture"></a>データセットと N 層アーキテクチャ

N 層データ アプリケーションでのデータセットの詳細については、「[n 層アプリケーションでのデータセットの操作](../data-tools/work-with-datasets-in-n-tier-applications.md)」を参照してください。

## <a name="datasets-and-xml"></a>データセットと XML

XML に対するデータセットの変換については、「[XML データのデータセットへの読み込み](../data-tools/read-xml-data-into-a-dataset.md)」と「[データセットを XML として保存する](../data-tools/save-a-dataset-as-xml.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
