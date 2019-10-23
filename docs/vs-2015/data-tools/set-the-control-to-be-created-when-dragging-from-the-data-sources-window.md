---
title: '[データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定します。Microsoft Docs'
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
- Data Sources Window, select controls
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- data [Visual Studio], Data Sources window
ms.assetid: 20597ff8-0c98-43ec-8fb1-05376804ba48
caps.latest.revision: 34
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 222ecfa56b179379c2d007e8635e7b40d6b1b660
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655384"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[データ ソース]** ウィンドウから WPF デザイナーまたは Windows フォーム デザイナーに項目をドラッグすることにより、データ バインド コントロールを作成できます。 **[データ ソース]** ウィンドウの各項目には、その項目をデザイナーにドラッグしたときに作成される既定のコントロールが関連付けられています。 ただし、別のコントロールが作成されるようにすることもできます。

## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>データ テーブルまたはオブジェクトに対して作成されるコントロールを設定する
 データ テーブルまたはオブジェクトを表す項目を **[データ ソース]** ウィンドウからドラッグする前に、すべてのデータを 1 つのコントロールに表示するか、それぞれの列またはプロパティを個別のコントロールに表示するかを選択できます。

 ここで、*オブジェクト*という用語は、カスタム ビジネス オブジェクト、エンティティ (Entity Data Model のエンティティ)、またはサービスによって返されるオブジェクトを意味します。

#### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>データ テーブルまたはオブジェクトに対して作成されるコントロールを設定するには

1. WPF デザイナーまたは Windows フォーム デザイナーが開いていることを確認します。

2. **[データ ソース]** ウィンドウで、設定するデータ テーブルまたはオブジェクトを表す項目を選択します。

3. 項目のドロップダウン メニューをクリックし、メニューの次の項目のいずれかをクリックします。

   - 各データ フィールドを個別のコントロールに表示するには、 **[詳細]** をクリックします。 データ項目をデザイナーにドラッグすると、このアクションにより、親のデータ テーブルまたはオブジェクトの列またはプロパティごとに異なるデータ バインド コントロールが作成され、各コントロールのラベルが作成されます。

   - すべてのデータを単一のコントロールに表示するには、リストで別のコントロールを選択します。たとえば、WPF アプリケーションでは **[DataGrid]** または **[List]** を選択し、Windows フォーム アプリケーションでは **[DataGridView]** を選択します。

     利用できるコントロールのリストは、開いたデザイナー、プロジェクトのターゲットである .NET Framework のバージョン、およびデータ バインディングをサポートするカスタム コントロールを**ツールボックス**に追加したかどうかによって異なります。 作成するコントロールが利用できるコントロールのリストに含まれている場合、コントロールをリストに追加できます。 詳細については、「 [[データソース] ウィンドウにカスタムコントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

     **[データソース]** ウィンドウでデータテーブルまたはオブジェクトのコントロールの一覧に追加できるカスタム Windows フォームコントロールを作成する方法については、「[複合データバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)する」を参照してください。

## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>データ列またはプロパティに対して作成されるコントロールを設定する
 オブジェクトの列またはプロパティを表す項目を **[データ ソース]** ウィンドウからデザイナーにドラッグする前に、作成されるコントロールを設定できます。

#### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>列またはプロパティに対して作成されるコントロールを設定するには

1. WPF デザイナーまたは Windows フォーム デザイナーが開いていることを確認します。

2. **[データ ソース]** ウィンドウで、目的のテーブルまたはオブジェクトを展開して、その列またはプロパティを表示します。

3. 作成されるコントロールを設定する各列または各プロパティを選択します。

4. 列またはプロパティのドロップダウン メニューをクリックし、項目をデザイナーにドラッグしたときに作成されるコントロールを選択します。

     利用できるコントロールのリストは、開いたデザイナー、プロジェクトのターゲットである .NET Framework のバージョン、および**ツールボックス**に追加したデータ バインディングをサポートするカスタム コントロールによって異なります。 作成するコントロールが利用できるコントロールのリストに含まれている場合、コントロールをリストに追加できます。 詳細については、「 [[データソース] ウィンドウにカスタムコントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

     **[データソース]** ウィンドウのデータ列またはプロパティのコントロールの一覧に追加できるカスタムコントロールを作成する方法については、「[単純なデータバインディングをサポートする Windows フォームユーザーコントロールを作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)する」を参照してください。

     列またはプロパティのコントロールを作成しない場合は、ドロップダウンメニューで **[なし]** を選択します。 これは、親のテーブルまたはオブジェクトをデザイナーにドラッグする必要があり、かつ特定の列またはプロパティを含める必要がない場合に便利です。

## <a name="see-also"></a>参照
 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
