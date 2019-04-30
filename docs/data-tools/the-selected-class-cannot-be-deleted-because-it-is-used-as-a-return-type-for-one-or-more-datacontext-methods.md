---
title: 選択したクラスは、1 つ以上の DataContext メソッドで戻り値の型として使用されているため、削除できません
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: d68254a0-f3a1-47e2-aed3-a83471e1d711
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5d63abefc67d54734380e6a1dc7f3364d5400c03
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62565421"
---
# <a name="the-selected-class-cannot-be-deleted-because-it-is-used-as-a-return-type-for-one-or-more-datacontext-methods"></a>選択したクラスは、1 つ以上の DataContext メソッドで戻り値の型として使用されているため、削除できません

1 つ以上の <xref:System.Data.Linq.DataContext> メソッドの戻り値の型が、選択されたエンティティ クラスになっています。 戻り値の型として使用されるエンティティ クラスを削除、<xref:System.Data.Linq.DataContext>メソッドにより失敗するプロジェクトをコンパイルします。 選択したエンティティ クラスを削除するには、そのエンティティ クラスを使用する <xref:System.Data.Linq.DataContext> メソッドを特定し、戻り値の型を別のエンティティ クラスに設定します。

<xref:System.Data.Linq.DataContext> メソッドの戻り値の型を元の自動生成型に戻すには、まず**メソッド** ペインから <xref:System.Data.Linq.DataContext> メソッドを削除し、次に**サーバー エクスプローラー**/**データベース エクスプローラー**から、オブジェクトをもう一度 **O/R デザイナー**にドラッグします。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. エンティティ クラスを戻り値の型として使用する <xref:System.Data.Linq.DataContext> メソッドを特定します。そのためには、**メソッド** ペインで <xref:System.Data.Linq.DataContext> メソッドを選択し、**[プロパティ]** ウィンドウで **[戻り値の型]** プロパティを調べます。

2. **[戻り値の型]** を別のエンティティ クラスに設定するか、メソッド ペインから <xref:System.Data.Linq.DataContext> メソッドを削除します。

## <a name="see-also"></a>関連項目

- [O/R デザイナーのメッセージ](../data-tools/o-r-designer-messages.md)
- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)