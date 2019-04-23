---
title: 'チュートリアル: 単一テーブル継承 (O/R デザイナー) を使用して LINQ to SQL クラスを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 63bc6328-e0df-4655-9ce3-5ff74dbf69a4
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 61509b7427a9c1a95fe15bba93d231f0dc37d136
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59664995"
---
# <a name="walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-or-designer"></a>チュートリアル: 単一テーブル継承 (O/R デザイナー) を使用して LINQ to SQL クラスを作成します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[LINQ to Visual Studio での SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)リレーショナル システムに実装されている通常の単一テーブル継承をサポートしています。 このチュートリアルで提供される汎用的な手順、[方法。O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)トピックでの継承の使用を示すために、実際のデータを提供し、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]します。  
  
 このチュートリアルでは次のタスクを行います。  
  
-   データベース テーブルを作成し、データを追加します。  
  
-   Windows フォーム アプリケーションを作成します。  
  
-   [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] ファイルをプロジェクトに追加します。  
  
-   新しいエンティティ クラスを作成します。  
  
-   継承を使用するようにエンティティ クラスを構成します。  
  
-   継承されたクラスをクエリします。  
  
-   Windows フォームにデータを表示します。  
  
## <a name="create-a-table-to-inherit-from"></a>継承するテーブルの作成  
 継承の動作を確認するには、小さな Person テーブルを作成し、それをベース クラスとして使用して、そのテーブルから継承する Employee オブジェクトを作成します。  
  
#### <a name="to-create-a-base-table-to-demonstrate-inheritance"></a>ベース テーブルを作成して継承の動作を確認するには  
  
1.  **サーバー エクスプ ローラー**/**データベース エクスプ ローラー**を右クリックし、**テーブル**ノードをクリックします**新しいテーブルの追加**します。  
  
    > [!NOTE]
    >  Northwind データベースを使用することも、テーブルを追加できる他の任意のデータベースを使用することもできます。  
  
2.  テーブル デザイナーで、次の列をテーブルに追加します。  
  
    |列名|データ型|Null を許容|  
    |-----------------|---------------|-----------------|  
    |**ID**|**int**|**False**|  
    |**Type**|**int**|**True**|  
    |**FirstName**|**nvarchar(200)**|**False**|  
    |**LastName**|**nvarchar(200)**|**False**|  
    |**Manager**|**int**|**True**|  
  
3.  ID 列を主キーとして設定します。  
  
4.  テーブルを **Person** という名前で保存します。  
  
## <a name="add-data-to-the-table"></a>テーブルへのデータの追加  
 継承が正しく構成されていることを確認できるように、単一テーブル継承のテーブルの各クラスにデータを入力する必要があります。  
  
#### <a name="to-add-data-to-the-table"></a>テーブルにデータを追加するには  
  
1.  データ ビューでテーブルを開きます  (を右クリックし、**人**テーブルに**サーバー エクスプ ローラー**/**データベース エクスプ ローラー**クリック**テーブル データの表示**)。  
  
2.  テーブルに次のデータをコピーします。 (コピーして、結果ウィンドウで、行全体を選択して、テーブルに貼り付けます。)  
  
    ||||||  
    |-|-|-|-|-|  
    |**ID**|**Type**|**FirstName**|**LastName**|**Manager**|  
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
  
## <a name="create-a-new-project"></a>新しいプロジェクトの作成  
 これでテーブルが作成されたので、新しいプロジェクトを作成して継承の構成を実際に行います。  
  
#### <a name="to-create-the-new-windows-application"></a>新しい Windows アプリケーションを作成するには  
  
1.  **ファイル**] メニューの [新しいプロジェクトを作成します。  
  
2.  プロジェクトに名前を**InheritanceWalkthrough**します。  
  
    > [!NOTE]
    >  [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]は Visual Basic プロジェクトと C# プロジェクトでサポートされています。 新しいプロジェクトはこれらの言語のどちらかで作成してください。  
  
3.  をクリックして、 **Windows フォーム アプリケーション**テンプレートとクリック**OK**。 詳細については、次を参照してください。[クライアント アプリケーション](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)します。  
  
4.  InheritanceWalkthrough プロジェクトが作成されに追加**ソリューション エクスプ ローラー**します。  
  
## <a name="add-a-linq-to-sql-classes-file-to-the-project"></a>LINQ to SQL クラス ファイルをプロジェクトに追加します。  
  
#### <a name="to-add-a-linq-to-sql-file-to-the-project"></a>LINQ to SQL ファイルをプロジェクトに追加するには  
  
1.  **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。  
  
2.  **LINQ to SQL クラス** テンプレートをクリックし、**[追加]** をクリックします。  
  
     プロジェクトに .dbml ファイルが追加され、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]が開きます。  
  
