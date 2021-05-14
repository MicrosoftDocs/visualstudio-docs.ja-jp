---
title: LINQ to SQL クラスをテーブルおよびビューにマップする (O/R デザイナー)
description: オブジェクト リレーショナル デザイナー (O/R デザイナー) で LINQ to SQL エンティティ クラス (テーブルおよびビューにマップされるクラス) を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0fb78bbc-7a78-4ab4-b32f-85ece912e660
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: b440e8c47afdec6e0b04b5f48a35e15fe48e1875
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866802"
---
# <a name="how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-or-designer"></a>方法: テーブルとビューにマップされた LINQ to SQL クラスを作成する (O/R デザイナー)

データベース テーブルおよびビューにマップされた [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] クラスは、*エンティティ クラス* と呼ばれます。 エンティティ クラスはレコードにマップされますが、エンティティ クラスの個々のプロパティはレコードを構成する個々の列にマップされます。 データベース テーブルまたはビューに基づくエンティティ クラスを作成するには、**サーバー エクスプローラー** または **データベース エクスプローラー** から [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)にテーブルまたはビューをドラッグします。 **O/R デザイナー** によってクラスが生成され、[!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 機能 (<xref:System.Data.Linq.DataContext> のデータ通信および編集機能) を有効にするために、特定の [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 属性が適用されます。 [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] クラスの詳細については、「[LINQ to SQL オブジェクト モデル](/dotnet/framework/data/adonet/sql/linq/the-linq-to-sql-object-model)」をご覧ください。

> [!NOTE]
> **O/R デザイナー** は、1:1 のマッピング関係のみがサポートされる単純なオブジェクト リレーショナル マッパーです。 つまり、エンティティ クラスには、データベース テーブルまたはビューとの 1:1 のマッピング関係しか持たせることができません。 1 つのエンティティ クラスを複数のテーブルにマップするなど、複雑なマッピングはサポートされていません。 ただし、複数の関連テーブルを結合するビューにエンティティ クラスをマップすることはできます。

## <a name="create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>データベース テーブルまたはビューにマップされる LINQ to SQL クラスの作成

**サーバー エクスプローラー** または **データベース エクスプローラー** から **O/R デザイナー** にテーブルまたはビューをドラッグすると、更新の実行に使用される <xref:System.Data.Linq.DataContext> のメソッドに加えて、エンティティ クラスが作成されます。

既定では、[!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] ランタイムによって、更新可能なエンティティ クラスの変更をデータベースに保存するロジックが作成されます。 このロジックは、テーブルのスキーマ (列定義と主キー情報) に基づいています。 この動作が不要な場合は、[!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] ランタイムの既定の動作を使用するのではなく、ストアド プロシージャを使用して挿入、更新、削除を実行するようにエンティティ クラスを構成できます。 詳細については、「[方法:更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>データベース テーブルまたはビューにマップされる LINQ to SQL クラスを作成するには

1. **サーバー エクスプローラー** または **データベース エクスプローラー** で、**[テーブル]** または **[ビュー]** を展開し、アプリケーションで使用するデータベース テーブルまたはビューを探します。

2. テーブルまたはビューを **O/R デザイナー** にドラッグします。

     エンティティ クラスが作成され、デザイン サーフェイスに表示されます。 このエンティティ クラスには、選択されたテーブルまたはビューの列にマップされるプロパティが含まれています。

## <a name="create-an-object-data-source-and-display-the-data-on-a-form"></a>オブジェクト データ ソースの作成とフォームへのデータの表示

**O/R デザイナー** を使用してエンティティ クラスを作成したら、オブジェクト データ ソースを作成し、[[データ ソース]](add-new-data-sources.md#data-sources-window) ウィンドウにエンティティ クラスを読み込むことができます。

### <a name="to-create-an-object-data-source-based-on-linq-to-sql-entity-classes"></a>LINQ to SQL エンティティ クラスに基づいてオブジェクト データ ソースを作成するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックしてプロジェクトをビルドします。

2. **[データ ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データ ソースの表示]** をクリックします。

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

4. **[データソースの種類を選択]** ページで、**[オブジェクト]** をクリックし、**[次へ]** をクリックします。

5. ノードを展開し、クラスを探して選択します。

    > [!NOTE]
    > **Customer** クラスが使用可能でない場合は、ウィザードをキャンセルし、プロジェクトをビルドしてからウィザードを再実行します。

6. **[完了]** をクリックしてデータ ソースを作成し、**Customer** エンティティ クラスを **[データ ソース]** ウィンドウに追加します。

7. **[データ ソース]** ウィンドウからフォームに項目をドラッグします。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [LINQ to SQL オブジェクト モデル](/dotnet/framework/data/adonet/sql/linq/the-linq-to-sql-object-model)
- [チュートリアル: エンティティ クラスの挿入、更新、および削除の動作のカスタマイズ](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [方法: LINQ to SQL クラス間の関連付け (リレーションシップ) を作成する (O/R デザイナー)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)
