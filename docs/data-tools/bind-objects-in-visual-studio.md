---
title: カスタムオブジェクトのデータバインド
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 2b046eaa4244d08c9fff9e2412471d018203de42
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648808"
---
# <a name="bind-objects-as-data-sources-in-visual-studio"></a>Visual Studio でオブジェクトをデータソースとしてバインドする

Visual Studio には、アプリケーションのデータソースとしてカスタムオブジェクトを操作するためのデザイン時ツールが用意されています。 UI コントロールにバインドするオブジェクトのデータベースからデータを格納する場合は、Entity Framework を使用してクラスまたはクラスを生成する方法をお勧めします。 Entity Framework は、すべての定型変更追跡コードを自動生成します。これは、DbSet オブジェクトで AcceptChanges を呼び出したときに、ローカルオブジェクトに対する変更がデータベースに自動的に保存されることを意味します。 詳細については、 [Entity Framework のドキュメント](https://ef.readthedocs.org/en/latest/)を参照してください。

> [!TIP]
> この記事のオブジェクトバインドの方法は、アプリケーションが既にデータセットに基づいている場合にのみ検討してください。 これらの方法は、データセットを既に使い慣れていて、処理するデータが表形式で複雑すぎる場合や大きすぎる場合にも使用できます。 DataReader を使用して直接オブジェクトにデータを読み込み、データバインドを使用せずに UI を手動で更新するなど、さらに簡単な例については、「 [ADO.NET を使用した単純なデータアプリケーションの作成](../data-tools/create-a-simple-data-application-by-using-adonet.md)」を参照してください。

## <a name="object-requirements"></a>オブジェクトの要件

カスタムオブジェクトが Visual Studio のデータデザインツールで動作するための唯一の要件は、オブジェクトに少なくとも1つのパブリックプロパティが必要であることです。

一般に、カスタムオブジェクトでは、アプリケーションのデータソースとして機能する特定のインターフェイス、コンストラクター、または属性は必要ありません。 ただし、オブジェクトを **[データソース]** ウィンドウからデザインサーフェイスにドラッグしてデータバインドコントロールを作成し、オブジェクトが <xref:System.ComponentModel.ITypedList> または <xref:System.ComponentModel.IListSource> インターフェイスを実装している場合は、オブジェクトに既定のコンストラクターが必要です。 そうしないと、Visual Studio はデータソースオブジェクトをインスタンス化できず、アイテムをデザイン画面にドラッグしたときにエラーが表示されます。

## <a name="examples-of-using-custom-objects-as-data-sources"></a>カスタムオブジェクトをデータソースとして使用する例

オブジェクトをデータソースとして使用する場合、アプリケーションロジックを実装する方法は数多くありますが、SQL データベースの場合は、Visual Studio で生成された TableAdapter オブジェクトを使用することによって簡略化できるいくつかの標準操作があります。 このページでは、Tableadapter を使用してこれらの標準プロセスを実装する方法について説明します。 カスタムオブジェクトを作成するためのガイドとしては使用しません。 たとえば、通常、オブジェクトの特定の実装やアプリケーションのロジックに関係なく、次のような標準的な操作を実行します。

- オブジェクトへのデータの読み込み (通常はデータベースから)。

- オブジェクトの型指定されたコレクションを作成します。

- オブジェクトをコレクションに追加したり、コレクションからオブジェクトを削除したりします。

- フォーム上のユーザーにオブジェクトデータを表示します。

- オブジェクトのデータの変更/編集。

- オブジェクトのデータをデータベースに保存し直す。

### <a name="load-data-into-objects"></a>オブジェクトへのデータの読み込み

この例では、Tableadapter を使用して、オブジェクトにデータを読み込みます。 既定では、Tableadapter は、データベースからデータをフェッチし、データテーブルを設定する2種類のメソッドを使用して作成されます。

- @No__t_0 メソッドは、返されたデータを既存のデータテーブルに格納します。

- @No__t_0 メソッドは、データが設定された新しいデータテーブルを返します。

データを使用してカスタムオブジェクトを読み込む最も簡単な方法は、`TableAdapter.GetData` メソッドを呼び出し、返されたデータテーブル内の行のコレクションをループ処理し、各オブジェクトに各行の値を設定することです。 TableAdapter に追加された任意のクエリのデータテーブルを返す `GetData` メソッドを作成できます。

> [!NOTE]
> Visual Studio では、TableAdapter クエリ `Fill`、既定で `GetData` されますが、これらの名前は任意の有効なメソッド名に変更できます。

次の例では、データテーブル内の行をループ処理し、オブジェクトにデータを設定する方法を示します。

[!code-csharp[VbRaddataConnecting#4](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_1.cs)]
[!code-vb[VbRaddataConnecting#4](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_1.vb)]

### <a name="create-a-typed-collection-of-objects"></a>オブジェクトの型指定されたコレクションを作成する

オブジェクトのコレクションクラスを作成することも、 [BindingSource コンポーネント](/dotnet/framework/winforms/controls/bindingsource-component)によって自動的に提供される型指定されたコレクションを使用することもできます。

オブジェクトのカスタムコレクションクラスを作成する場合は、<xref:System.ComponentModel.BindingList%601> から継承することをお勧めします。 このジェネリッククラスは、コレクションを管理するための機能を提供するだけでなく、Windows フォームのデータバインディングインフラストラクチャに通知を送信するイベントを発生させる機能を提供します。

@No__t_0 で自動的に生成されたコレクションは、型指定されたコレクションに対して <xref:System.ComponentModel.BindingList%601> を使用します。 アプリケーションで追加の機能が必要ない場合は、<xref:System.Windows.Forms.BindingSource> 内でコレクションを維持することができます。 詳細については、<xref:System.Windows.Forms.BindingSource> クラスの <xref:System.Windows.Forms.BindingSource.List%2A> プロパティを参照してください。

> [!NOTE]
> コレクションに <xref:System.ComponentModel.BindingList%601> の基本実装によって提供されていない機能が必要な場合は、必要に応じてクラスに追加できるように、カスタムコレクションを作成する必要があります。

次のコードは、`Order` オブジェクトの厳密に型指定されたコレクションのクラスを作成する方法を示しています。

[!code-csharp[VbRaddataConnecting#8](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_2.cs)]
[!code-vb[VbRaddataConnecting#8](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_2.vb)]

### <a name="add-objects-to-a-collection"></a>コレクションへのオブジェクトの追加

コレクションにオブジェクトを追加するには、カスタムコレクションクラスまたは <xref:System.Windows.Forms.BindingSource> の `Add` メソッドを呼び出します。

> [!NOTE]
> @No__t_0 メソッドは、<xref:System.ComponentModel.BindingList%601> から継承するときに、カスタムコレクションに対して自動的に提供されます。

次のコードは、<xref:System.Windows.Forms.BindingSource> 内の型指定されたコレクションにオブジェクトを追加する方法を示しています。

[!code-csharp[VbRaddataConnecting#5](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_3.cs)]
[!code-vb[VbRaddataConnecting#5](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_3.vb)]

次のコードは、<xref:System.ComponentModel.BindingList%601> から継承する型指定されたコレクションにオブジェクトを追加する方法を示しています。

> [!NOTE]
> この例では、`Orders` コレクションは `Customer` オブジェクトのプロパティです。

[!code-csharp[VbRaddataConnecting#6](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_4.cs)]
[!code-vb[VbRaddataConnecting#6](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_4.vb)]

### <a name="remove-objects-from-a-collection"></a>コレクションからオブジェクトを削除する

コレクションからオブジェクトを削除するには、カスタムコレクションクラスまたは <xref:System.Windows.Forms.BindingSource> の `Remove` または `RemoveAt` メソッドを呼び出します。

> [!NOTE]
> @No__t_2 から継承する場合、カスタムコレクションに対して `Remove` メソッドと `RemoveAt` メソッドが自動的に提供されます。

次のコードは、<xref:System.Windows.Forms.BindingSource.RemoveAt%2A> メソッドを使用して、<xref:System.Windows.Forms.BindingSource> 内の型指定されたコレクションからオブジェクトを検索および削除する方法を示しています。

[!code-csharp[VbRaddataConnecting#7](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_5.cs)]
[!code-vb[VbRaddataConnecting#7](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_5.vb)]

### <a name="display-object-data-to-users"></a>オブジェクトのデータをユーザーに表示する

オブジェクトのデータをユーザーに表示するには、**データソース構成**ウィザードを使用してオブジェクトデータソースを作成し、オブジェクト全体または個々のプロパティを **[データソース]** ウィンドウからフォームにドラッグします。

### <a name="modify-the-data-in-objects"></a>オブジェクトのデータを変更する

Windows フォームコントロールにデータバインドされているカスタムオブジェクト内のデータを編集するには、単にバインドされたコントロール (またはオブジェクトのプロパティで直接) のデータを編集します。 データバインディングアーキテクチャは、オブジェクト内のデータを更新します。

アプリケーションで変更を追跡する必要がある場合、および提案された変更を元の値にロールバックする必要がある場合は、オブジェクトモデルにこの機能を実装する必要があります。 データテーブルが提案された変更を追跡する方法の例については、「<xref:System.Data.DataRowState>、<xref:System.Data.DataSet.HasChanges%2A>、および <xref:System.Data.DataTable.GetChanges%2A>」を参照してください。

### <a name="save-data-in-objects-back-to-the-database"></a>オブジェクトのデータをデータベースに保存する

オブジェクトから TableAdapter の DBDirect メソッドに値を渡すことによって、データベースにデータを保存し直します。

Visual Studio によって、データベースに対して直接実行できる DBDirect メソッドが作成されます。 これらのメソッドは、DataSet オブジェクトまたは DataTable オブジェクトを必要としません。

|TableAdapter DBDirect メソッド|説明|
| - |-----------------|
|`TableAdapter.Insert`|データベースに新しいレコードを追加します。これにより、個々の列の値をメソッドのパラメーターとして渡すことができます。|
|`TableAdapter.Update`|データベース内の既存のレコードを更新します。 Update メソッドは、元の列と新しい列の値をメソッドのパラメーターとして受け取ります。 元の値は元のレコードを検索するために使用され、新しい値はそのレコードを更新するために使用されます。<br /><br /> @No__t_0 メソッドは、<xref:System.Data.DataRow>s の <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow>、または配列をメソッドパラメーターとして取得することによって、データセットの変更をデータベースに戻すためにも使用されます。|
|`TableAdapter.Delete`|メソッドパラメーターとして渡された元の列の値に基づいて、データベースから既存のレコードを削除します。|

オブジェクトのコレクションからデータを保存するには、オブジェクトのコレクションをループ処理します (たとえば、for-next ループを使用します)。 TableAdapter の DBDirect メソッドを使用して、各オブジェクトの値をデータベースに送信します。

次の例は、`TableAdapter.Insert` DBDirect メソッドを使用して、新しい顧客をデータベースに直接追加する方法を示しています。

[!code-csharp[VbRaddataSaving#23](../data-tools/codesnippet/CSharp/bind-objects-in-visual-studio_6.cs)]
[!code-vb[VbRaddataSaving#23](../data-tools/codesnippet/VisualBasic/bind-objects-in-visual-studio_6.vb)]

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)