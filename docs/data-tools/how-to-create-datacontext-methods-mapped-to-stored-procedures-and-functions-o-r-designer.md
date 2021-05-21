---
title: DataContext メソッドを sprocs や関数にマップする
description: オブジェクト リレーショナル デザイナー (O/R デザイナー) を使用して、ストアド プロシージャ (sprocs) や関数にマップされた DataContext メソッドを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 2f9b003deb7bc4c564be62d8e7ca486c88cee8a1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858736"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)

ストアド プロシージャと関数は、<xref:System.Data.Linq.DataContext> メソッドとして **O/R デザイナー** に追加できます。 メソッドを呼び出して必要なパラメーターを渡すと、データベースでストアド プロシージャまたは関数が実行され、<xref:System.Data.Linq.DataContext> メソッドの戻り値の型のデータが返されます。 <xref:System.Data.Linq.DataContext> メソッドの詳細については、「[DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」を参照してください。

> [!NOTE]
> ストアド プロシージャを使用して、エンティティ クラスからデータベースに変更が保存されたときに挿入、更新、削除を実行する既定の [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] ランタイムの動作をオーバーライドすることもできます。 詳細については、「[方法:更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

## <a name="create-datacontext-methods"></a>DataContext メソッドを作成する

<xref:System.Data.Linq.DataContext> メソッドを作成するには、ストアド プロシージャまたは関数を、<strong>サーバー エクスプローラーまたは**データベース エクスプローラー</strong>から **O/R デザイナー** にドラッグします。

> [!NOTE]
> 生成される <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、**O/R デザイナー** でストアド プロシージャまたは関数をドロップする場所によって異なります。 既存のエンティティ クラスに項目を直接ドロップすると、そのエンティティ クラスを戻り値の型とする <xref:System.Data.Linq.DataContext> メソッドが作成されます。 **O/R デザイナー** の空の領域に項目をドロップすると、自動的に生成された型を返す <xref:System.Data.Linq.DataContext> メソッドが作成されます。 <xref:System.Data.Linq.DataContext> メソッドを **[メソッド]** ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、**[プロパティ]** ウィンドウでメソッドを選択し、**[戻り値の型]** プロパティを調べます。 詳細については、「[方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>自動生成された型を返す DataContext メソッドを作成するには

1. **サーバー エクスプローラー** または **データベース エクスプローラー** で、作業中のデータベースの **[ストアド プロシージャ]** ノードを展開します。

2. 目的のストアド プロシージャを見つけ、**O/R デザイナー** の空の領域にドラッグします。

     自動生成された戻り値の型を使用して <xref:System.Data.Linq.DataContext> メソッドが作成され、**[メソッド]** ペインに表示されます。

### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>エンティティ クラスを戻り値の型とする DataContext メソッドを作成するには

1. **サーバー エクスプローラー** または **データベース エクスプローラー** で、作業中のデータベースの **[ストアド プロシージャ]** ノードを展開します。

2. 目的のストアド プロシージャを見つけ、**O/R デザイナー** の既存のエンティティ クラスにドラッグします。

     選択したエンティティ クラスを戻り値の型として <xref:System.Data.Linq.DataContext> メソッドが作成され、**[メソッド]** ペインに表示されます。

> [!NOTE]
> 既存の <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を変更する方法については、「[方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [チュートリアル: LINQ to SQL クラスを作成する](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Visual Basic における LINQ の概要](/dotnet/visual-basic/programming-guide/language-features/linq/introduction-to-linq)
- [C# での LINQ](/dotnet/csharp/linq/linq-in-csharp)
