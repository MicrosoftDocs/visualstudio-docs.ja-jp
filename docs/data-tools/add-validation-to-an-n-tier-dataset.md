---
title: n 層データセットに検証を追加する
description: Visual Studio で n 層データセットに検証を追加します。 個々の列または行全体に対する変更を検証します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, validating
- validation [Visual Basic], n-tier data applications
- validating n-tier data applications
ms.assetid: 34ce4db6-09bb-4b46-b435-b2514aac52d3
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 4911cc5ced991389d2c7b03a405c4fe9e28c5cc0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859360"
---
# <a name="add-validation-to-an-n-tier-dataset"></a>n 層データセットに検証を追加する
n 層ソリューションに分離されたデータセットへの検証の追加は、単一ファイルのデータセット (1 つのプロジェクト内のデータセット) に検証を追加するのと基本的には同じです。 データで検証を実行する位置として推奨されるのは、データ テーブルの <xref:System.Data.DataTable.ColumnChanging> イベントや <xref:System.Data.DataTable.RowChanging> イベントの発生時です。

データセットには、データセットのデータ テーブルの列および行変更イベントにユーザー コードを追加できる部分クラスを作成する機能があります。 n 層ソリューションのデータセットにコードを追加する方法の詳細については、「[n 層アプリケーションのデータセットにコードを追加する](../data-tools/add-code-to-datasets-in-n-tier-applications.md)」および「[n 層アプリケーションの TableAdapter にコードを追加する](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)」を参照してください。 部分クラスの詳細については、「[方法: クラス デザイナーで 1 つのクラスを複数の部分クラスに分割する](../ide/class-designer/how-to-split-a-class-into-partial-classes.md)」または「[部分クラスとメソッド](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)」を参照してください。

> [!NOTE]
> ( **[DataSet プロジェクト]** プロパティを設定して) TableAdapter からデータセットを分離するときに、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存のデータセット部分クラスは、データセット プロジェクトに手動で移動する必要があります。

> [!NOTE]
> C# では、<xref:System.Data.DataTable.ColumnChanging> イベントおよび <xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーはデータセット デザイナーにより自動作成されません。 イベント ハンドラーを手動で作成し、基になるイベントにイベント ハンドラーをフックする必要があります。 次の手順では、Visual Basic と C# の両方で必要なイベント ハンドラーを作成する方法について説明します。

## <a name="validate-changes-to-individual-columns"></a>個々の列の変更の検証
個々の列の値は、<xref:System.Data.DataTable.ColumnChanging> イベントを処理することにより検証します。 <xref:System.Data.DataTable.ColumnChanging> イベントは、列の値が変更されたときに発生します。 **データセット デザイナー** の目的の列をダブルクリックすることにより、<xref:System.Data.DataTable.ColumnChanging> イベントのイベント ハンドラーを作成します。

最初に列をダブルクリックすると、デザイナーにより <xref:System.Data.DataTable.ColumnChanging> イベントのイベント ハンドラーが生成されます。 特定の列をテストする `If...Then` ステートメントも作成されます。 たとえば、Northwind Orders テーブルの **RequiredDate** 列をダブルクリックすると次のコードが生成されます。

```vb
Private Sub OrdersDataTable_ColumnChanging(ByVal sender As System.Object, ByVal e As System.Data.DataColumnChangeEventArgs) Handles Me.ColumnChanging
    If (e.Column.ColumnName = Me.RequiredDateColumn.ColumnName) Then
        ' Add validation code here.
    End If
End Sub
```

> [!NOTE]
> C# プロジェクトでは、データセットの部分クラスとデータセットの個々のテーブルのみがデータセット デザイナーにより作成されます。 C# では、Visual Basic と同様に <xref:System.Data.DataTable.ColumnChanging> イベントおよび <xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーはデータセット デザイナーにより自動作成されません。 C# プロジェクトでは、イベントを処理するメソッドを手動で作成し、基になるイベントにメソッドをフックする必要があります。 次の手順では、必要なイベント ハンドラーを Visual Basic と C# の両方で作成する方法について説明します。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-add-validation-during-changes-to-individual-column-values"></a>個々の列値の変更時に検証を追加するには

