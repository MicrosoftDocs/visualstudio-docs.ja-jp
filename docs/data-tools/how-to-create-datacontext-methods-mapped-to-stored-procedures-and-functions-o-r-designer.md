---
title: DataContext メソッドを sprocs および関数にマップする (O/R デザイナー)
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4fa392467024a38dc447e6a5077f855d3464103b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648364"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)

ストアドプロシージャおよび関数を <xref:System.Data.Linq.DataContext> メソッドとして**O/R デザイナー**に追加できます。 メソッドを呼び出して必要なパラメーターを渡すと、データベースでストアド プロシージャまたは関数が実行され、<xref:System.Data.Linq.DataContext> メソッドの戻り値の型のデータが返されます。 @No__t_0 メソッドの詳細については、「 [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」を参照してください。

> [!NOTE]
> また、ストアドプロシージャを使用すると、エンティティクラスからデータベースに変更が保存されるときに挿入、更新、および削除を実行する既定の [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 実行時の動作をオーバーライドすることもできます。 詳細については、「[方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

## <a name="create-datacontext-methods"></a>DataContext メソッドの作成

@No__t_0 メソッドを作成するには、ストアドプロシージャまたは関数を<strong>サーバーエクスプローラーまたは * * データベースエクスプローラー</strong>から**O/R デザイナー**にドラッグします。

> [!NOTE]
> 生成された <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、 **O/R デザイナー**でストアドプロシージャまたは関数をドロップする場所によって異なります。 既存のエンティティ クラスに項目を直接ドロップすると、そのエンティティ クラスを戻り値の型とする <xref:System.Data.Linq.DataContext> メソッドが作成されます。 **O/R デザイナー**の空の領域に項目をドロップすると、自動的に生成された型を返す <xref:System.Data.Linq.DataContext> メソッドが作成されます。 <xref:System.Data.Linq.DataContext> メソッドを **[メソッド]** ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、 **[プロパティ]** ウィンドウでメソッドを選択し、 **[戻り値の型]** プロパティを調べます。 詳細については、「[方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>自動生成された型を返す DataContext メソッドを作成するには

1. **サーバーエクスプローラー**または**データベースエクスプローラー**で、作業しているデータベースの **[ストアドプロシージャ]** ノードを展開します。

2. 目的のストアドプロシージャを見つけて、 **O/R デザイナー**の空の領域にドラッグします。

     自動生成された戻り値の型を使用して <xref:System.Data.Linq.DataContext> メソッドが作成され、 **[メソッド]** ペインに表示されます。

### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>エンティティ クラスを戻り値の型とする DataContext メソッドを作成するには

1. **サーバーエクスプローラー**または**データベースエクスプローラー**で、作業しているデータベースの **[ストアドプロシージャ]** ノードを展開します。

2. 目的のストアドプロシージャを見つけて、 **O/R デザイナー**の既存のエンティティクラスにドラッグします。

     選択したエンティティ クラスを戻り値の型として <xref:System.Data.Linq.DataContext> メソッドが作成され、 **[メソッド]** ペインに表示されます。

> [!NOTE]
> 既存の <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を変更する方法の詳細については、「[方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [チュートリアル: LINQ to SQL クラスの作成](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Visual Basic における LINQ の概要](/dotnet/visual-basic/programming-guide/language-features/linq/introduction-to-linq)
- [C# での LINQ](/dotnet/csharp/linq/linq-in-csharp)
