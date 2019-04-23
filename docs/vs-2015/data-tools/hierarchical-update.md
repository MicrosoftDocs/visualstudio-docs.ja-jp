---
title: 階層更新 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- saving data, changed data
- data [Visual Basic], hierarchical update
- saving updated data
- datasets [Visual Basic], hierarchical update
- hierarchical update
- saving data, hierarchical update
- modified data saving
- updated data saving
- related tables, saving
ms.assetid: 68bae3f6-ec9b-45ee-a33a-69395029f54c
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 17eb5c1ca2ad35b7a510c5a70d3ad5c5f741c69d
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60063401"
---
# <a name="hierarchical-update"></a>階層更新
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

階層的な更新プログラム *、参照整合性を維持しながら、データベースに戻す (2 つ以上の関連テーブルを含むデータセット) から更新されたデータを保存するプロセスを指します。 *参照整合性*の挿入、更新、および関連レコードを削除する動作を制御するデータベース内の制約によって定義される一貫性規則を参照します。 たとえば、その顧客の注文を作成するを許可する前に、顧客レコードの作成を強制する参照の整合性を勧めします。  データセットのリレーションシップの詳細については、次を参照してください[データセットのリレーションシップ。](../data-tools/relationships-in-datasets.md)  
  
 階層更新機能を使用して、`TableAdapterManager`を管理する、`TableAdapter`型指定された dataset の s。 `TableAdapterManager`コンポーネントは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]-は、クラスを生成の一部、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]します。 データ ソース ウィンドウから Windows フォームまたは WPF ページにテーブルをドラッグするとは、Visual Studio がフォームまたはページで、TableAdapterManager の型の変数を追加し、コンポーネント トレイにデザイナーで参照してください。 詳細については、`TableAdapterManager`クラスの TableAdapterManager リファレンスのセクションを参照してください[TableAdapterManager の概要](http://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)します。  
  
 既定では、データセットは、外部キー制約を適用しないことを意味する「リレーションのみ、」として関連テーブルを処理します。 データセット デザイナーを使用して、デザイン時にその設定を変更できます。 2 つのテーブル間の関係の行を選択、**関係** ダイアログ ボックス。 TableAdapterManager 動作ときにここで加えた変更が決定が元のデータベースに関連するテーブルに、変更も送信します。  
  
## <a name="enablehierarchical-update-in-a-dataset"></a>データセット内の Enablehierarchical update  
 プロジェクトで追加または作成されたすべての新しいデータセットでは、階層更新が既定で有効になっています。 設定して、階層更新をオンまたはオフに、**階層更新**をデータセット デザイナーで型指定されたデータセットのプロパティ**True**または**False**:  
  
 ![階層更新設定](../data-tools/media/hierarchical-update-setting.png "階層更新の設定")  
  
## <a name="create-a-new-relation-between-tables"></a>テーブル間に新しいリレーションシップを作成します。  
 2 つのテーブル間に新しいリレーションシップを作成する、データセット デザイナーで、各テーブルのタイトル バーを選択します。 右クリックし選択**リレーションを追加**します。  
  
 ![階層更新の追加 メニューの関係](../data-tools/media/hierarchical-update-add-relation-menu.png "階層更新 メニューの関係を追加します。")  
  
## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>Foreign key 制約、カスケード更新プログラム、および削除を理解します。  
 生成されたデータセット コードで、データベースでの外部キー制約と連鎖動作がどのように作成されるかを理解することは重要です。  
  
 既定では、データセットのデータ テーブルは、データベースでのリレーションシップと一致するリレーションシップ (<xref:System.Data.DataRelation>) が設定された状態で生成されます。 ただし、データセットでのリレーションシップは、外部キー制約としては生成されません。 <xref:System.Data.DataRelation>として構成されている**リレーションシップのみ**せず<xref:System.Data.ForeignKeyConstraint.UpdateRule%2A>または<xref:System.Data.ForeignKeyConstraint.DeleteRule%2A>有効にします。  
  
 連鎖更新と連鎖削除は、データベースのリレーションシップで連鎖更新や連鎖削除が有効になっている場合でも、既定で無効になっています。 たとえば、新しい顧客と新しい注文を作成し、データを保存しようは、データベースで定義されている外部キー制約を持つの競合を発生することが。 詳細については、「[方法 :データセット内の Foreign Key 制約を構成する](http://msdn.microsoft.com/library/3954c388-e209-4a67-a34e-5ca106282f8e)します。  
  
## <a name="set-the-order-to-perform-updates"></a>更新プログラムを実行する順序を設定します。  
 更新プログラムを実行する順序を設定するデータセットのすべてのテーブルで変更されたすべてのデータを保存する個々 の注文を挿入、更新、および削除したセットが必要です。 階層更新が有効な場合、まず挿入が実行され、次に更新、削除の順で実行されます。 `TableAdapterManager` には、更新、挿入、削除の順に実行できる `UpdateOrder` プロパティも用意されています。  
  
> [!NOTE]
>  更新順序は、すべてが含まれているかを理解しておく必要があります。 つまり、更新プログラムが実行されると、挿入、および削除の後は、データセット内のすべてのテーブルに対して実行されます。  
  
 設定する、`UpdateOrder`から項目をドラッグした後、プロパティ、[データ ソース ウィンドウ](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)、フォームに次のように選択します、`TableAdapterManager`コンポーネント トレイ、および設定して、`UpdateOrder`プロパティ、 **プロパティ。** ウィンドウ。 詳細については、「[方法 :階層更新を実行するときに、順序を設定](http://msdn.microsoft.com/library/a0734935-78dd-4c0b-80d7-5e7925789c83)します。  
  
## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>階層更新を実行する前に、データセットのバックアップ コピーを作成します。  
 データを保存すると (`TableAdapterManager.UpdateAll()` メソッドを呼び出すことにより)、`TableAdapterManager` は単一のトランザクションで各テーブルのデータの更新を試みます。 任意のテーブルの更新時に、なんらかが失敗した場合、トランザクション全体がロールバックされます。 ほとんどの場合は、ロールバックは、アプリケーションを元の状態を返します。  
  
 ただし、バックアップ コピーからデータセットを復元することもできます。 この 1 つの例には、自動インクリメント値を使用している場合があります。 たとえば、保存操作が成功しなかった、自動インクリメント値は、データセットではリセットされませんおよび自動インクリメント値を作成するデータセットが続行されます。これには、アプリケーションで許容されることができない可能性がある番号付けギャップが残されます。 これが問題となる状況では、`TableAdapterManager` に備わっている `BackupDataSetBeforeUpdate` プロパティを使用して、トランザクションが失敗した場合に既存のデータセットをバックアップ コピーと置き換えることができます。  
  
> [!NOTE]
>  バックアップ コピーは、中にメモリ内にのみ、`TableAdapterManager.UpdateAll`メソッドが実行されています。 そのためはこのバックアップ データセットにプログラムでアクセス元のデータセットを置き換えるかスコープから外れるのですぐ、`TableAdapterManager.UpdateAll`メソッドの実行が完了します。  
  
## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>階層更新を実行するコードを保存、生成された変更します。  
 データセットでの関連データ テーブルへの変更をデータベースに保存するには、`TableAdapterManager.UpdateAll` メソッドを呼び出し、関連テーブルが含まれるデータセットの名前を渡します。 たとえば、NorthwindDataset 内のすべてのテーブルの更新をバックエンドのデータベースに送信するには、`TableAdapterManager.UpdateAll(NorthwindDataset)` メソッドを実行します。  
  
 **[データ ソース]** ウィンドウから項目をドロップすると、各テーブルにデータを読み込むコード (`TableAdapter.Fill` メソッド) が `Form_Load` イベントに自動的に追加されます。 <xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタン クリック イベントにも、データセットのデータをデータベースに保存するコード (`TableAdapterManager.UpdateAll` メソッド) が追加されます。  
  
 生成された保存コードには、`CustomersBindingSource.EndEdit` メソッドを呼び出すコード行も含まれています。 具体的には、呼び出し、<xref:System.Windows.Forms.BindingSource.EndEdit%2A>最初のメソッド<xref:System.Windows.Forms.BindingSource>フォームに追加されています。 つまり、このコードはからドラッグされる最初のテーブルの生成のみ、**データソース**ウィンドウから、フォームにします。 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 呼び出しは、現在編集中のデータ バインド コントロールで実行されている変更をコミットします。 したがって、あるデータ バインド コントロールにフォーカスがある状態で **[保存]** ボタンをクリックすると、実際の保存 (`TableAdapterManager.UpdateAll` メソッド) が実行される前に、そのコントロール内のすべての保留中の編集がコミットされます。  
  
> [!NOTE]
>  データセット デザイナーが追加されるだけ、`BindingSource.EndEdit`がフォームにドロップされる最初のテーブルのコード。 したがって、フォーム上の各関連テーブルに対して、`BindingSource.EndEdit` メソッドを呼び出すコード行を手動で追加する必要があります。 つまり、このチュートリアルでも、`OrdersBindingSource.EndEdit` メソッドの呼び出しを追加する必要があります。  
  
#### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>保存前に、関連テーブルへの変更をコミットするコードを更新するには  
  
1. <xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタンをダブルクリックし、コード エディターで **Form1** を開きます。  
  
2. `OrdersBindingSource.EndEdit` メソッドを呼び出す行の後に、`CustomersBindingSource.EndEdit` メソッドを呼び出すコード行を追加します。 **[保存]** ボタン クリック イベントのコードは、次のようになります。  
  
    [!code-csharp[VSProDataOrcasHierarchicalUpdate#1](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs#1)]
    [!code-vb[VSProDataOrcasHierarchicalUpdate#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb#1)]  
  
   データベースにデータを保存する前に関連子テーブルに対する変更をコミットするだけでなく、新しい子レコードをデータセットに追加する前に、新しく作成された親レコードをコミットすることが必要な場合もあります。 つまり、外部キー制約により、新しい子レコード (Orders) をデータセットに追加する前に、データセットに新しい親レコード (Customer) を追加することが必要な場合もあります。 この操作を行うには、子 `BindingSource.AddingNew` イベントを使用します。  
  
> [!NOTE]
>  新しい親レコードをコミットする必要があるかどうかは、データ ソースにバインドするために使用されるコントロールの種類によって異なります。 このチュートリアルでは、親テーブルにバインドする個々 のコントロールを使用します。 これには、新しい親レコードをコミットするコードを追加が必要です。 親レコードは、複雑なバインド コントロールに代わりに表示されていた場合と同様、<xref:System.Windows.Forms.DataGridView>この追加<xref:System.Windows.Forms.BindingSource.EndEdit%2A>呼び出しの親レコードは必要ありません。 これは、コントロールの基になるデータ バインディング機能によって、新しいレコードのコミットが行われるためです。  
  
#### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>データセットで新しい子レコードを追加する前に親レコードをコミットするコードを追加するには  
  
1. `OrdersBindingSource.AddingNew` イベントのイベント ハンドラーを作成します。  
  
    - 開いている**Form1**デザイン ビューで、次のように選択します**OrdersBindingSource** 、コンポーネント トレイに次のように選択します。**イベント**で、**プロパティ**ウィンドウ、および。ダブルクリックし、 **AddingNew**イベント。  
  
2. 呼び出すイベント ハンドラーにコードの行を追加、`CustomersBindingSource.EndEdit`メソッド。 `OrdersBindingSource_AddingNew` イベント ハンドラー内のコードは、次のようになります。  
  
     [!code-csharp[VSProDataOrcasHierarchicalUpdate#2](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs#2)]
     [!code-vb[VSProDataOrcasHierarchicalUpdate#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb#2)]  
  
## <a name="tableadaptermanager-reference"></a>TableAdapterManager の参照  
 既定で、`TableAdapterManager`関連テーブルを含むデータセットを作成するときにクラスが生成されます。 値を変更するクラスが生成されていることを防ぐために、`Hierarchical Update`を false に、データセットのプロパティ。 Windows フォームまたは WPF ページのデザイン サーフェイスに関係のあるテーブルをドラッグすると、Visual Studio は、クラスのメンバー変数を宣言します。 データ バインドを使用しない場合は、手動で変数を宣言する必要があります。  
  
 `TableAdapterManager`クラスの一部、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]します。 そのため、ドキュメントを検索することはできません。 デザイン時にデータセットの作成プロセスの一環として作成されます。  
  
 よく使用されるメソッドとプロパティの次のとおり、`TableAdapterManager`クラス。  
  
|メンバー|説明|  
|------------|-----------------|  
|`UpdateAll` メソッド|すべてのデータ テーブルからすべてのデータを保存します。|  
|`BackUpDataSetBeforeUpdate` プロパティ|実行する前に、データセットのバックアップ コピーを作成するかどうか、`TableAdapterManager.UpdateAll`メソッド。ブール値。|  
|*tableName* `TableAdapter`プロパティ|表す、`TableAdapter`します。 生成された`TableAdapterManager`の各プロパティを含む`TableAdapter`を管理します。 たとえば、Customers と Orders テーブルを含むデータセットが生成されます、`TableAdapterManager`を格納している`CustomersTableAdapter`と`OrdersTableAdapter`プロパティ。|  
|`UpdateOrder` プロパティ|個々 の insert、update、および delete コマンドの順序を制御します。 この設定の値の 1 つに、`TableAdapterManager.UpdateOrderOption`列挙体。<br /><br /> 既定で、`UpdateOrder`に設定されている**InsertUpdateDelete**します。 つまり、挿入、し、更新、および削除は、データセット内のすべてのテーブルに対して実行されます。 詳細については、「[方法 :階層更新を実行するときに、順序を設定](http://msdn.microsoft.com/library/a0734935-78dd-4c0b-80d7-5e7925789c83)します。|  
  
## <a name="see-also"></a>関連項目  
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
