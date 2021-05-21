---
title: 単一テーブル継承を使用した LINQ to SQL クラス
description: このチュートリアルでは、Visual Studio オブジェクト リレーショナル デザイナー (O/R デザイナー) で単一テーブル継承を使用して、LINQ to SQL クラスを作成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 63bc6328-e0df-4655-9ce3-5ff74dbf69a4
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 7ed6d6f9d6a0e723979764313d185a41f49a08ce
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858151"
---
# <a name="walkthrough-create-linq-to-sql-classes-by-using-single-table-inheritance-or-designer"></a>チュートリアル: 単一テーブル継承を使用して LINQ to SQL クラスを作成する (O/R デザイナー)
[Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)では、リレーショナル システムに通常実装されている単一テーブル継承がサポートされています。 このチュートリアルでは、「[方法: O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)」に記載されている汎用的な手順を拡張し、実際のデータを使用して [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)]での継承の使用方法を示します。

このチュートリアルでは次のタスクを実行します。

- データベース テーブルを作成し、データを追加します。

- Windows フォーム アプリケーションを作成します。

- [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] ファイルをプロジェクトに追加します。

- 新しいエンティティ クラスを作成します。

- 継承を使用するようにエンティティ クラスを構成します。

- 継承されたクラスをクエリします。

- Windows フォームにデータを表示します。

## <a name="create-a-table-to-inherit-from"></a>継承するテーブルの作成
継承のしくみを確認するために、小さな `Person` テーブルを作成し、それを基底クラスとして使用して、そこから継承する `Employee` オブジェクトを作成します。

### <a name="to-create-a-base-table-to-demonstrate-inheritance"></a>ベース テーブルを作成して継承の動作を確認するには

1. **サーバー エクスプローラー** または **データベース エクスプローラー** で、 **[テーブル]** ノードを右クリックし、 **[新しいテーブルの追加]** をクリックします。

    > [!NOTE]
    > Northwind データベースを使用することも、テーブルを追加できる他の任意のデータベースを使用することもできます。

2. **テーブル デザイナー** で、次の列をテーブルに追加します。

    |列名|データ型|Null を許容|
    |-----------------|---------------|-----------------|
    |**ID**|**int**|**False**|
    |**Type**|**int**|**True**|
    |**FirstName**|**nvarchar(200)**|**False**|
    |**LastName**|**nvarchar(200)**|**False**|
    |**マネージャー**|**int**|**True**|

3. ID 列を主キーとして設定します。

4. テーブルを **Person** という名前で保存します。

## <a name="add-data-to-the-table"></a>テーブルへのデータの追加
継承が正しく構成されていることを確認できるように、単一テーブル継承のテーブルの各クラスにデータを入力する必要があります。

### <a name="to-add-data-to-the-table"></a>テーブルにデータを追加するには

1. データ ビューでテーブルを開きます  (**サーバー エクスプローラー** または **データベース エクスプローラー** で **Person** テーブルを右クリックし、 **[テーブル データの表示]** をクリックします)。

2. テーブルに次のデータをコピーします。 ( **[結果]** ペインで行全体を選択してコピーし、テーブルに貼り付けることができます。)

    |**ID**|**Type**|**FirstName**|**LastName**|**マネージャー**|
    |-|-|-|-|-|
    |**1**|**1**|**Anne**|**Wallace**|**NULL**|
    |**2**|**1**|**Carlos**|**Grilo**|**NULL**|
    |**3**|**1**|**Yael**|**Peled**|**NULL**|
    |**4**|**2**|**Gatis**|**Ozolins**|**1**|
    |**5**|**2**|**Andreas**|**Hauser**|**1**|
    |**6**|**2**|**Tiffany**|**Phuvasate**|**1**|
    |**7**|**2**|**Alexey**|**Orekhov**|**2**|
    |**8**|**2**|**Michał**|**Poliszkiewicz**|**2**|
    |**9**|**2**|**Tai**|**Yee**|**2**|
    |**10**|**2**|**Fabricio**|**Noriega**|**3**|
    |**11**|**2**|**Mindy**|**Martin**|**3**|
    |**12**|**2**|**Ken**|**Kwok**|**3**|

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
これでテーブルが作成されたので、新しいプロジェクトを作成して継承の構成を実際に行います。