1. **ソリューション エクスプローラー** で *.xsd* ファイルをダブルクリックしてデータセットを開きます。 詳細については、「[チュートリアル: データセット デザイナーを使用したデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. 検証する列をダブルクリックします。 この操作によって <xref:System.Data.DataTable.ColumnChanging> イベント ハンドラーが作成されます。

    > [!NOTE]
    > データセット デザイナーでは、C# イベントのイベント ハンドラーは自動作成されません。 C# でイベントを処理するために必要なコードは、次のセクションに含まれています。 `SampleColumnChangingEvent` を作成し、<xref:System.Data.DataTable.EndInit%2A> メソッドで <xref:System.Data.DataTable.ColumnChanging> イベントにフックします。

3. アプリケーションの要件を満たすデータが `e.ProposedValue` に含まれていることを検証するコードを追加します。 指定された値が受け入れられない場合、エラーがあることを表すように該当する列を設定します。

     次のコード例では、**Quantity** 列に 0 より大きい値が含まれていることを検証します。 **Quantity** が 0 以下の場合、列はエラーに設定されます。 **Quantity** が 0 より大きい場合、`Else` 句によりエラーが消去されます。 列変更イベント ハンドラー内のコードは、次のようになります。

    ```vb
    If (e.Column.ColumnName = Me.QuantityColumn.ColumnName) Then
        If CType(e.ProposedValue, Short) <= 0 Then
            e.Row.SetColumnError(e.Column, "Quantity must be greater than 0")
        Else
            e.Row.SetColumnError(e.Column, "")
        End If
    End If
    ```

    ```csharp
    // Add this code to the DataTable partial class.

    public override void EndInit()
    {
        base.EndInit();
        // Hook up the ColumnChanging event
        // to call the SampleColumnChangingEvent method.
        ColumnChanging += SampleColumnChangingEvent;
    }

    public void SampleColumnChangingEvent(object sender, System.Data.DataColumnChangeEventArgs e)
    {
        if (e.Column.ColumnName == QuantityColumn.ColumnName)
        {
            if ((short)e.ProposedValue <= 0)
            {
                e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
            }
            else
            {
                e.Row.SetColumnError("Quantity", "");
            }
        }
    }
    ```

## <a name="validate-changes-to-whole-rows"></a>行全体の変更の検証
行全体の値は、<xref:System.Data.DataTable.RowChanging> イベントを処理することにより検証します。 <xref:System.Data.DataTable.RowChanging> イベントは、すべての列の値がコミットされたときに発生します。 ある列の値が別の列の値に依存している場合は、<xref:System.Data.DataTable.RowChanging> イベントで検証を行う必要があります。 たとえば、Northwind の Orders テーブルの OrderDate と RequiredDate について考えます。

注文が入力されると、RequiredDate が OrderDate と同じか、それより前の日付の注文が入力されていないかを検証します。 この例では、RequiredDate 列と OrderDate 列の両方を比較する必要があるため、個々の列の変更を検証しても意味がありません。

**データセット デザイナー** で、テーブルのタイトル バーにあるテーブル名をダブルクリックして、<xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーを作成します。

#### <a name="to-add-validation-during-changes-to-whole-rows"></a>行全体の変更時に検証を追加するには

1. **ソリューション エクスプローラー** で *.xsd* ファイルをダブルクリックしてデータセットを開きます。 詳細については、「[チュートリアル: データセット デザイナーを使用したデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. デザイナーでデータ テーブルのタイトル バーをダブルクリックします。

     `RowChanging` イベント ハンドラーを使用して部分クラスが作成され、コード エディターが開きます。

    > [!NOTE]
    > C# プロジェクトでは、<xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーはデータセット デザイナーにより自動作成されません。 <xref:System.Data.DataTable.RowChanging> イベントを処理するメソッドを作成し、そのイベントをフックするコードをテーブルの初期化メソッドで実行する必要があります。

3. 部分クラスの宣言内にユーザー コードを追加します。

4. 次のコードに、<xref:System.Data.DataTable.RowChanging> イベント発生時に検証を行うユーザー コードを追加する場所を示します。 C# の例には、イベント ハンドラー メソッドを `OrdersRowChanging` イベントにフックするコードも含まれています。

    ```vb
    Partial Class OrdersDataTable
        Private Sub OrdersDataTable_OrdersRowChanging(ByVal sender As System.Object, ByVal e As OrdersRowChangeEvent) Handles Me.OrdersRowChanging
            ' Add logic to validate columns here.
            If e.Row.RequiredDate <= e.Row.OrderDate Then
                ' Set the RowError if validation fails.
                e.Row.RowError = "Required Date cannot be on or before the OrderDate"
            Else
                ' Clear the RowError when validation passes.
                e.Row.RowError = ""
            End If
        End Sub
    End Class
    ```

    ```csharp
    partial class OrdersDataTable
    {
        public override void EndInit()
        {
            base.EndInit();
            // Hook up the event to the
            // RowChangingEvent method.
            OrdersRowChanging += RowChangingEvent;
        }

        public void RowChangingEvent(object sender, OrdersRowChangeEvent e)
        {
            // Perform the validation logic.
            if (e.Row.RequiredDate <= e.Row.OrderDate)
            {
                // Set the row to an error when validation fails.
                e.Row.RowError = "Required Date cannot be on or before the OrderDate";
            }
            else
            {
                // Clear the RowError if validation passes.
                e.Row.RowError = "";
            }
        }
    }
    ```

## <a name="see-also"></a>関連項目

- [n 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [チュートリアル: n 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [データセットのデータの検証](../data-tools/validate-data-in-datasets.md)