## <a name="create-the-inheritance-by-using-the-or-designer"></a>O/R デザイナーを使用した継承の作成  
 **ツールボックス**からデザイン サーフェイスに**継承**オブジェクトをドラッグして、継承を構成します。  
  
#### <a name="to-create-the-inheritance"></a>継承を作成するには  
  
1.  **サーバー エクスプ ローラー**/**データベース エクスプ ローラー**に移動し、 **Person**先ほど作成したテーブル。  
  
2.  ドラッグ、 **Person**テーブルを[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]デザイン サーフェイス。  
  
3.  1 秒あたりのドラッグ**Person**テーブルを[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]し、名前に変更**従業員**します。  
  
4.  **Person** オブジェクトから **Manager** プロパティを削除します。  
  
5.  **Employee** オブジェクトから、**Type**、**ID**、**FirstName**、および **LastName** の各プロパティを削除します。 (つまり、**Manager** 以外のプロパティをすべて削除します。)  
  
6.  **ツールボックス**の **[オブジェクト リレーショナル デザイナー]** タブで、**Person** オブジェクトと **Employee** オブジェクトの間に**継承**を作成します。 これを作成するには、**ツールボックス**の **[継承]** 項目をクリックしてマウス ボタンを放します。 次に、クリックして、**従業員**オブジェクトをクリックし、 **Person**内のオブジェクト、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。 継承線の矢印が指す、 **Person**オブジェクト。  
  
7.  デザイン サーフェイスで**継承**線をクリックします。  
  
8.  **[識別子プロパティ]** プロパティを **Type** に設定します。  
  
9. **[派生クラスの識別子の値]** プロパティを **2** に設定します。  
  
10. **[基本クラスの識別子の値]** プロパティを **1** に設定します。  
  
11. **[継承の既定値]** プロパティを **Person** に設定します。  
  
12. プロジェクトをビルドします。  
  
## <a name="query-the-inherited-class-and-display-the-data-on-the-form"></a>継承されたクラスのクエリおよびフォームへのデータの表示  
 オブジェクト モデル内の特定のクラスを照会するコードをフォームに追加します。  
  
#### <a name="to-create-a-linq-query-and-display-the-results-on-the-form"></a>LINQ クエリを作成し、フォームに結果を表示するには  
  
1.  ドラッグ、 **ListBox**を Form1 にします。  
  
2.  フォームをダブルクリックして、`Form1_Load` イベント ハンドラーを作成します。  
  
3.  `Form1_Load` イベント ハンドラーに次のコードを追加します。  
  
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
  
## <a name="test-the-application"></a>アプリケーションのテスト  
 アプリケーションを実行し、リスト ボックスに表示されているレコードがすべて従業員 ([Type] 列の値が 2 のレコード) であることを確認します。  
  
#### <a name="to-test-the-application"></a>アプリケーションをテストするには  
  
1.  F5 キーを押します。  
  
2.  [Type] 列の値が 2 のレコードのみが表示されていることを確認します。  
  
3.  フォームを閉じます  (**[デバッグ]** メニューの **[デバッグの停止]** をクリックします。)  
  
## <a name="see-also"></a>関連項目  
 [LINQ to Visual Studio での SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [方法: LINQ to SQL クラス (O/R デザイナー) をプロジェクトに追加します。](http://msdn.microsoft.com/library/7bb184ab-ec54-4cda-b706-604b2b4a3ed6)   
 [チュートリアル: LINQ to SQL クラス (O/R デザイナー) を作成します。](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [方法: 更新、挿入、および削除 (O/R デザイナー) を実行するストアド プロシージャを割り当てる](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [方法: Visual Basic または C# でオブジェクト モデルを生成する](http://msdn.microsoft.com/library/a0c73b33-5650-420c-b9dc-f49310c201ee)
