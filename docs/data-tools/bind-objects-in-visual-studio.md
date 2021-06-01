---
title: カスタム オブジェクトをデータ バインドする
description: Visual Studio でオブジェクトをデータ ソースとしてバインドします。 カスタム オブジェクトをアプリケーションのデータ ソースとして操作するための、デザイン時ツールを使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 140700615759404f02109c4506f4c27d083a74b1
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215540"
---
# <a name="bind-objects-as-data-sources-in-visual-studio"></a>Visual Studio でオブジェクトをデータ ソースとしてバインドする

Visual Studio では、カスタム オブジェクトをアプリケーションのデータ ソースとして操作するためのデザイン時ツールが提供されています。 UI コントロールにバインドしたオブジェクトにデータベースのデータを格納したい場合は、Entity Framework を使用して、クラス (1 つまたは複数) を生成する方法が推奨されます。 Entity Framework では、定型の変更追跡コードがすべて自動生成されます。これは、DbSet オブジェクトで AcceptChanges を呼び出したときに、ローカル オブジェクトに対する変更がデータベースに自動的に保存されることを意味します。 詳しくは、[Entity Framework のドキュメント](https://ef.readthedocs.org/en/latest/)をご覧ください。

> [!TIP]
> この記事にあるオブジェクト バインドの方法は、アプリケーションが既にデータセットに基づいている場合にのみ、その使用を検討してください。 これらの方法は、データセットを既に使い慣れていて、処理するデータが表形式であり、複雑すぎたり大きすぎたりしない場合にも使用できます。 DataReader を使ってオブジェクトにデータを直接読み込み、データバインドを使わずに UI を手動で更新するなど、さらに簡単な例については、「[ADO.NET を使用した単純なデータ アプリケーションの作成](../data-tools/create-a-simple-data-application-by-using-adonet.md)」を参照してください。

## <a name="object-requirements"></a>オブジェクトの要件

カスタム オブジェクトを Visual Studio のデータ デザイン ツールで操作するための唯一の要件は、オブジェクトに少なくとも 1 つのパブリック プロパティが必要であるということです。

一般に、カスタム オブジェクトでは、アプリケーションのデータ ソースとして機能する、特定のインターフェイス、コンストラクター、属性は必要ありません。 ただし、オブジェクトを **[データ ソース]** ウィンドウからデザイン サーフェイスにドラッグしてデータ バインド コントロールを作成する場合で、オブジェクトが <xref:System.ComponentModel.ITypedList> または <xref:System.ComponentModel.IListSource> インターフェイスを実装している場合は、オブジェクトに既定のコンストラクターが必要です。 これがない場合、Visual Studio はデータ ソース オブジェクトをインスタンス化できないので、デザイン サーフェイスに項目をドラッグするとエラーが表示されます。

## <a name="examples-of-using-custom-objects-as-data-sources"></a>カスタム オブジェクトをデータ ソースとして使用する例

オブジェクトをデータ ソースとして使用する場合、アプリケーション ロジックを実装する方法は数多くありますが、SQL データベースに関しては、Visual Studio で生成された TableAdapter オブジェクトを使用することで簡略化できる、いくつかの標準操作があります。 このページでは、TableAdapter を使ってこれらの標準プロセスを実装する方法について説明します。 カスタム オブジェクトを作成するためのガイドではありません。 たとえば、通常は、オブジェクトの特定の実装やアプリケーションのロジックに関係なく、次のような標準の操作を実行します。

- オブジェクトにデータを読み込む (通常はデータベースから)。

- オブジェクトの型指定されたコレクションを作成する。

- コレクション内のオブジェクトの追加や削除を行う。

- フォーム上でオブジェクト データをユーザー向けに表示する。

- オブジェクト内のデータを変更/編集する。

- オブジェクトのデータを取得元のデータベースに保存する。

### <a name="load-data-into-objects"></a>オブジェクトにデータを読み込む

この例では、TableAdapter を使ってオブジェクトにデータを読み込みます。 既定では、TableAdapter は、データベースからデータをフェッチしてデータ テーブルに設定する、2 種類のメソッドを使って作成されます。

- `TableAdapter.Fill` メソッドは、返されたデータを既存のデータ テーブルに格納します。

- `TableAdapter.GetData` メソッドは、データが設定された新しいデータ テーブルを返します。

カスタム オブジェクトにデータを読み込む最も簡単な方法は、`TableAdapter.GetData` メソッドを呼び出し、返されたデータ テーブル内の行のコレクションをループ処理して、各オブジェクトに各行の値を設定するという方法です。 データが設定されたデータ テーブルを返す `GetData` メソッドは、TableAdapter に追加された任意のクエリに対して作成できます。

> [!NOTE]
> Visual Studio では、TableAdapter クエリに既定で `Fill` および `GetData` という名前が指定されますが、これらの名前は任意の有効なメソッド名に変更することもできます。

次の例は、データ テーブル内の行をループ処理し、オブジェクトにデータを設定する方法を示したものです。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Form1.vb" id="Snippet4":::

### <a name="create-a-typed-collection-of-objects"></a>オブジェクトの型指定されたコレクションを作成する

オブジェクトのコレクション クラスを作成することも、[BindingSource コンポーネント](/dotnet/framework/winforms/controls/bindingsource-component)によって自動的に提供される、型指定されたコレクションを使用することもできます。

オブジェクトのカスタム コレクション クラスを作成する場合は、<xref:System.ComponentModel.BindingList%601> から継承することをお勧めします。 このジェネリック クラスでは、コレクションを管理するための機能だけでなく、Windows フォームのデータ バインディング インフラストラクチャに通知を送るイベントを発生させる機能も提供されます。

<xref:System.Windows.Forms.BindingSource> で自動的に生成されたコレクションでは、型指定されたコレクション用に <xref:System.ComponentModel.BindingList%601> が使用されます。 アプリケーションで追加の機能が必要ない場合は、コレクションを <xref:System.Windows.Forms.BindingSource> 内で保持することができます。 詳しくは、<xref:System.Windows.Forms.BindingSource> クラスの <xref:System.Windows.Forms.BindingSource.List%2A> プロパティを参照してください。

> [!NOTE]
> <xref:System.ComponentModel.BindingList%601> の基本実装によって提供されない機能がコレクションに必要な場合は、カスタム コレクションを作成して、必要に応じてクラスに追加できるようにする必要があります。

次のコードは、`Order` オブジェクトの厳密に型指定されたコレクション用のクラスを作成する方法を示したものです。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet8":::

### <a name="add-objects-to-a-collection"></a>コレクションにオブジェクトを追加する

コレクションにオブジェクトを追加するには、カスタム コレクション クラスまたは <xref:System.Windows.Forms.BindingSource> の `Add` メソッドを呼び出します。

> [!NOTE]
> <xref:System.ComponentModel.BindingList%601> から継承した場合、`Add` メソッドは、カスタム コレクションに対して自動的に提供されます。

次のコードは、<xref:System.Windows.Forms.BindingSource> 内の型指定されたコレクションにオブジェクトを追加する方法を示したものです。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet5":::

次のコードは、<xref:System.ComponentModel.BindingList%601> から継承した型指定されたコレクションにオブジェクトを追加する方法を示したものです。

> [!NOTE]
> この例では、`Orders` コレクションは `Customer` オブジェクトのプロパティです。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet6":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet6":::

### <a name="remove-objects-from-a-collection"></a>コレクションからオブジェクトを削除する

コレクションからオブジェクトを削除するには、カスタム コレクション クラスまたは <xref:System.Windows.Forms.BindingSource> の、`Remove` または `RemoveAt` メソッドを呼び出します。

> [!NOTE]
> <xref:System.ComponentModel.BindingList%601> から継承した場合、`Remove` および `RemoveAt` メソッドは、カスタム コレクションに対して自動的に提供されます。

次のコードは、<xref:System.Windows.Forms.BindingSource.RemoveAt%2A> メソッドを使って、<xref:System.Windows.Forms.BindingSource> 内の型指定されたコレクションからオブジェクトを検索し、削除する方法を示したものです。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet7":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet7":::

### <a name="display-object-data-to-users"></a>オブジェクトのデータをユーザーに表示する

オブジェクトのデータをユーザーに表示するには、**データ ソース構成** ウィザードを使ってオブジェクト データ ソースを作成した後、オブジェクト全体または個々のプロパティを、 **[データ ソース]** ウィンドウからフォーム上にドラッグします。

### <a name="modify-the-data-in-objects"></a>オブジェクト内のデータを変更する

Windows フォーム コントロールにデータ バインドされているカスタム オブジェクト内のデータを編集するには、バインドされたコントロール内のデータを編集します (またはオブジェクトのプロパティ内で直接編集します)。 オブジェクト内のデータは、データ バインディング アーキテクチャによって更新されます。

アプリケーションで変更を追跡する必要がある場合で、提案された変更を元の値にロールバックする必要がある場合は、オブジェクト モデルにその機能を実装する必要があります。 データ テーブルで提案された変更がどのように追跡されるかの例については、<xref:System.Data.DataRowState>、<xref:System.Data.DataSet.HasChanges%2A>、および <xref:System.Data.DataTable.GetChanges%2A> に関する記事を参照してください。

### <a name="save-data-in-objects-back-to-the-database"></a>オブジェクト内のデータを取得元のデータベースに保存する

データを取得元のデータベースに保存するには、オブジェクトから、TableAdapter の DBDirect メソッドに値を渡します。

データベースに対して直接実行できる DBDirect メソッドが、Visual Studio によって作成されます。 これらのメソッドでは、DataSet オブジェクトや DataTable オブジェクトは必要ありません。

|TableAdapter DBDirect メソッド|説明|
| - |-----------------|
|`TableAdapter.Insert`|データベースに新しいレコードを追加します。これにより、個々の列の値をメソッド パラメーターとして渡せるようになります。|
|`TableAdapter.Update`|データベースの既存のレコードを更新します。 Update メソッドは、元の列と新しい列の値をメソッドのパラメーターとして受け取ります。 元の値は元のレコードを検索するために使用され、新しい値はそのレコードを更新するために使用されます。<br /><br /> `TableAdapter.Update` メソッドは、<xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow>、または <xref:System.Data.DataRow> の配列をメソッド パラメーターとして受け取り、データベースに戻されるデータセット内の変更を調整するためにも使用されます。|
|`TableAdapter.Delete`|メソッド パラメーターとして渡された元の列の値に基づいて、データベースから既存のレコードを削除します。|

オブジェクトのコレクションのデータを保存するには、オブジェクトのコレクションをループ処理します (たとえば、for-next ループを使用するなど)。 各オブジェクトの値をデータベースに送信するには、TableAdapter の DBDirect メソッドを使用します。

次の例は、`TableAdapter.Insert` DBDirect メソッドを使って、新規の顧客をデータベースに直接追加する方法を示したものです。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet23":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet23":::

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
