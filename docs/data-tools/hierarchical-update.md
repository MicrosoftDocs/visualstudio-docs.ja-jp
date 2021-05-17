---
title: 階層更新
description: 階層更新を確認します。これには参照整合性規則を維持しながら、更新済みのデータ (2 つ以上の関連テーブルのあるデータセットから) の DB への保存が必要です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
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
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: d43d4267ce0e180a525e990e372b7a6773a9cc51
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215813"
---
# <a name="hierarchical-update"></a>階層更新

*階層更新* とは、参照整合性規則を維持しながら、更新済みのデータ (複数の関連テーブルのあるデータセットから) をデータベースに保存するプロセスを表します。 *参照整合性* とは、関連レコードの挿入、更新、および削除の動作を制御するデータベース内の制約によって提供される整合性規則を表します。 たとえば、その顧客の注文を作成する前に、顧客レコードの作成を強制することは参照整合性です。  データセット内のリレーションシップの詳細については、[データセット間のリレーションシップ](../data-tools/relationships-in-datasets.md)に関するページを参照してください。

階層更新機能では、`TableAdapterManager` を使用して、型指定されたデータセットで `TableAdapter` を管理します。 `TableAdapterManager`コンポーネントは、.NET 型ではなく、Visual Studio で生成されたクラスです。 **[データ ソース]** ウィンドウから Windows フォームまたは WPF ページにテーブルをドラッグすると、Visual Studio によって TableAdapterManager 型の変数がフォームまたはページに追加され、デザイナーのコンポーネント トレイに表示されます。 `TableAdapterManager` クラスの詳細については、[TableAdapter](../data-tools/create-and-configure-tableadapters.md)」の TableAdapterManager リファレンスに関するセクションを参照してください。

既定で、データセットでは関連テーブルが "リレーションシップのみ" として扱われ、これは、外部キー制約が適用されないことを意味します。 デザイン時にその設定を変更するには、**データセット デザイナー** を使用します。 2 つのテーブル間のリレーションシップの線を選択して、 **[リレーションシップ]** ダイアログ ボックスを表示します。 ここで行った変更によって、関連テーブルの変更をデータベースに戻すときの `TableAdapterManager` の動作が決まります。

## <a name="enable-hierarchical-update-in-a-dataset"></a>データセットの階層更新を有効にする

プロジェクトで追加または作成されたすべての新しいデータセットでは、階層更新が既定で有効になっています。 階層更新をオンまたはオフにするには、型指定されたデータセットの **[階層更新]** プロパティを **[True]** または **[False]** に設定します。

![階層更新の設定](../data-tools/media/hierarchical-update-setting.png)

## <a name="create-a-new-relation-between-tables"></a>テーブル間に新しいリレーションシップを作成する

2 つのテーブル間に新しいリレーションシップを作成するには、データセット デザイナーで、各テーブルのタイトル バーを選択し、右クリックして、 **[リレーションシップの追加]** を選択します。

![階層更新の [リレーションシップの追加] メニュー](../data-tools/media/hierarchical-update-add-relation-menu.png)

## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>外部キー制約、連鎖更新、および連鎖削除について

生成されたデータセット コードで、データベースでの外部キー制約と連鎖動作がどのように作成されるかを理解することは重要です。

既定では、データセットのデータ テーブルは、データベースでのリレーションシップと一致するリレーションシップ (<xref:System.Data.DataRelation>) が設定された状態で生成されます。 ただし、データセットでのリレーションシップは、外部キー制約としては生成されません。 <xref:System.Data.DataRelation> は、<xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> または <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> が有効でない状態で **[リレーションシップのみ]** として構成されます。

連鎖更新と連鎖削除は、データベースのリレーションシップで連鎖更新や連鎖削除が有効になっている場合でも、既定で無効になっています。 たとえば、新しい顧客と新しい注文を作成した後にデータを保存しようとすると、データベースに定義された外部キー制約との競合が発生することがあります。 詳細については、「[データセットの読み込み中に制約をオフにする](turn-off-constraints-while-filling-a-dataset.md)」を参照してください。

## <a name="set-the-order-to-perform-updates"></a>更新を実行する順序の設定

