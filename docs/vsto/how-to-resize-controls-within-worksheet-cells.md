---
title: '方法: ワークシートのセル内のコントロールをサイズ変更する'
description: Visual Studio を使用して、デザイン時と実行時の両方で、Microsoft Excel ワークシートのセル内のコントロールのサイズを変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- managed controls, resizing
- worksheets, resizing
- Windows Forms controls [Office development in Visual Studio], resizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7b42c10fd82ec077b295a8bc683fa138c2eb095b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825746"
---
# <a name="how-to-resize-controls-within-worksheet-cells"></a>方法: ワークシートのセル内のコントロールをサイズ変更する
  ワークシート上の列または行のサイズを変更すると、セル内のホスト コントロールは、サイズ変更されたセルの高さまたは幅に自動的にサイズ変更されます。 Windows フォーム コントロールは、既定では自動的にサイズ変更されません。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 デザイン時にコントロールを追加する場合は、各コントロールの配置オプションを設定する必要があります。

 Windows フォーム コントロールをプログラムで追加し、範囲引数を指定する場合は、その範囲内にあるセルのサイズが変更されると、コントロールのサイズが自動的に変更されます。 詳細については、「[実行時に Office 文書にコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

## <a name="resize-controls-at-design-time"></a>デザイン時にコントロールのサイズを変更する

### <a name="to-make-controls-resize-with-cells-at-design-time"></a>デザイン時にコントロールのサイズをセルに合わせて変更するには

1. **[ツールボックス]** から、Windows フォーム コントロールをワークシートにドラッグします。

2. コントロールを右クリックし、 **[コントロールの書式設定]** をクリックします。

3. **[コントロールの書式設定]** ダイアログ ボックスで、 **[プロパティ]** タブをクリックします。

4. **[オブジェクトの位置関係]** の **[セルに合わせて移動やサイズ変更をする]** オプションを選択し、 **[OK]** をクリックします。

     コントロールを含むセルのサイズを変更すると、セルに合わせてコントロールのサイズが変更されます。

## <a name="resize-controls-at-run-time"></a>実行時にコントロールのサイズを変更する
 実行時に Windows フォーム コントロールを追加し、コントロールの場所として <xref:Microsoft.Office.Interop.Excel.Range> を渡す場合は、その範囲を含むワークシート セルのサイズが変更されると、コントロールのサイズが自動的に変更されます。

### <a name="to-make-controls-resize-with-cells-at-run-time"></a>実行時にコントロールのサイズをセルに合わせて変更するには

1. 範囲 A1 にコントロールを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet5":::

     コントロールを含むセルのサイズを変更すると、セルに合わせてコントロールのサイズが変更されます。

## <a name="reset-control-placement"></a>コントロールの配置をリセットする
 `Placement` プロパティを次のいずれかの <xref:Microsoft.Office.Interop.Excel.XlPlacement> 値に設定することによって、コントロールの配置とサイズ変更をリセットできます。

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMove>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMoveAndSize>

### <a name="to-change-the-behavior-of-a-control-so-that-it-does-not-resize-or-move-with-the-cell"></a>コントロールの動作を変更して、セルに合わせたサイズ変更や移動が行われないようにするには

1. コントロールの Placement プロパティを呼び出し、値を <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating> に設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet6":::

## <a name="see-also"></a>関連項目
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [方法: 印刷時にワークシートのコントロールを非表示にする](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Office ドキュメントでの Windows フォーム コントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
