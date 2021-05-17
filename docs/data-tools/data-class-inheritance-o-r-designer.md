---
title: データ クラスの継承 (O/R デザイナー)
description: Visual Studio の LINQ to SQL クラス ツールであるオブジェクト リレーショナル デザイナー (O/R デザイナー) で、データ クラスの継承の作業を行います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: af32653c-f4e6-4217-8c5a-e32b322b4918
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 4fed8d57359a6b4f7b6f64b283ed30c824ae32de
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867062"
---
# <a name="data-class-inheritance-or-designer"></a>データ クラスの継承 (O/R デザイナー)

LINQ to SQL のクラスは、他のオブジェクトと同様に、継承を使用して他のクラスから派生させることができます。 コードでは、あるクラスが別のクラスから継承されていることを宣言することによって、オブジェクト間の継承関係を指定できます。 データベースでは、継承関係が複数の方法で作成されます。 **オブジェクト リレーショナル デザイナー** (**O/R Designer**)では、リレーショナル システムに実装されている場合が多いため、単一テーブル継承の概念がサポートされています。

単一テーブル継承では、基本クラスと派生クラスの両方の列が入った単一データベース テーブルが関係します。 リレーショナル データでは、識別子の列に、特定のレコードが属するクラスを決定する値が含まれます。 たとえば、会社に採用されたすべての人が含まれる `Persons` テーブルがあるとします。 従業員の人もいれば、管理者の人もいます。 `Persons` テーブルには `Type` という列があり、列の値は管理者は 1、従業員は 2 です。 `Type` 列が識別子の列です。 このシナリオでは、従業員のサブクラスを作成し、そのクラスには `Type` の値が 2 であるレコードだけを格納します。

[!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)] を使用してエンティティ クラスでの継承を構成する場合、継承データを含んだ単一テーブルをデザイナーに、継承階層のクラスごとに 1 回、計 2 回ドラッグします。 デザイナーにテーブルを追加した後、**[オブジェクト リレーショナル デザイナー]** ツールボックスでそれらのテーブルを継承項目に接続して、**[プロパティ]** ウィンドウで 4 つの継承プロパティを設定します。

## <a name="inheritance-properties"></a>継承プロパティ

継承プロパティとその説明については、次の表を参照してください。

|プロパティ|説明|
|--------------|-----------------|
|**識別子プロパティ**|現在のレコードが属するクラスを判別するプロパティ (列にマップされる)。|
|**基本クラスの識別子の値**|レコードが基本クラスに属することを決定する (**識別子プロパティ** として指定された列の) 値。|
|**派生クラスの識別子の値**|レコードが派生クラスに属することを決定する (**識別子プロパティ** として指定されたプロパティの) 値。|
|**継承の既定値**|**[識別子プロパティ]** であると指定されたプロパティの値が、 **[基本クラスの識別子の値]** または **[派生クラスの識別子の値]** のどちらにも一致しない場合に格納されるクラス。|

継承を使用し、リレーショナル データに対応するオブジェクト モデルの作成は、混乱しやすい場合があります。 このトピックでは、継承を構成する場合に必要な基本的な概念と個々のプロパティについて説明します。 以下のトピックには、**O/R デザイナー** を使用した継承の構成方法について、より詳しい説明が記載されています。

|トピック|説明|
|-----------|-----------------|
|[方法: O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)|**O/R デザイナー** を使用して、単一テーブル継承を使用するエンティティ クラスを構成する方法について説明しています。|
|[チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)|**O/R デザイナー** を使用して、単一テーブル継承を使用するエンティティ クラスを構成するための詳細な手順が記載されています。|

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [はじめに](/dotnet/framework/data/adonet/sql/linq/getting-started)
