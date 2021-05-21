---
title: '方法 : ListObject コントロールにデータを読み込む'
description: データ バインディングを使用して、ドキュメントにデータをすばやく追加します。 リスト オブジェクトを切断しても、データは表示できますが、データ ソースとのバインドは解除されます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnecting from data sources
- ListObject control, disconnecting from a data source
- ListObject control, filling with data
- data [Office development in Visual Studio], adding to worksheets
- data binding, ListObject controls
- worksheets, populating with data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 91fb4da23f388234e3800805e2beb3b7a8fbb20e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828918"
---
# <a name="how-to-fill-listobject-controls-with-data"></a>方法 : ListObject コントロールにデータを読み込む
  データ バインディングを使用すると、ドキュメントにデータをすばやく追加できます。 リスト オブジェクトにデータをバインドした後、リスト オブジェクトを切断すると、データは表示されますが、データ ソースとのバインドは解除されます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

### <a name="to-bind-data-to-a-listobject-control"></a>ListObject コントロールにデータをバインドするには

1. クラス レベルで <xref:System.Data.DataTable> を作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs" id="Snippet20":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb" id="Snippet20":::

2. `Startup` クラス (ドキュメント レベル プロジェクトの場合) または `Sheet1` クラス (アプリケーション レベル プロジェクトの場合) の `ThisAddIn` イベント ハンドラーにサンプルの列とデータを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs" id="Snippet21":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb" id="Snippet21":::

3. <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> メソッドを呼び出し、列名を表示順に渡します。 リスト オブジェクト内の列の順序は、 <xref:System.Data.DataTable>に表示される順序とは異なる場合があります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs" id="Snippet22":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb" id="Snippet22":::

### <a name="to-disconnect-the-listobject-control-from-the-data-source"></a>データ ソースから ListObject コントロールを切断するには

1. <xref:Microsoft.Office.Tools.Excel.ListObject.Disconnect%2A> の `List1`メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet4.cs" id="Snippet23":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet4.vb" id="Snippet23":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例では、このコードがあるワークシートに、 <xref:Microsoft.Office.Tools.Excel.ListObject> という名前の既存の `list1` があることを前提としています。

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [方法 : データに ListObject 列をマップする](../vsto/how-to-map-listobject-columns-to-data.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ListObject コントロール](../vsto/listobject-control.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [方法: データベースのデータをワークシートに読み込む](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)