### <a name="to-create-the-new-windows-forms-application"></a>新しい Windows フォーム アプリケーションを作成するには

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、プロジェクトの種類として **[Windows フォーム アプリ]** を選択します。

4. プロジェクトに **InheritanceWalkthrough** という名前を付け、 **[OK]** を選択します。

     **InheritanceWalkthrough** プロジェクトが作成されて、**ソリューション エクスプローラー** に追加されます。

## <a name="add-a-linq-to-sql-classes-file-to-the-project"></a>LINQ to SQL クラス ファイルをプロジェクトに追加します

### <a name="to-add-a-linq-to-sql-file-to-the-project"></a>LINQ to SQL ファイルをプロジェクトに追加するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **LINQ to SQL クラス** テンプレートをクリックし、**[追加]** をクリックします。

     プロジェクトに *.dbml* ファイルが追加され、**O/R デザイナー** が開きます。

## <a name="create-the-inheritance-by-using-the-or-designer"></a>O/R デザイナーを使用した継承の作成
**ツールボックス** からデザイン サーフェイスに **継承** オブジェクトをドラッグして、継承を構成します。

### <a name="to-create-the-inheritance"></a>継承を作成するには

1. **サーバー エクスプローラー** または **データベース エクスプローラー** で、以前に作成した **Person** テーブルに移動します。

2. **Person** テーブルを **O/R デザイナー** のデザイン サーフェイスにドラッグします。

3. 2 つ目の **Person** テーブルを **O/R デザイナー** にドラッグし、名前を **Employee** に変更します。

4. **Person** オブジェクトから **Manager** プロパティを削除します。

5. **Employee** オブジェクトから、**Type**、**ID**、**FirstName**、および **LastName** の各プロパティを削除します。 (つまり、**Manager** 以外のプロパティをすべて削除します。)

6. **ツールボックス** の **[オブジェクト リレーショナル デザイナー]** タブで、**Person** オブジェクトと **Employee** オブジェクトの間に **継承** を作成します。 これを作成するには、**ツールボックス** の **[継承]** 項目をクリックしてマウス ボタンを放します。 次に、**O/R デザイナー** で、**Employee** オブジェクト、**Person** オブジェクトの順にクリックします。 これで、継承線の矢印が **Person** オブジェクトを指しています。

7. デザイン サーフェイスで **継承** 線をクリックします。

8. **[識別子プロパティ]** プロパティを **Type** に設定します。

9. **[派生クラスの識別子の値]** プロパティを **2** に設定します。

10. **[基本クラスの識別子の値]** プロパティを **1** に設定します。

11. **[継承の既定値]** プロパティを **Person** に設定します。

12. プロジェクトをビルドします。

## <a name="query-the-inherited-class-and-display-the-data-on-the-form"></a>継承されたクラスのクエリおよびフォームへのデータの表示
ここでは、オブジェクト モデル内の特定のクラスのクエリを実行するコードをフォームに追加します。

### <a name="to-create-a-linq-query-and-display-the-results-on-the-form"></a>LINQ クエリを作成し、フォームに結果を表示するには

1. **ListBox** を **Form1** にドラッグします。

2. フォームをダブルクリックして、`Form1_Load` イベント ハンドラーを作成します。

3. `Form1_Load` イベント ハンドラーに次のコードを追加します。

    ```vb
    Dim dc As New DataClasses1DataContext
    Dim results = From emp In dc.Persons _
        Where TypeOf emp Is Employee _
        Select emp

    For Each Emp As Employee In results
        ListBox1.Items.Add(Emp.LastName)
    Next
    ```

    ```csharp
    NorthwindDataContext dc = new DataClasses1DataContext();
    var results = from emp in dc.Persons
                  where emp is Employee
                  select emp;

    foreach(Employee Emp in results)
    {
        listBox1.Items.Add(Emp.LastName)
    }
    ```

## <a name="test-the-application"></a>アプリケーションをテストする
アプリケーションを実行し、リスト ボックスに表示されているレコードがすべて従業員 ( **[Type]** 列の値が 2 のレコード) であることを確認します。

### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. **F5** キーを押します。

2. **[Type]** 列の値が 2 のレコードのみが表示されていることを確認します。

3. フォームを閉じます  ( **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。)

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [方法: Visual Basic または C# でオブジェクト モデルを生成する](/dotnet/framework/data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp)
