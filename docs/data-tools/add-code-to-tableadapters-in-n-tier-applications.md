---
title: n 層アプリケーションの TableAdapters にコードを追加する
description: n 層アプリケーションのテーブル アダプターにコードを追加します。 TableAdapter の部分クラス ファイルを作成し、(DatasetName.DataSet.Designer にではなく) それにコードを追加します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: da4db396d718fcd8b88b476278a2470663b58a8b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859477"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>n 層アプリケーションの TableAdapters にコードを追加する
TableAdapter の部分クラス ファイルを作成し、(*DatasetName.DataSet.Designer* ファイルにコードを追加するのではなく) そこにコードを追加することにより、TableAdapter の機能を拡張できます。 部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、[Partial](/dotnet/visual-basic/language-reference/modifiers/partial) または [partial (型)](/dotnet/csharp/language-reference/keywords/partial-type) に関するページを参照してください。

TableAdapter を定義するコードは、データセット内の TableAdapter に変更が加えられるたびに生成されます。 このコードは、TableAdapter の構成を変更するウィザードの実行中に変更が行われた場合にも生成されます。 TableAdapter の再生成時にコードが削除されないようにするには、TableAdapter の部分クラス ファイルにコードを追加します。

既定では、データセット コードと TableAdapter コードを分離すると、プロジェクトごとに別個のクラス ファイルが生成されます。 元のプロジェクトには、TableAdapter コードを含む *DatasetName.Designer.vb* (または *DatasetName.Designer.cs*) という名前のファイルが存在します。 **[DataSet プロジェクト]** プロパティで指定したプロジェクトには、データセット コードを含む *DatasetName.DataSet.Designer.vb* (または *DatasetName.DataSet.Designer.cs*) という名前のファイルが存在します。

> [!NOTE]
> **[DataSet プロジェクト]** プロパティを設定してデータセットと TableAdapter を分離する場合でも、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存のデータセット部分クラスは、データセット プロジェクトに手動で移動する必要があります。

> [!NOTE]
> データセットは、検証が必要な場合に <xref:System.Data.DataTable.ColumnChanging> および <xref:System.Data.DataTable.RowChanging> イベント ハンドラーを生成するための機能を提供します。 詳細については、「[n 層データセットに検証を追加する](../data-tools/add-validation-to-an-n-tier-dataset.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>n 層アプリケーションの TableAdapter にユーザー コードを追加するには

1. *.xsd* ファイルが含まれているプロジェクトを探します。

2. *.xsd* ファイルをダブルクリックして、**データセット デザイナー** を開きます。

3. コードを追加する TableAdapter を右クリックし、 **[コードの表示]** を選択します。

     部分クラスが作成され、コード エディターが開きます。

4. 部分クラスの宣言内にコードを追加します。

5. 次の例では、`NorthwindDataSet` でコードを `CustomersTableAdapter` に追加する方法を示します。

    ```vb
    Partial Public Class CustomersTableAdapter
        ' Add code here to add functionality
        ' to the CustomersTableAdapter.
    End Class
    ```

    ```csharp
    public partial class CustomersTableAdapter
    {
        // Add code here to add functionality
        // to the CustomersTableAdapter.
    }
    ```

## <a name="see-also"></a>関連項目

- [n 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [n 層アプリケーションのデータセットにコードを追加する](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [Tableadapter の作成および構成](create-and-configure-tableadapters.md)
- [階層更新の概要](hierarchical-update.md)
