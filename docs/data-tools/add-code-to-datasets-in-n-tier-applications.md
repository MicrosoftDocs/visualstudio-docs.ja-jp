---
title: n 層アプリケーションのデータセットにコードを追加する
description: Visual Studio で、n 層アプリのデータセットにコードを追加します。 データセットの部分クラス ファイルを作成し、(DatasetName.Dataset.Designer ではなく) そのファイルにコードを追加します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, extending DataSets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: c1a6e424fe76b94321ca79ab08496cd160969890
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867530"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>n 層アプリケーションのデータセットにコードを追加する

データセットの部分クラス ファイルを作成し、(*DatasetName*.Dataset.Designer ファイルにコードを追加するのではなく) そのファイルにコードを追加することで、データセットの機能を拡張できます。 部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、[Partial](/dotnet/visual-basic/language-reference/modifiers/partial) に関する記事または[部分クラスと部分メソッド](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)に関する記事を参照してください。

データセットを定義するコードは、(型指定されたデータセット内の) データセット定義が変更されるたびに生成されます。 このコードは、データセットの構成を変更するウィザードの実行中に変更を行ったときにも生成されます。 データセットの再生成時にコードが削除されないようにするには、データセットの部分クラス ファイルにコードを追加します。

既定では、データセット コードと TableAdapter コードを分離すると、プロジェクトごとに別個のクラス ファイルが生成されます。 元のプロジェクトには、TableAdapter コードを含む *DatasetName.Designer.vb* (または *DatasetName.Designer.cs*) という名前のファイルが存在します。 **[DataSet プロジェクト]** プロパティで指定したプロジェクトには、*DatasetName.DataSet.Designer.vb* (または *DatasetName.DataSet.Designer.cs*) という名前のファイルが存在します。このファイルには、データセット コードが含まれます。

> [!NOTE]
> ( **[DataSet プロジェクト]** プロパティを設定して) データセットと TableAdapter を分離するときに、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存のデータセット部分クラスは、手動でデータセット プロジェクトに移動する必要があります。

> [!NOTE]
> 検証コードを追加する必要がある場合、型指定されたデータセットでは、<xref:System.Data.DataTable.ColumnChanging> および <xref:System.Data.DataTable.RowChanging> イベント ハンドラーを生成するための機能が提供されます。 詳細については、「[n 層データセットに検証を追加する](../data-tools/add-validation-to-an-n-tier-dataset.md)」を参照してください。

## <a name="to-add-code-to-datasets-in-n-tier-applications"></a>n 層アプリケーションのデータセットにコードを追加するには

1. *.xsd* ファイルが含まれているプロジェクトを見つけます。

2. **.xsd** ファイルを選択して、データセットを開きます。

3. コードを追加するデータ テーブル (タイトル バーのテーブル名) を右クリックし、 **[コードの表示]** を選択します。

     部分クラスが作成され、コード エディターに表示されます。

4. 部分クラスの宣言内にコードを追加します。

     次の例は、NorthwindDataSet の CustomersDataTable にコードを追加する場所を示しています。

    ```vb
    Partial Public Class CustomersDataTable
        ' Add code here to add functionality
        ' to the CustomersDataTable.
    End Class
    ```

    ```csharp
    partial class CustomersDataTable
    {
        // Add code here to add functionality
        // to the CustomersDataTable.
    }
    ```

## <a name="see-also"></a>関連項目

- [n 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [n 層アプリケーションの TableAdapters にコードを追加する](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [Tableadapter の作成および構成](create-and-configure-tableadapters.md)
- [階層更新の概要](hierarchical-update.md)
- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
