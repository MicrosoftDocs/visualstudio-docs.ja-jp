---
title: WPF アプリケーションでルックアップ テーブルを作成する
description: WPF アプリでルックアップ テーブルを作成します。 ルックアップ テーブルとは、別のテーブルの外部キー フィールドの値に基づいて、データ テーブルからの情報を表示するコントロールです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 56a1fbff-c7e8-4187-a1c1-ffd17024bc1b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: cc390642155d33f75bf5c4a69236945658845639
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867101"
---
# <a name="create-lookup-tables-in-wpf-applications"></a>WPF アプリケーションでルックアップ テーブルを作成する

"*ルックアップ テーブル*" ("*参照バインディング*" と呼ばれることもあります) という用語は、別のテーブルの外部キー フィールドの値に基づいて、データ テーブルからの情報を表示するコントロールを表します。 ルックアップ テーブルを作成するには、 **[データ ソース]** ウィンドウの親テーブルまたはオブジェクトのメイン ノードを、関連する子テーブルの列またはプロパティに既にバインドされているコントロールにドラッグします。

たとえば、販売データベースの `Orders` テーブルであれば、次のように使用されます。 `Orders` テーブルの各レコードには、注文した顧客を示す `CustomerID` が含まれています。 `CustomerID` は、`Customers` テーブルの顧客レコードを指す外部キーです。 `Orders` テーブルから注文の一覧を表示するときに、`CustomerID` ではなく、実際の顧客名を表示したい場合があります。 顧客名は `Customers` テーブルに含まれているので、顧客名を表示するにはルックアップ テーブルを作成する必要があります。 ルックアップ テーブルでは、`Orders` レコードの `CustomerID` 値を使用してリレーションシップをナビゲートし、顧客名を返します。

## <a name="to-create-a-lookup-table"></a>ルックアップ テーブルを作成するには

1. 関連データを含む次のいずれかの種類のデータ ソースをプロジェクトに追加します。

    - データセットまたは Entity Data Model。

    - WCF Data Service、WCF サービス、または Web サービス。 詳細については、「[方法: サービスのデータに接続する](../data-tools/how-to-connect-to-data-in-a-service.md)」を参照してください。

    - オブジェクト。 詳細については、[Visual Studio でのオブジェクトへのバインド](bind-objects-in-visual-studio.md)に関する記事を参照してください。

    > [!NOTE]
    > ルックアップ テーブルを作成するには、関連する 2 つのテーブルまたはオブジェクトがプロジェクトのデータ ソースとして存在している必要があります。

2. **WPF デザイナー** を開き、 **[データ ソース]** ウィンドウ内の項目の有効なドロップ ターゲットであるコンテナーがデザイナーに含まれていることを確認します。

     有効なドロップ ターゲットの詳細については、「[Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

3. **[データ]** メニューの **[データ ソースの表示]** をクリックして **[データ ソース]** ウィンドウを開きます。

4. **[データ ソース]** ウィンドウで、親テーブルまたはオブジェクトと関連する子テーブルまたはオブジェクトが表示されるまでノードを展開します。

    > [!NOTE]
    > 関連する子テーブルまたはオブジェクトは、親テーブルまたはオブジェクトの下に展開可能な子ノードとして表示されるノードです。

5. 子ノードのドロップダウン メニューをクリックし、 **[詳細]** を選択します。

6. 子ノードを展開します。

7. 子ノードの下で、子と親のデータを関連付ける項目のドロップダウン メニューをクリックします (前の例では、これは **CustomerID** ノードです)。参照バインディングをサポートする次のいずれかの種類のコントロールを選択します。

    - **ComboBox**

    - **ListBox**

    - **ListView**

        > [!NOTE]
        > **ListBox** または **ListView** コントロールが一覧に表示されていない場合は、これらのコントロールを一覧に追加できます。 詳細については、「[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

    - <xref:System.Windows.Controls.Primitives.Selector> から派生したカスタム コントロール。

        > [!NOTE]
        > **[データ ソース]** ウィンドウの項目に対して選択できるコントロールの一覧にカスタム コントロールを追加する方法については、「[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

8. **[データ ソース]** ウィンドウから WPF デザイナーのコンテナーに子ノードをドラッグします (前の例では、子ノードは **Orders** ノードです)。

     Visual Studio により、ドラッグした項目ごとに新しいデータバインド コントロールを作成する XAML が生成されます。 この XAML では、子テーブルまたはオブジェクトの新しい <xref:System.Windows.Data.CollectionViewSource> もドロップ ターゲットのリソースに追加します。 一部のデータ ソースでは、Visual Studio によって、テーブルまたはオブジェクトにデータを読み込むコードも生成されます。 詳細については、「[Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

9. **[データ ソース]** ウィンドウから、前に作成した参照バインディング コントロールに親ノードをドラッグします (前の例では、親ノードは **Customers** ノードです)。

     Visual Studio では、参照バインディングを構成するために、コントロールにいくつかのプロパティが設定されます。 次の表に、Visual Studio によって変更されるプロパティを示します。 必要に応じて、XAML または **[プロパティ]** ウィンドウでこれらのプロパティを変更できます。

    |プロパティ|設定の説明|
    |--------------| - |
    |<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>|このプロパティでは、コントロールに表示されるデータを取得するために使用されるコレクションまたはバインディングを指定します。 Visual Studio により、このプロパティは、コントロールにドラッグした親データの <xref:System.Windows.Data.CollectionViewSource> に設定されます。|
    |<xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A>|このプロパティでは、コントロールに表示されるデータ項目のパスを指定します。 Visual Studio により、このプロパティは、親データの主キーの後にある、文字列データ型を含む最初の列またはプロパティに設定されます。<br /><br /> 親データの別の列またはプロパティを表示する場合は、このプロパティを別のプロパティのパスに変更します。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A>|Visual Studio により、このプロパティは、デザイナーにドラッグした子データの列またはプロパティにバインドされます。 これは親データへの外部キーです。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValuePath%2A>|Visual Studio により、このプロパティは、親データへの外部キーである子データの列またはプロパティのパスに設定されます。|

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [WPF アプリケーションで関連データを表示する](../data-tools/display-related-data-in-wpf-applications.md)
- [チュートリアル: WPF アプリケーションでの関連データの表示](../data-tools/display-related-data-in-wpf-applications.md)
