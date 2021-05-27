---
title: DataContext メソッドの戻り値の型を変更する
description: オブジェクト リレーショナル デザイナー (O/R デザイナー) でストアド プロシージャまたは関数をドロップするとき、DataContext メソッドの戻り値の型を変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c5b66bff-6dbb-43c0-bffa-317133ca5b9e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 4226be60f91fb1b9d55e279be2a697861c3f9566
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858801"
---
# <a name="how-to-change-the-return-type-of-a-datacontext-method-or-designer"></a>方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)
ストアド プロシージャまたは関数に基づいて作成された <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、**O/R デザイナー** でストアド プロシージャまたは関数をドロップした場所に応じて異なります。 既存のエンティティ クラスに項目を直接ドロップすると、そのエンティティ クラスを戻り値の型とする <xref:System.Data.Linq.DataContext> メソッドが作成されます (ストアド プロシージャまたは関数によって返されるデータのスキーマがエンティティ クラスの形状と一致する場合)。 **O/R デザイナー** の空の領域に項目をドロップすると、自動生成された型を返す <xref:System.Data.Linq.DataContext> メソッドが作成されます。 <xref:System.Data.Linq.DataContext> メソッドをメソッド ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、**[プロパティ]** ウィンドウでそのメソッドを選択し、**[Return Type]** プロパティをクリックします。

> [!NOTE]
> **[プロパティ]** ウィンドウを使用しても、戻り値の型がエンティティ クラスに設定されている <xref:System.Data.Linq.DataContext> メソッドは、自動生成型を返すようには変更できません。 自動生成型を返すように <xref:System.Data.Linq.DataContext> メソッドを戻すには、元のデータベース オブジェクトをもう一度 **O/R デザイナー** にドラッグする必要があります。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-change-the-return-type-of-a-datacontext-method-from-the-auto-generated-type-to-an-entity-class"></a>DataContext メソッドの戻り値の型を、自動生成型からエンティティ クラスに変更するには

1. メソッド ペインで <xref:System.Data.Linq.DataContext> メソッドを選択します。

2. **[プロパティ]** ウィンドウの **[戻り値の型]** を選択し、**[戻り値の型]** リストで使用可能なエンティティ クラスを選択します。 目的のエンティティ クラスが一覧にない場合は、そのエンティティ クラスを追加するか、**O/R デザイナー** で作成して一覧に追加します。

3. *.dbml* ファイルを保存します。

## <a name="to-change-the-return-type-of-a-datacontext-method-from-an-entity-class-back-to-the-auto-generated-type"></a>DataContext メソッドの戻り値の型を、エンティティ クラスから自動生成型に変更するには

1. **メソッド** ペインで <xref:System.Data.Linq.DataContext> メソッドを選択し、削除します。

2. **サーバー エクスプローラー** または **データベース エクスプローラー** からデータベース オブジェクトを **O/R デザイナー** の空の領域にドラッグします。

3. *.dbml* ファイルを保存します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
