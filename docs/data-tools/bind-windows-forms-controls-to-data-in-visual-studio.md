---
title: Windows フォーム コントロールをデータにバインドする
description: アプリケーションのユーザーにデータを表示できるように、Visual Studio で Windows フォーム コントロールをデータにバインドします。
ms.custom: SEO-VS-2020
ms.date: 11/03/2017
ms.topic: how-to
helpviewer_keywords:
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 3da0c4e9835c9b6f6498aa28b82f2e631d1717ba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867413"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>Visual Studio でのデータへの Windows フォーム コントロールのバインド

データを Windows フォームにバインドすることで、アプリケーションのユーザーに対してデータを表示できます。 これらのデータバインド コントロールを作成するには、Visual Studio で **[データ ソース]** ウィンドウから Windows フォーム デザイナーに項目をドラッグします。

![データ ソースのドラッグ操作](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> **[データ ソース]** ウィンドウが表示されていない場合は、 **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** の順に選択するか、**Shift** + **Alt** + **D** キーを押して開くことができます。 **[データ ソース]** ウィンドウを表示するには、Visual Studio でプロジェクトを開いておく必要があります。

項目をドラッグする前に、バインド先のコントロールの種類を設定できます。 テーブル自体を選択するか、個々の列を選択するかによって、表示される値が異なります。  また、カスタム値を設定することもできます。 テーブルの場合、 **[詳細]** を使用すると、各列が個別のコントロールにバインドされます。

![DataGridView にデータ ソースをバインドする](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>BindingSource および BindingNavigator コントロール

<xref:System.Windows.Forms.BindingSource> コンポーネントは 2 つの目的で利用できます。 まず、コントロールをデータにバインドするときに、抽象化レイヤーの役割を果たします。 フォーム上のコントロールは、データ ソースに直接バインドされるのではなく、<xref:System.Windows.Forms.BindingSource> コンポーネントにバインドされます。 また、オブジェクトのコレクションを管理できます。 <xref:System.Windows.Forms.BindingSource> に型を追加すると、その型の一覧が作成されます。

<xref:System.Windows.Forms.BindingSource> コンポーネントの詳細については、次のトピックを参照してください。

- [BindingSource コンポーネント](/dotnet/framework/winforms/controls/bindingsource-component)

- [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [BindingSource コンポーネント アーキテクチャ](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

[BindingNavigator コントロール](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)は、Windows アプリケーションによって表示されるデータ間を移動するためのユーザー インターフェイスを提供します。

## <a name="bind-to-data-in-a-datagridview-control"></a>DataGridView コントロールのデータへのバインド

[DataGridView コントロール](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms)の場合、テーブル全体がその 1 つのコントロールにバインドされます。 **DataGridView** をフォームにドラッグすると、レコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) も表示されます。 [DataSet](../data-tools/dataset-tools-in-visual-studio.md)、[TableAdapter](../data-tools/create-and-configure-tableadapters.md)、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。 次の図では、Customers テーブルが Orders テーブルに関連付けられているため、[TableAdapterManager](/previous-versions/bb384426(v=vs.140)) も追加されています。 これらの変数はすべて、自動生成コードでフォーム クラスのプライベート メンバーとして宣言されています。 **DataGridView** に入力するための自動生成コードは、`Form_Load` イベント ハンドラーにあります。 データを保存してデータベースを更新するためのコードは、**BindingNavigator** の `Save` イベント ハンドラーにあります。 必要に応じて、このコードを移動または変更できます。

![GridView と BindingNavigator](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

**DataGridView** と **BindingNavigator** の動作は、それぞれの右上隅にあるスマート タグをクリックしてカスタマイズできます。

![DataGridView と BindingNavigator のスマート タグ](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

自分のアプリケーションに必要なコントロールが **[データ ソース]** ウィンドウ内から使用できない場合は、コントロールを追加できます。 詳細については、「[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

**[データ ソース]** ウィンドウからフォーム上の既存のコントロールに項目をドラッグして、コントロールをデータにバインドすることもできます。 データに既にバインドされているコントロールのデータ バインディングは、最後にドラッグされた項目に再設定されます。 有効なドロップ ターゲットであるためには、 **[データ ソース]** ウィンドウからドラッグされた項目の基になるデータ型をコントロールが表示できる必要があります。 たとえば、データ型が <xref:System.DateTime> である項目を <xref:System.Windows.Forms.CheckBox> にドラッグするのは無効です。<xref:System.Windows.Forms.CheckBox> は日付を表示できないためです。

## <a name="bind-to-data-in-individual-controls"></a>個々のコントロールのデータへのバインド

データ ソースを **[詳細]** にバインドすると、データセットの各列が個別のコントロールにバインドされます。

![データ ソースを詳細にバインドする](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> 前の図では、Orders テーブルからではなく、Customers テーブルの Orders プロパティからドラッグしていることに注意してください。 `Customer.Orders` プロパティにバインドすることで、**DataGridView** でのナビゲーション コマンドが詳細コントロールにすぐに反映されます。 Orders テーブルからドラッグした場合でも、コントロールはデータセットにバインドされますが、**DataGridView** と同期されません。

次の図は、Customers テーブルの Orders プロパティが **[データ ソース]** ウィンドウの **[詳細]** にバインドされた後にフォームに追加される既定のデータバインド コントロールを示しています。

![詳細情報にバインドされた Orders テーブル](../data-tools/media/raddata-orders-table-bound-to-details.png)

各コントロールにスマート タグがあることにも注意してください。 このタグを使用すると、そのコントロールにのみ適用されるカスタマイズが可能になります。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Windows フォームでのデータ バインディング (.NET Framework)](/dotnet/framework/winforms/windows-forms-data-binding)