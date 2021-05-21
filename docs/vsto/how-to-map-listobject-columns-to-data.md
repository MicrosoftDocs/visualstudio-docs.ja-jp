---
title: '方法 : データに ListObject 列をマップする'
description: SetDataBinding メソッドを呼び出すときに、ListObject に表示する列をマップする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], mapping to ListObject column
- ListObject control, mapping data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 68cb12503d0f8ad59de92f965c0ed51fbc0d7f40
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827462"
---
# <a name="how-to-map-listobject-columns-to-data"></a>方法 : データに ListObject 列をマップする
  <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを <xref:System.Data.DataTable>にバインドするとき、リストの中のすべての列を表示しなくてもよい場合や、データにバインドされていない特定の列が含まれている場合があります。 <xref:Microsoft.Office.Tools.Excel.ListObject> メソッドを呼び出すと、 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> に表示する列をマップできます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="map-columns"></a>列のマップ

### <a name="to-map-a-data-table-to-columns-in-a-list"></a>データ テーブルをリスト内の列にマップするには

1. クラス レベルで <xref:System.Data.DataTable> を作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet16":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet16":::

2. `Startup` クラス (ドキュメント レベル プロジェクトの場合) または `Sheet1` クラス (VSTO アドイン プロジェクトの場合) の `ThisAddIn` イベント ハンドラーにサンプルの列とデータを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet17":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet17":::

3. <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> メソッドを呼び出し、列名を表示順に渡します。 リストのオブジェクトは新たに作成された <xref:System.Data.DataTable> にバインドされますが、リスト オブジェクト内の列の順序は、<xref:System.Data.DataTable> に表示される順序とは異なります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet18":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet18":::

## <a name="specify-unmapped-columns"></a>マップされていない列の指定
 列を <xref:System.Data.DataTable>にマップするときに空の文字列を渡して、特定の列をデータにバインドしないことも指定できます。 そのようにすると、データにバインドされない新しい列は <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールに追加されます。

### <a name="to-specify-an-unmapped-column-when-mapping-listobject-columns"></a>ListObject 列をマップするときにマップしない列を指定するには

1. <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> メソッドを呼び出し、列名を表示順に渡します。 空の文字列を使用して、マップしない列を追加する位置を示します。この場合は、タイトル列と姓の列の間です。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet19":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet19":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例では、このコードがあるワークシートに、 <xref:Microsoft.Office.Tools.Excel.ListObject> という名前の既存の `list1` があることを前提としています。

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [方法 : ListObject コントロールにデータを読み込む](../vsto/how-to-fill-listobject-controls-with-data.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ListObject コントロール](../vsto/listobject-control.md)
