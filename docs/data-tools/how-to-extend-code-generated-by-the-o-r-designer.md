---
title: '方法: O-R デザイナーで生成されたコードを拡張する'
description: オブジェクト リレーショナル デザイナー (O/R デザイナー) で生成されたコードを拡張する方法を確認します。 エンティティ クラスにコードを追加します。 DataContext にコードを追加します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 2404fd48aade91c623efb12e89f4a97da01ec66b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858710"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>方法: O/R デザイナーで生成されたコードを拡張する
**O/R デザイナー** で生成されたコードは、デザイナー サーフェイスでエンティティ クラスや他のオブジェクトに変更を加えると再生成されます。 このコードの再生成により、通常、生成されたコードに追加したコードは、デザイナーがコードを再生成するときに上書きされます。 **O/R デザイナー** には、上書きされないコードを追加できる部分クラス ファイルを生成する機能が用意されています。 **O/R デザイナー** で生成されたコードに独自のコードを追加する例の 1 つとして、LINQ to SQL (エンティティ) クラスへのデータ検証の追加があります。 詳細については、「[方法: エンティティ クラスに検証を追加する](../data-tools/how-to-add-validation-to-entity-classes.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>エンティティ クラスにコードを追加する

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>部分クラスを作成し、エンティティ クラスにコードを追加するには

1. **O/R デザイナー** で LINQ to SQL クラス ファイル ( **.dbml** ファイル) を開くか、新しく作成します (**ソリューション エクスプローラー** または **データベース エクスプローラー** で、 **.dbml** ファイルをダブルクリックします)。

2. **O/R デザイナー** で、検証を追加するクラスを右クリックして、**[コードの表示]** をクリックします。

     コード エディターが開き、選択したエンティティ クラスの部分クラスが表示されます。

3. エンティティ クラスの部分クラス宣言内にコードを追加します。

## <a name="add-code-to-a-datacontext"></a>DataContext にコードを追加する

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>部分クラスを作成し、DataContext にコードを追加するには

1. **O/R デザイナー** で LINQ to SQL クラス ファイル ( **.dbml** ファイル) を開くか、新しく作成します (**ソリューション エクスプローラー** または **データベース エクスプローラー** で、 **.dbml** ファイルをダブルクリックします)。

2. **O/R デザイナー** で、デザイナーの空の領域を右クリックし、 **[コードの表示]** をクリックします。

     コード エディターが開き、DataContext の部分クラスが表示されます。

3. DataContext の部分クラス宣言内にコードを追加します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
