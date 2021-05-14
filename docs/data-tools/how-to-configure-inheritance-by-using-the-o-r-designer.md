---
title: O/R デザイナーを使用して継承を構成する
description: 単一テーブル継承をサポートするオブジェクト リレーショナル デザイナー (O/R デザイナー) を使用して継承を構成する方法について説明します。 継承されたデータ クラスを作成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: fee2c42e6ec84280f4090a8ae1dfea83a81ee369
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866828"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>方法: O/R デザイナーを使用して継承を構成する
**オブジェクト リレーショナル デザイナー** (**O/R デザイナー**) では、リレーショナル システムに実装されていることが多い単一テーブル継承の概念がサポートされています。 単一テーブル継承には、親情報と子情報の両方のフィールドを含む単一のデータベース テーブルがあります。 リレーショナル データでは、判別用の列に、レコードが属するクラスを決定する値が含まれています。

たとえば、会社に雇用されているすべての人を含む `Persons` テーブルについて考えてみます。 従業員の人もいれば、管理者の人もいます。 `Persons` テーブルには、管理者を表す値 1 と従業員を表す値 2 を含む `EmployeeType` という名前の列が含まれています。これが識別子列です。 このシナリオでは、従業員のサブクラスを作成して、そのクラスには `EmployeeType` の値が 2 のレコードだけを入れます。 適用されない列を各クラスから削除することもできます。

継承を使用する (およびリレーショナル データに対応する) オブジェクト モデルの作成は、わかりにくい場合があります。 次の手順では、**O/R デザイナー** で継承を設定するために必要な手順を概説します。 既存のテーブルと列を参照せずに汎用的な手順に従うのは難しい場合があるので、データを使用したチュートリアルが用意されています。 詳細な手順を使用して継承を構成するため、 **O/R デザイナー** を参照してください [チュートリアル: LINQ to SQL を作成するクラスの単一テーブル継承 (O/R デザイナー) を使用して](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)します。

## <a name="to-create-inherited-data-classes"></a>継承されたデータ クラスを作成するには

1. 既存の Visual Basic プロジェクトまたは C# プロジェクトに **LINQ to SQL クラス** 項目を追加して、**O/R デザイナー** を開きます。

2. 基本クラスとして使用するテーブルを **O/R デザイナー** にドラッグします。

3. テーブルの 2 つ目のコピーを **O/R デザイナー** にドラッグし、名前を変更します。 これは、派生クラス、つまりサブクラスです。

4. **ツールボックス** の **[オブジェクト リレーショナル デザイナー]** タブで **[継承]** をクリックし、サブクラス (名前を変更したテーブル) をクリックして、基本クラスに接続します。

    > [!NOTE]
    > **ツールボックス** の **[継承]** 項目をクリックしてマウス ボタンを放し、手順 3 で作成したクラスの 2 番目のコピーをクリックしてから、手順 2 で作成した最初のクラスをクリックします。 継承線の矢印は最初のクラスを指しています。

5. 各クラスで、関連付けに使用されていない、表示する必要のないオブジェクト プロパティを削除します。 関連付けに使用されているオブジェクト プロパティを削除しようとすると、"[プロパティ \<property name> は関連付け \<association name> に関与しているため、削除できません](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md)" というエラーが表示されます。

    > [!NOTE]
    > 派生クラスは基本クラスで定義されているプロパティを継承するため、各クラスに同じ列を定義することはできません  (列はプロパティとして実装されます)。基本クラスのプロパティに継承修飾子を設定することで、派生クラスでの列の作成を可能にすることができます。 詳細については、「[継承の基本 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)」をご覧ください。

6. **O/R デザイナー** で継承線を選択します。

7. **[プロパティ]** ウィンドウで、 **[識別子プロパティ]** を、クラスのレコードを区別するための列の名前に設定します。

8. **[派生クラスの識別子の値]** プロパティに、レコードが継承された型であることを示すデータベース内の値を設定します。 (これは識別子列に格納される値であり、継承されたクラスを示すために使用されます。)

9. **[基本クラスの識別子の値]** プロパティに、レコードが基本型であることを示す値を設定します。 (これは識別子列に格納される値であり、基本クラスを示すために使用されます。)

10. オプションとして、**[継承の既定値]** プロパティを設定することもできます。これは、定義済みの継承コードと一致しない行を読み込むときに使用される継承階層の型を示します。 つまり、あるレコードの識別子列に、 **[派生クラスの識別子の値]** プロパティと **[基本クラスの識別子の値]** プロパティのどちらの値とも一致しない値が含まれている場合、そのレコードは **[継承の既定値]** として指定された型に読み込まれます。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [継承の基本 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [継承](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)
