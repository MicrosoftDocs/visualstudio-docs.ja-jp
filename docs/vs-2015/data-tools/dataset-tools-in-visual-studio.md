---
title: データセットのツール
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vs.data.DataSet
dev_langs:
- VB
- CSharp
- C++
- aspx
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
caps.latest.revision: 53
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 23e4deba53288383a569f6da6e14d27f723825ee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657385"
---
# <a name="dataset-tools-in-visual-studio"></a>Visual Studio のデータセット ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
> データセットと関連クラスは、アプリケーションがデータベースから切断されている間に、アプリケーションがメモリ内のデータを処理できるようにする、2000年より前のレガシ .NET テクノロジです。 これらは、ユーザーがデータを変更し、変更をデータベースに保存できるようにするアプリケーションに特に役立ちます。 データセットは非常に優れたテクノロジであることが実証されていますが、新しい .NET アプリケーションでは Entity Framework を使用することをお勧めします。 Entity Framework では、オブジェクトモデルとして表形式データを操作するためのより自然な方法が提供されます。これにより、プログラミングインターフェイスがより簡単になります。

 DataSet オブジェクトは、実質的にはミニデータベースであるメモリ内オブジェクトです。 これには、開いている接続を維持しなくても、1つまたは複数のデータベースのデータを格納および変更できる DataTable、DataColumn、および DataRow オブジェクトが含まれています。 データセットは、データへの変更に関する情報を保持するため、アプリケーションが再接続されると、更新プログラムを追跡してデータベースに送り返すことができます。

 データセットと関連クラスは、.NET Framework クラスライブラリの system.string 名前空間で定義されています。 コードでは、データセットを動的に作成および変更できます。 その方法の詳細については、「ADO.NET」を参照してください。 このセクションのドキュメントでは、Visual Studio デザイナーを使用してデータセットを操作する方法について説明します。 1つ注意すべき点: デザイナーを使用して作成されたデータセットは、TableAdapter オブジェクトを使用してデータベースとやり取りしますが、プログラムによって DataAdapter オブジェクトを使用します。 プログラムによるデータセットの作成の詳細については、「 [dataadapter And datareader](https://msdn.microsoft.com/library/cc952ca2-ec19-46ab-9189-15174b52cb74)」を参照してください。

 アプリケーションでデータベースからのデータの読み取りのみを行う必要があり、更新、追加、または削除を実行しない場合は、通常、DataReader オブジェクトを使用して、ジェネリックリストオブジェクトまたは別のコレクションオブジェクトにデータを取得することで、パフォーマンスを向上させることができます。 データを表示している場合は、ユーザーインターフェイスをコレクションにデータバインドすることができます。

## <a name="dataset-workflow"></a>データセットワークフロー
 Visual Studio には、データセットの操作を簡略化するためのツールが多数用意されています。 基本的なエンドツーエンドのワークフローは次のとおりです。

- **[データソース]** ウィンドウを使用すると、1つまたは複数のデータソースから新しいデータセットを作成できます。 **データセットデザイナー**を使用してデータセットを構成し、そのプロパティを設定します。 たとえば、含めるデータソースのテーブルと、各テーブルの列を指定する必要があります。 データセットに必要なメモリの量を節約するには、慎重に選択してください。 詳細については、[データセットの作成と構成](../data-tools/create-and-configure-datasets-in-visual-studio.md)に関するページを参照してください。

- 外部キーが正しく処理されるように、テーブル間のリレーションシップを指定します。 詳細については、「 [tableadapter を使用したデータセットの読み込み](../data-tools/fill-datasets-by-using-tableadapters.md)」を参照してください。

- **TableAdapter 構成ウィザード**を使用して、データセットを設定するクエリまたはストアドプロシージャ、および実装するデータベース操作 (更新、削除など) を指定します。 詳細については、次のトピックを参照してください。

  - [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)

  - [データセットのデータの編集](../data-tools/edit-data-in-datasets.md)

  - [データセットのデータの検証](../data-tools/validate-data-in-datasets.md)

  - [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)

- データセット内のデータを照会して検索します。 詳細については、「[クエリデータセット](../data-tools/query-datasets.md)」を参照してください。 [!INCLUDE[linq_dataset](../includes/linq-dataset-md.md)] では、<xref:System.Data.DataSet> オブジェクトのデータに対して[LINQ (統合言語クエリ)](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)を有効にします。 詳細については、「[LINQ to DataSet](https://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17)」を参照してください。

- **[データソース]** ウィンドウを使用すると、ユーザーインターフェイスコントロールをデータセットまたはその個々の列にバインドしたり、ユーザーが編集できる列を指定したりできます。 詳細については、「 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。

## <a name="datasets-and-n-tier-architecture"></a>データセットと N 層アーキテクチャ
 N 層アプリケーションのデータセットの詳細については、「 [n 層アプリケーションでのデータセットの操作](../data-tools/work-with-datasets-in-n-tier-applications.md)」を参照してください。

## <a name="datasets-and-xml"></a>データセットと XML
 XML との間でデータセットを変換する方法については、「データ[セットへの xml データの読み込み](../data-tools/read-xml-data-into-a-dataset.md)」と「 [xml としてのデータセットの保存](../data-tools/save-a-dataset-as-xml.md)」を参照してください。

## <a name="see-also"></a>参照
 [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
