---
title: データセットの読み込み中に制約をオフにする
description: データセットの読み込み中に制約をオフにする方法について説明します。 プログラムで、またはデータセット デザイナーを使用して、更新の制約を一時停止します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DataRow.BeginEdit
- DataRow.EndEdit
- DataRow.CancelEdit
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, constraints
- constraints [Visual Basic], datasets
- datasets [Visual Basic], constraints
- constraints [Visual Basic], suspending during dataset update
ms.assetid: 553f7d0c-2faa-4c17-b226-dd02855bf1dc
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 3280894ba1634f9775def74a88dcb413c94ba77a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215709"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>データセットの読み込み中に制約をオフにする

データセットに制約 (外部キー制約など) が含まれる場合、それらは、データセットに対して実行される操作の順序に関連するエラーを発生させる危険性があります。 たとえば、親レコードを読み込む前に子レコードを読み込むと、制約違反となり、エラーが発生する場合があります。 子レコードを読み込んだ直後に、関連する親があるかどうかが制約でチェックされ、エラーが生成されます。

一時的に制約を中断する機構がない場合は、レコードを子テーブルに読み込もうとするたびにエラーが生成されます。 データセットのすべての制約を中断する別の方法として、<xref:System.Data.DataRow.BeginEdit%2A> プロパティおよび <xref:System.Data.DataRow.EndEdit%2A> プロパティを使用できます。

> [!NOTE]
> 制約をオフにすると、検証イベント (<xref:System.Data.DataTable.ColumnChanging>、<xref:System.Data.DataTable.RowChanging> など) は生成されなくなります。

## <a name="to-suspend-update-constraints-programmatically"></a>更新制約をプログラムによって中断するには

- 次の例は、データセットでの制約チェックを一時的に無効にする方法を示しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet10":::

## <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>データセット デザイナーを使って更新制約を中断するには

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「[チュートリアル: データセット デザイナーを使用してデータセットを作成する](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. **[プロパティ]** ウィンドウで、 <xref:System.Data.DataSet.EnforceConstraints%2A> プロパティを `false`に設定します。

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
- [データセットのリレーションシップ](../data-tools/relationships-in-datasets.md)
