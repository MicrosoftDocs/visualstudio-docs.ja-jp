---
title: パラメーター付きの TableAdapter クエリを作成する
description: パラメーター付きの TableAdapter クエリを作成する方法について説明します。 パラメーター クエリは、クエリ内の WHERE 句の条件を満たすデータを返します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- TableAdapters, parameterized queries
- data [Visual Studio], searching data
- queries [Visual Studio], creating
- TableAdapters, searching data
- queries [Visual Studio], TableAdapters
ms.assetid: 104d1d19-b5a9-4071-b81e-1b3af08e9c7b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: d747459abc62462864e94ed9b8af9b11c6b9eabe
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215931"
---
# <a name="create-parameterized-tableadapter-queries"></a>パラメーター付きの TableAdapter クエリを作成する

パラメーター クエリは、クエリ内の WHERE 句の条件を満たすデータを返します。 たとえば、顧客リストをパラメーター化して、顧客のリストを戻す SQL ステートメントに `WHERE City = @City` を追加することで、特定の都市の顧客のみが表示されるようにできます。

パラメーター化された TableAdapter クエリは、**データセット デザイナー** で作成します。さらに、Windows アプリケーションで **[データ]** メニューの **[データ ソースのパラメーター化]** コマンドを使用して作成することもできます。 **[データ ソースのパラメーター化]** コマンドによって、パラメーター値を入力してクエリを実行できるコントロールがフォームに作成されます。

> [!NOTE]
> パラメーター化されたクエリを作成する場合は、コーディング対象のデータベースに固有のパラメーター表記を使用します。 たとえば、Access データ ソースと OleDb データ ソースは疑問符 "?" を使用してパラメーターを表すため、WHERE 句は `WHERE City = ?` のようになります。

## <a name="create-a-parameterized-tableadapter-query"></a>パラメーター化された TableAdapter クエリの作成

### <a name="to-create-a-parameterized-query-in-the-dataset-designer"></a>データセット デザイナーでパラメーター クエリを作成するには

- 新しい TableAdapter を作成し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。 詳細については、「[TableAdapter の作成および構成](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

     または

- 既存の TableAdapter にクエリを追加し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。

### <a name="to-create-a-parameterized-query-while-designing-a-data-bound-form"></a>データ バインド フォームの設計時にパラメーター クエリを作成するには

1. フォーム上の既にデータセットにバインドされているコントロールを選択します。 詳細については、[Visual Studio で Windows フォーム コントロールをデータにバインドする](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)方法に関するページを参照してください。

2. **[データ]** メニューの **[クエリの追加]** を選択します。

3. **[検索条件ビルダー]** ダイアログ ボックスの設定を完了し、目的のパラメーターを含む WHERE 句を SQL ステートメントに追加します。

### <a name="to-add-a-query-to-an-existing-data-bound-form"></a>既存のデータ バインド フォームにクエリを追加するには

1. **Windows フォーム デザイナー** でフォームを開きます。

2. **[データ]** メニューの **[クエリの追加]** または **[データ スマート タグ]** を選択します。

    > [!NOTE]
    > **[データ]** メニューの **[クエリの追加]** が使用できない場合は、パラメーターの追加先のデータ ソースを表示するフォーム上のコントロールを選択します。 たとえば、フォームに <xref:System.Windows.Forms.DataGridView> コントロールのデータが表示される場合は、そのコントロールを選択します。 フォームに個々のコントロールのデータが表示される場合は、いずれかのデータ バインド コントロールを選択します。

3. **[データ ソース テーブルを選択してください]** 領域で、パラメーター化を追加するテーブルを選択します。

4. 新しいクエリを作成する場合は、**[新しいクエリ名]** ボックスに名前を入力します。

     または

     **[既存のクエリ名]** ボックスでクエリを選択します。

5. **[クエリ テキスト]** ボックスに、パラメーターを受け取るクエリを入力します。

6. **[OK]** を選択します。

     パラメーターを入力するコントロールと **[読み込み]** ボタンが、<xref:System.Windows.Forms.ToolStrip> コントロールのフォームに追加されます。

### <a name="query-for-null-values"></a>Null 値のクエリ

現在の値がないレコードをクエリする場合は、TableAdapter パラメーターに null 値を割り当てることができます。 たとえば、`WHERE` 句に `ShippedDate` パラメーターがある次のクエリを考えてみます。

```sql
SELECT CustomerID, OrderDate, ShippedDate
FROM Orders
WHERE (ShippedDate = @ShippedDate) OR (ShippedDate IS NULL)
```

これが TableAdapter に対するクエリであった場合、次のコードによって、出荷されていないすべての注文をクエリできます。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Form2.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Form2.vb" id="Snippet8":::

クエリで null 値を受け入れるようにするには:

1. **データセット デザイナー** で、null パラメーター値を受け入れる必要がある TableAdapter クエリを選択します。

2. **[プロパティ]** ウィンドウで、 **[パラメーター]** を選択し、省略記号 ( **[...]** ) ボタンをクリックして、**パラメーター コレクション エディター** を開きます。

3. null 値を許容するパラメーターを選択し、**AllowDbNull** プロパティを `true` に設定します。

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
