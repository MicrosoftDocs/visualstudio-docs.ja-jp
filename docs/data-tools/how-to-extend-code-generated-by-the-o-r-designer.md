---
title: '方法: O/R デザイナーで生成されたコードを拡張する'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e82166ab336023812c63045c031b81d94dea67e0
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60066248"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>方法: O/R デザイナーで生成されたコードを拡張する
によって生成されたコード、 **O/R デザイナー**エンティティ クラスをデザイナー画面には、その他のオブジェクトが変更されたときに再生成します。 このコードの再生成により、通常、生成されたコードに追加したコードは、デザイナーがコードを再生成するときに上書きされます。 **O/R デザイナー**が上書きされないコードを追加できる部分クラス ファイルを生成する機能を提供します。 によって生成されたコードに独自のコードを追加する 1 つの例、 **O/R デザイナー** to SQL (エンティティ) クラスでデータ検証を LINQ を追加します。 詳細については、「[方法 :エンティティ クラスに検証を追加](../data-tools/how-to-add-validation-to-entity-classes.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>エンティティ クラスにコードを追加します。

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>部分クラスを作成し、エンティティ クラスにコードを追加するには

1. 開くか、新しい LINQ to SQL クラス ファイルの作成 (**.dbml**ファイル) で、 **O/R デザイナー**します。 (ダブルクリックして、 **.dbml**ファイル**ソリューション エクスプ ローラー**または**データベース エクスプ ローラー**)。

2. **O/R デザイナー**で、検証を追加するクラスを右クリックして、**[コードの表示]** をクリックします。

     コード エディターが開き、選択したエンティティ クラスの部分クラスが表示されます。

3. エンティティ クラスの部分クラス宣言内にコードを追加します。

## <a name="add-code-to-a-datacontext"></a>DataContext にコードを追加します。

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>部分クラスを作成し、DataContext にコードを追加するには

1. 開くか、新しい LINQ to SQL クラス ファイルの作成 (**.dbml**ファイル) で、 **O/R デザイナー**します。 (ダブルクリックして、 **.dbml**ファイル**ソリューション エクスプ ローラー**または**データベース エクスプ ローラー**)。

2. **O/R デザイナー**デザイナーの空の領域を右クリックし、クリックして**コードの表示**します。

     コード エディターが開き、DataContext の部分クラスが表示されます。

3. DataContext の部分クラス宣言内にコードを追加します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラス (O/R デザイナー) を作成](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)