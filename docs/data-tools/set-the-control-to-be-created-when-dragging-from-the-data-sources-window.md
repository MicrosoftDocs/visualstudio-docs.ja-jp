---
title: ドラッグしたときに作成するコントロールを設定する
description: Visual Studio で、[データ ソース] ウィンドウから WPF デザイナーまたは Windows フォーム デザイナーにドラッグしたときに作成されるコントロールを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Data Sources Window, select controls
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- data [Visual Studio], Data Sources window
ms.assetid: 20597ff8-0c98-43ec-8fb1-05376804ba48
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 6b4d1782a82a1eb2147d540b1799f5152c4f2308
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858437"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する

**[データ ソース]** ウィンドウから WPF デザイナーまたは Windows フォーム デザイナーに項目をドラッグすることにより、データ バインド コントロールを作成できます。 **[データ ソース]** ウィンドウの各項目には、その項目をデザイナーにドラッグしたときに作成される既定のコントロールが関連付けられています。 ただし、別のコントロールが作成されるようにすることもできます。

## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>データ テーブルまたはオブジェクトに対して作成されるコントロールを設定する

データ テーブルまたはオブジェクトを表す項目を **[データ ソース]** ウィンドウからドラッグする前に、すべてのデータを 1 つのコントロールに表示するか、それぞれの列またはプロパティを個別のコントロールに表示するかを選択できます。

ここで、*オブジェクト* という用語は、カスタム ビジネス オブジェクト、エンティティ (Entity Data Model のエンティティ)、またはサービスによって返されるオブジェクトを意味します。

### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>データ テーブルまたはオブジェクトに対して作成されるコントロールを設定するには

1. **WPF** デザイナーまたは **Windows フォーム** デザイナーが開いていることを確認します。

2. **[データ ソース]** ウィンドウで、設定するデータ テーブルまたはオブジェクトを表す項目を選択します。

   > [!TIP]
   > **[データ ソース]** ウィンドウが開いていない場合は、 **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** の順に選択することで開くことができます。

3. 項目のドロップダウン メニューをクリックし、メニューの次の項目のいずれかをクリックします。

    - 各データ フィールドを個別のコントロールに表示するには、**[詳細]** をクリックします。 データ項目をデザイナーにドラッグすると、このアクションにより、親のデータ テーブルまたはオブジェクトの列またはプロパティごとに異なるデータ バインド コントロールが作成され、各コントロールのラベルが作成されます。

    - すべてのデータを単一のコントロールに表示するには、リストで別のコントロールを選択します。たとえば、WPF アプリケーションでは **[DataGrid]** または **[List]** を選択し、Windows フォーム アプリケーションでは **[DataGridView]** を選択します。

    使用可能なコントロールの一覧は、開いているデザイナー、プロジェクトがターゲットとしている .NET のバージョン、データ バインディングをサポートするカスタム コントロールが **[ツールボックス]** に追加されているかどうかによって異なります。 作成するコントロールが使用可能なコントロールの一覧にない場合は、そのコントロールを一覧に追加できます。 詳細については、「[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

    **[データ ソース]** ウィンドウのデータ テーブルまたはオブジェクトのコントロールの一覧に追加できるカスタム Windows フォーム コントロールを作成する方法については、「[複雑なデータ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)」を参照してください。

## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>データ列またはプロパティに対して作成されるコントロールを設定する

オブジェクトの列またはプロパティを表す項目を **[データ ソース]** ウィンドウからデザイナーにドラッグする前に、作成されるコントロールを設定できます。

### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>列またはプロパティに対して作成されるコントロールを設定するには

1. **WPF** デザイナーまたは **Windows フォーム** デザイナーが開いていることを確認します。

2. **[データ ソース]** ウィンドウで、目的のテーブルまたはオブジェクトを展開して、その列またはプロパティを表示します。

3. 作成されるコントロールを設定する各列または各プロパティを選択します。

4. 列またはプロパティのドロップダウン メニューをクリックし、項目をデザイナーにドラッグしたときに作成されるコントロールを選択します。

     使用可能なコントロールの一覧は、開いているデザイナー、プロジェクトがターゲットとしている .NET のバージョン、 **[ツールボックス]** に追加されている、データ バインディングをサポートするカスタム コントロールによって異なります。 作成するコントロールが利用できるコントロールのリストに含まれている場合、コントロールをリストに追加できます。 詳細については、「[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

     **[データ ソース]** ウィンドウのデータ列またはプロパティのコントロールの一覧に追加できるカスタム コントロールを作成する方法については、「[単純なデータ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)」を参照してください。

     列またはプロパティのコントロールを作成しない場合は、ドロップダウン メニューの **[なし]** を選択します。 これは、親のテーブルまたはオブジェクトをデザイナーにドラッグする必要があり、かつ特定の列またはプロパティを含める必要がない場合に便利です。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
