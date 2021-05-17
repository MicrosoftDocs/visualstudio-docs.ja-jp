---
title: TableAdapter の機能を拡張する
description: TableAdapter の部分クラス ファイルにコードを追加して、TableAdapter の機能を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- data [Visual Studio], extending TableAdapters
- TableAdapters, adding functionality
ms.assetid: 418249c8-c7f3-47ef-a94c-744cb6fe6aaf
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: f8cea8ec761bf50ddc0f928112975c366f62418b
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215839"
---
# <a name="extend-the-functionality-of-a-tableadapter"></a>TableAdapter の機能を拡張する

Tableadapter の部分クラス ファイルにコードを追加することにより、TableAdapter の機能を拡張できます。

**データセット デザイナー** で TableAdapter に変更が加えられた場合、またはウィザードによって TableAdapter の構成が変更された場合に、TableAdapter を定義するコードが再生成されます。 TableAdapter の再生成時にコードが削除されないようにするには、TableAdapter の部分クラス ファイルにコードを追加します。

部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、[Partial](/dotnet/visual-basic/language-reference/modifiers/partial) または [partial (型)](/dotnet/csharp/language-reference/keywords/partial-type) に関するページを参照してください。

## <a name="locate-tableadapters-in-code"></a>コード内の TableAdapter の検索

TableAdapter は **データセット デザイナー** でデザインされますが、生成される TableAdapter のクラスは、<xref:System.Data.DataSet> の入れ子にされたクラスではありません。 TableAdapter は、TableAdapter の関連付けられたデータセットの名前に基づいた名前空間に配置されます。 たとえば、アプリケーションに `HRDataSet` という名前のデータセットが含まれている場合、TableAdapter は `HRDataSetTableAdapters` 名前空間に配置されます。 (名前付け規則がこのパターンに従います: *DatasetName* + `TableAdapters`)。

次の例では、`CustomersTableAdapter` という名前の TableAdapter が、`NorthwindDataSet` を使用したプロジェクトに存在するものとします。

### <a name="to-create-a-partial-class-for-a-tableadapter"></a>TableAdapter の部分クラスを作成するには

1. **[プロジェクト]** メニューに移動して、 **[クラスの追加]** をクリックして、新しいクラスをプロジェクトに追加します。

2. クラスに `CustomersTableAdapterExtended` という名前を付けます。

3. **[追加]** を選択します。

4. 次のように、プロジェクトの正しい名前空間と部分クラス名でコードを置き換えます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/CustomersTableAdapterExtended.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/CustomersTableAdapterExtended.vb" id="Snippet2":::

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