更新を実行する順序を設定すると、データセットのすべてのテーブルで変更されたすべてのデータを保存するために必要な個々の挿入、更新、および削除の順序が設定されます。 階層更新が有効な場合、まず挿入が実行され、次に更新、削除の順で実行されます。 `TableAdapterManager` には、更新、挿入、削除の順に実行できる `UpdateOrder` プロパティも用意されています。

> [!NOTE]
> 更新順序にはすべてが含まれることを理解することが重要です。 つまり、更新が実行されるときに、データセット内のすべてのテーブルに対して、挿入、次に削除が実行されます。

`UpdateOrder` プロパティを設定するには、[データ ソース ウィンドウ](add-new-data-sources.md#data-sources-window)からフォームに項目をドラッグした後、コンポーネント トレイの `TableAdapterManager` をクリックし、 **[プロパティ]** ウィンドウで `UpdateOrder` プロパティを設定します。

## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>階層更新を実行する前にデータセットのバックアップ コピーを作成する

データを保存すると (`TableAdapterManager.UpdateAll()` メソッドを呼び出すことにより)、`TableAdapterManager` は単一のトランザクションで各テーブルのデータの更新を試みます。 任意のテーブルの更新時に、なんらかが失敗した場合、トランザクション全体がロールバックされます。 ほとんどの状況では、ロールバックによってアプリケーションがその元の状態に戻ります。

ただし、バックアップ コピーからデータセットを復元することもできます。 この 1 つの例は、自動インクリメント値を使用している場合に発生する可能性があります。 たとえば、保存操作に失敗した場合、データセットで自動インクリメント値がリセットされず、データセットによって自動インクリメント値が作成され続けることがあります。 これにより、アプリケーションで許容できない可能性がある番号付けのずれが発生します。 これが問題となる状況では、`TableAdapterManager` に備わっている `BackupDataSetBeforeUpdate` プロパティを使用して、トランザクションが失敗した場合に既存のデータセットをバックアップ コピーと置き換えることができます。

> [!NOTE]
> バックアップ コピーは、`TableAdapterManager.UpdateAll` メソッドの実行中はメモリ内にのみ存在します。 したがって、このバックアップ データセットは元のデータセットを置き換えるか、`TableAdapterManager.UpdateAll` メソッドが実行を終了するとすぐにスコープ外になるため、このバックアップ データセットにプログラムからアクセスすることはできません。

## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>階層更新を実行するように生成された保存コードを変更する

データセットでの関連データ テーブルへの変更をデータベースに保存するには、`TableAdapterManager.UpdateAll` メソッドを呼び出し、関連テーブルが含まれるデータセットの名前を渡します。 たとえば、NorthwindDataset 内のすべてのテーブルの更新をバックエンドのデータベースに送信するには、`TableAdapterManager.UpdateAll(NorthwindDataset)` メソッドを実行します。

**[データ ソース]** ウィンドウから項目をドロップすると、各テーブルにデータを読み込むコード (`TableAdapter.Fill` メソッド) が `Form_Load` イベントに自動的に追加されます。 <xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタン クリック イベントにも、データセットのデータをデータベースに保存するコード (`TableAdapterManager.UpdateAll` メソッド) が追加されます。

生成された保存コードには、`CustomersBindingSource.EndEdit` メソッドを呼び出すコード行も含まれています。 具体的には、フォームに最初に追加された <xref:System.Windows.Forms.BindingSource> の <xref:System.Windows.Forms.BindingSource.EndEdit%2A> メソッドを呼び出します。 つまり、このコードは、 **[データ ソース]** ウィンドウからフォームに最初にドラッグされたテーブルに対してのみ生成されます。 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 呼び出しは、現在編集中のデータ バインド コントロールで実行されている変更をコミットします。 したがって、あるデータ バインド コントロールにフォーカスがある状態で **[保存]** ボタンをクリックすると、実際の保存 (`TableAdapterManager.UpdateAll` メソッド) が実行される前に、そのコントロール内のすべての保留中の編集がコミットされます。

> [!NOTE]
> **データセット デザイナー** では、フォームに最初にドロップされたテーブルに対してのみ `BindingSource.EndEdit` コードが追加されます。 したがって、フォーム上の各関連テーブルに対して、`BindingSource.EndEdit` メソッドを呼び出すコード行を手動で追加する必要があります。 つまり、このチュートリアルでも、`OrdersBindingSource.EndEdit` メソッドの呼び出しを追加する必要があります。

### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>保存前に、関連テーブルへの変更をコミットするコードを更新するには

1. <xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタンをダブルクリックし、コード エディターで **Form1** を開きます。

2. `OrdersBindingSource.EndEdit` メソッドを呼び出す行の後に、`CustomersBindingSource.EndEdit` メソッドを呼び出すコード行を追加します。 **[保存]** ボタン クリック イベントのコードは、次のようになります。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet1":::

データベースにデータを保存する前に関連子テーブルに対する変更をコミットするだけでなく、新しい子レコードをデータセットに追加する前に、新しく作成された親レコードをコミットすることが必要な場合もあります。 つまり、外部キー制約により、新しい子レコード (`Orders`) をデータセットに追加できるようになる前に、データセットに新しい親レコード (`Customer`) を追加する必要がある場合があります。 この操作を行うには、子 `BindingSource.AddingNew` イベントを使用します。

> [!NOTE]
> 新しい親レコードをコミットする必要があるかどうかは、データ ソースへのバインドに使用されるコントロールの種類によって異なります。 このチュートリアルでは、親テーブルとのバインドに個別のコントロールを使用します。 これには、新しい親レコードをコミットする追加のコードが必要になります。 代わりに、親レコードが <xref:System.Windows.Forms.DataGridView> のような複雑なバインド コントロールに表示される場合は、親レコードに対するこの追加の <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 呼び出しは必要ありません。 これは、コントロールの基になるデータバインド機能によって、新しいレコードのコミットが行われるためです。

### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>データセットで新しい子レコードを追加する前に親レコードをコミットするコードを追加するには

1. `OrdersBindingSource.AddingNew` イベントのイベント ハンドラーを作成します。

    - デザイン ビューで **Form1** を開いて、コンポーネント トレイの **[OrdersBindingSource]** をクリックし、 **[プロパティ]** ウィンドウで **[イベント]** を選択して、 **[AddingNew]** イベントをダブルクリックします。

2. `CustomersBindingSource.EndEdit` メソッドを呼び出すコード行をイベント ハンドラーに追加します。 `OrdersBindingSource_AddingNew` イベント ハンドラー内のコードは、次のようになります。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet2":::

## <a name="tableadaptermanager-reference"></a>TableAdapterManager リファレンス

既定では、関連テーブルを含むデータセットを作成すると、`TableAdapterManager` クラスが生成されます。 クラスが生成されないようにするには、データセットの `Hierarchical Update` プロパティの値を false に変更します。 Windows フォームまたは WPF ページのデザイン サーフェイスにリレーションシップを持つテーブルをドラッグすると、Visual Studio ではクラスのメンバー変数が宣言されます。 データ バインドを使用しない場合は、手動で変数を宣言する必要があります。

`TableAdapterManager` クラスは .NET 型ではありません。 このため、ドキュメントで確認することができません。 これは、デザイン時にデータセット作成プロセスの一部として作成されます。

`TableAdapterManager` クラスのよく使用されるメソッドとプロパティを次に示します。

|メンバー|説明|
|------------|-----------------|
|`UpdateAll` メソッド|すべてのデータ テーブルのすべてのデータを保存します。|
|`BackUpDataSetBeforeUpdate` プロパティ|`TableAdapterManager.UpdateAll` メソッドを実行する前に、データセットのバックアップ コピーを作成するかどうかを決定します。ブール型です。|
|*tableName* `TableAdapter` プロパティ|`TableAdapter` を表します。 生成された `TableAdapterManager` には、管理される各 `TableAdapter` のプロパティが含まれています。 たとえば、Customers テーブルと Orders テーブルがあるデータセットは、`CustomersTableAdapter` プロパティと `OrdersTableAdapter` プロパティを含む `TableAdapterManager` によって生成されます。|
|`UpdateOrder` プロパティ|個々の挿入、更新、削除コマンドの順序を制御します。 これは、`TableAdapterManager.UpdateOrderOption` 列挙のいずれかの値に設定します。<br /><br /> 既定では、`UpdateOrder` は **InsertUpdateDelete** に設定されます。 これは、データセット内のすべてのテーブルに対して、挿入、更新、削除の順に実行されることを意味します。|

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
