---
title: '方法: ListObject コントロールのサイズを変更する'
description: Visual Studio を使用して、Microsoft Excel ブック内の ListObject コントロールのサイズをプログラムによって変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- ListObject control, resizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a2fd0b8ce46ba15066ab4cf070807e2457c21e70
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828957"
---
# <a name="how-to-resize-listobject-controls"></a>方法: ListObject コントロールのサイズを変更する
  <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールのサイズは Microsoft Office Excel ブックにコントロールを追加するときに設定しますが、後でサイズを変更することもできます。 たとえば、2 列のリストを 3 列のリストに変更できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 ドキュメント レベルのプロジェクトでは、デザイン時または実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールのサイズを変更できます。 VSTO アドイン プロジェクトでは、実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールのサイズを変更できます。

 このトピックでは、次のタスクについて説明します。

- [デザイン時に ListObject コントロールのサイズを変更する](#designtime)

- [文書レベルのプロジェクトで、実行時に ListObject コントロールのサイズを変更する](#runtimedoclevel)

- [VSTO アドイン プロジェクトで、実行時に ListObject コントロールのサイズを変更する](#runtimeaddin)

  <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールの詳細については、「[ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

## <a name="resize-a-listobject-control-at-design-time"></a><a name="designtime"></a> デザイン時に ListObject コントロールのサイズを変更する
 リストのサイズを変更するには、サイズ変更ハンドルのいずれかをクリックしてドラッグでき、また **[リストのサイズ変更]** ダイアログ ボックスでそのサイズを再定義することもできます。

### <a name="to-resize-a-list-by-using-the-resize-list-dialog-box"></a>[リストのサイズ変更] ダイアログ ボックスを使用してリストのサイズを変更するには

1. <xref:Microsoft.Office.Tools.Excel.ListObject> テーブル内の任意の場所をクリックします。 リボンの **[テーブル ツール]**  >  **[デザイン]** タブが表示されます。

2. [プロパティ] セクションで、 **[テーブルのサイズ変更]** をクリックします。

    ![VSTO_ResizeTable](../vsto/media/vsto-resizetable.png)

3. テーブルの新しいデータ範囲を選択します。

4. **[OK]** をクリックします。

## <a name="resize-a-listobject-control-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 実行時に文書レベルのプロジェクトで ListObject コントロールのサイズを変更する
 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールのサイズは、実行時に <xref:Microsoft.Office.Tools.Excel.ListObject.Resize%2A> メソッドを使用して変更できます。 このメソッドは、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをワークシート上の新しい位置に移動するためには使用できません。 ヘッダーは同じ行のままである必要があり、サイズを変更した <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールは元のリスト オブジェクトに重なる必要があります。 サイズ変更した <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールには、ヘッダー行および少なくとも 1 つのデータ行が含まれている必要があります。

### <a name="to-resize-a-list-object-programmatically"></a>リスト オブジェクトのサイズをプログラムで変更するには

1. <xref:Microsoft.Office.Tools.Excel.ListObject> に、セル **A1** から **B3** にまたがる `Sheet1`コントロールを作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet6":::

2. リストのサイズをセル **A1** から **C5** までに変更します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet7":::

## <a name="resize-a-listobject-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a> 実行時に VSTO アドイン プロジェクトで ListObject のサイズを変更する
 実行時に、任意の開いているワークシート上の <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールのサイズを変更できます。 VSTO アドインを使用して <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをワークシートに追加する方法の詳細については、「[方法: ワークシートに ListObject コントロールを追加する](../vsto/how-to-add-listobject-controls-to-worksheets.md)」をご覧ください。

### <a name="to-resize-a-list-object-programmatically"></a>リスト オブジェクトのサイズをプログラムで変更するには

1. <xref:Microsoft.Office.Tools.Excel.ListObject> に、セル **A1** から **B3** にまたがる `Sheet1`コントロールを作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet12":::

2. リストのサイズをセル **A1** から **C5** までに変更します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet13":::

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [実行時に Office 文書にコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ListObject コントロール](../vsto/listobject-control.md)
- [方法: ワークシートに ListObject コントロールを追加する](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [方法: Bookmark コントロールのサイズを変更する](../vsto/how-to-resize-bookmark-controls.md)
- [方法: NamedRange コントロールのサイズを変更する](../vsto/how-to-resize-namedrange-controls.md)
