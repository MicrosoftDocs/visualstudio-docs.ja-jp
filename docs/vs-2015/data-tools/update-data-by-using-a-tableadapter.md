---
title: TableAdapter を使用してデータ更新 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 30d1fd3ee211d6b30f435104a2e2f9b42ed100c0
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692345"
---
# <a name="update-data-by-using-a-tableadapter"></a>TableAdapter を使用してデータを更新する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Databaseby 呼び出し元に戻す、更新されたデータを送信するには、データセット内のデータを変更して検証した後、 `Update` TableAdapter のメソッド。 `Update`メソッドを 1 つのデータ テーブルを更新してに基づいて適切なコマンド (INSERT、UPDATE、または DELETE) の実行、<xref:System.Data.DataRow.RowState%2A>表内の各データ行のできます。 データセットの関連するテーブルが、Visual Studio は、更新プログラムを実行するために使用 TableAdapterManager クラスを生成します。 TableAdapterManager クラスにより、データベースで定義されている外部キー制約に基づく正しい順序で更新が行われるようになります。 データ バインド コントロールを使用すると、データ バインディング アーキテクチャには、tableAdapterManager と呼ばれる TableAdapterManager クラスのメンバー変数が作成されます。 詳細については、次を参照してください。[階層の更新の概要](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)します。  
  
> [!NOTE]
> データセットの内容でデータ ソースを更新しようとするときにエラーが発生することができます。エラーを回避するをお勧めごと、アダプターを呼び出すコードを配置する`Update`メソッド内で、 `try` / `catch`ブロックします。  
  
 データ ソースを更新するための実際の手順は、ビジネス ニーズによって異なることができますが、次の手順が含まれています。  
  
1. アダプターの呼び出す`Update`メソッドで、 `try` / `catch`ブロック。  
  
2. 例外が検出された場合は、エラーを引き起こしたデータ行を探します。 詳細については、「[方法 :エラーが発生した行を探す](https://msdn.microsoft.com/library/1fa907c5-fe66-4f29-a253-2b97b900050c)します。  
  
3. データの問題を調整 (プログラムを使用できる場合、または無効な行を変更するためのユーザーに提示することで) 行、および更新プログラムをもう一度やり直して (<xref:System.Data.DataRow.HasErrors%2A>、 <xref:System.Data.DataTable.GetErrors%2A>)。  
  
## <a name="savedata-to-a-database"></a>データベースに Savedata  
 呼び出す、 `Update` TableAdapter のメソッド。 データベースに書き込まれる値を含むデータ テーブルの名前を渡します。  
  
#### <a name="to-update-a-database-by-using-a-tableadapter"></a>TableAdapter を使用してデータベースを更新するには  
  
- TableAdapter を囲む`Update`メソッドで、 `try` / `catch`ブロックします。 次の例の内容を更新する方法を示しています、`Customers`テーブルに`NorthwindDataSet`内から、 `try` / `catch`ブロックします。  
  
     [!code-csharp[VbRaddataSaving#9](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#9)]
     [!code-vb[VbRaddataSaving#9](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#9)]  
  
## <a name="see-also"></a>関連項目  
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
