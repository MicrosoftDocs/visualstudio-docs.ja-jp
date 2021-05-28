---
title: '方法: Office ドキュメントに Windows フォーム コントロールを追加する'
description: ドキュメント レベルのプロジェクトで、Microsoft Office Excel および Microsoft Office Word のドキュメントのデザイン時に Windows フォーム コントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], adding
- controls [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], Windows Forms controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e5a196c54a513376edef5c837a429bece6dd7b16
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824836"
---
# <a name="how-to-add-windows-forms-controls-to-office-documents"></a>方法: Office ドキュメントに Windows フォーム コントロールを追加する
  Windows フォーム コントロールは、デザイン時にドキュメント レベルのプロジェクトの Microsoft Office Excel および Microsoft Office Word のドキュメントに追加できます。 実行時には、ドキュメントレベルのカスタマイズと VSTO アドインにコントロールを追加できます。たとえば、ワークシートに <xref:Microsoft.Office.Tools.Excel.Controls.ComboBox> コントロールを追加して、ユーザーがオプションの一覧から選択できるようにすることもできます。

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

 このトピックでは、次のタスクについて説明します。

- [デザイン時にコントロールを追加する](#designtime)

- [ドキュメント レベルのプロジェクトで実行時にコントロールを追加する](#runtimedoclevel)

- [VSTO アドインで実行時にコントロールを追加する](#runtimeaddin)

## <a name="add-controls-at-design-time"></a><a name="designtime"></a> デザイン時にコントロールを追加する
 デザイン時にドキュメント レベルのプロジェクトの文書に Windows フォーム コントロールを追加する方法はいくつかあります。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-drag-a-windows-forms-control-to-the-document"></a>Windows フォーム コントロールをドキュメントにドラッグするには

1. Visual Studio で Excel ブック プロジェクトまたは Word 文書プロジェクトを作成するかまたは開き、ドキュメントがデザイナーに表示されるようにします。 プロジェクトの作成について詳しくは、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」をご覧ください。

2. **ツールボックス** の **[コモン コントロール]** タブで、追加するコントロールをクリックし、ドキュメントまでドラッグします。

    > [!NOTE]
    > Excel 内でコントロールを選択すると、 **数式バー** に  " **=EMBED("WinForms.Control.Host","")**" と表示されます。 このテキストは必要なので、削除しないでください。

### <a name="to-draw-a-windows-forms-control-on-the-document"></a>Windows フォーム コントロールをドキュメントに描画するには

1. Visual Studio で Excel ブック プロジェクトまたは Word 文書プロジェクトを作成するかまたは開き、ドキュメントがデザイナーに表示されるようにします。 プロジェクトの作成について詳しくは、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」をご覧ください。

2. **ツールボックス** の **[コモン コントロール]** タブで、追加するコントロールをクリックします。

3. ドキュメント上で、コントロールの左上隅となる位置をクリックし、コントロールの右下隅となる位置までドラッグします。

     指定したドキュメントの位置に、指定したサイズのコントロールが追加されます。

    > [!NOTE]
    > Excel 内でコントロールを選択すると、**数式バー** に **=EMBED("WinForms.Control.Host","")** と表示されます。 このテキストは必要なので、削除しないでください。

### <a name="to-add-a-windows-forms-control-to-the-document-by-single-clicking-the-control"></a>シングルクリックで Windows フォーム コントロールをドキュメントに追加するには

1. Visual Studio で Excel ブック プロジェクトまたは Word 文書プロジェクトを作成するかまたは開き、ドキュメントがデザイナーに表示されるようにします。 プロジェクトの作成について詳しくは、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」をご覧ください。

2. **ツールボックス** の **[コモン コントロール]** タブで、追加するコントロールをクリックします

3. ドキュメント上で、コントロールを追加する位置をクリックします。

     コントロールが既定のサイズでドキュメントに追加されます。

    > [!NOTE]
    > Excel 内でコントロールを選択すると、 **数式バー** に  " **=EMBED("WinForms.Control.Host","")**" と表示されます。 このテキストは必要なので、削除しないでください。

### <a name="to-add-a-windows-forms-control-to-the-document-by-double-clicking-the-control"></a>ダブルクリックで Windows フォーム コントロールをドキュメントに追加するには

1. Visual Studio で Excel ブック プロジェクトまたは Word 文書プロジェクトを作成するかまたは開き、ドキュメントがデザイナーに表示されるようにします。 プロジェクトの作成について詳しくは、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」をご覧ください。

2. **ツールボックス** の **[コモン コントロール]** タブで、追加するコントロールをダブルクリックします。

     コントロールは、ドキュメントまたはアクティブなペインの中央に追加されます。

    > [!NOTE]
    > Excel 内でコントロールを選択すると、 **数式バー** に  " **=EMBED("WinForms.Control.Host","")**" と表示されます。 このテキストは必要なので、削除しないでください。

### <a name="to-add-a-windows-forms-control-to-the-document-by-pressing-the-enter-key"></a>Enter キーを押して Windows フォーム コントロールをドキュメントに追加するには

1. Visual Studio で Excel ブック プロジェクトまたは Word 文書プロジェクトを作成するかまたは開き、ドキュメントがデザイナーに表示されるようにします。 プロジェクトの作成について詳しくは、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」をご覧ください。

2. **ツールボックス** の **[コモン コントロール]** タブで、追加するコントロールをクリックし、**Enter** キーを押します。

     コントロールは、ドキュメントまたはアクティブなペインの中央に追加されます。

    > [!NOTE]
    > Excel 内でコントロールを選択すると、 **数式バー** に  " **=EMBED("WinForms.Control.Host","")**" と表示されます。 このテキストは必要なので、削除しないでください。

## <a name="add-controls-at-run-time-in-document-level-projects"></a><a name="runtimedoclevel"></a> ドキュメント レベルのプロジェクトで実行時にコントロールを追加する
 Windows フォーム コントロールは、実行時にプログラムを使用してドキュメントに追加できます。 Word では、`ThisDocument` クラスの <xref:Microsoft.Office.Tools.Word.DocumentBase.Controls%2A> プロパティのメソッドを使用します。 Excel では、`Sheet`*n* クラスの <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Controls%2A> プロパティのメソッドを使用します。 各メソッドにはいくつかのオーバーロードがあり、それらを使用してさまざまな方法でコントロールの場所を指定できます。

 実行時にドキュメントに Windows フォーム コントロールを追加した場合、ドキュメントが閉じられると、コントロールはドキュメント内に保持されません。 次にドキュメントを開くときに、コントロールを再作成できます。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

### <a name="to-add-a-windows-forms-control-at-run-time"></a>実行時に Windows フォーム コントロールを追加するには

1. 名前が Add\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A> などの追加する Windows フォーム コントロールのクラス名) のメソッドを使用します。

     次のコード例は、Excel のドキュメント レベルのプロジェクトで、`Sheet1` のセル **C5** に <xref:Microsoft.Office.Tools.Excel.Controls.Button> を追加する方法を示したものです。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet4":::

## <a name="add-controls-at-run-time-in-vsto-add-ins"></a><a name="runtimeaddin"></a> VSTO アドインで実行時にコントロールを追加する
 Windows フォーム コントロールは、実行時にプログラムを使用して任意の開いているドキュメントに追加できます。 まず、開いているドキュメントかワークシートに基づいたホスト項目を生成します。 次に、Word では、新しいホスト項目の <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> プロパティのメソッドを使用します。 Excel では、新しいホスト項目の <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> プロパティのメソッドを使用します。 各メソッドにはいくつかのオーバーロードがあり、それらを使用してさまざまな方法でコントロールの場所を指定できます。

 実行時にドキュメントに Windows フォーム コントロールを追加した場合、ドキュメントが閉じられると、コントロールはドキュメント内に保持されません。 次にドキュメントを開くときに、コントロールを再作成できます。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

 VSTO アドイン プロジェクトでのホスト項目の生成について詳しくは、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」をご覧ください。

### <a name="to-add-a-windows-forms-control-at-run-time"></a>実行時に Windows フォーム コントロールを追加するには

1. 名前が Add\<*control class*> (*control class* は、<xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A> などの追加する Windows フォーム コントロールのクラス名) のメソッドを使用します。

    > [!NOTE]
    > [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする VSTO アドイン プロジェクトでは、*Microsoft.Office.Tools.Excel.v4.0.Utilities.dll* または *Microsoft.Office.Tools.Word.v4.0.Utilities.dll* アセンブリへの参照を先に追加する必要があります。Add\<*control class*> メソッドへのアクセスは、その後で可能になります。

     次のコード例で、Word VSTO アドインを使用して作業中のドキュメントの最初の段落に <xref:Microsoft.Office.Tools.Word.Controls.Button> を追加する方法を示します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet7":::

## <a name="see-also"></a>関連項目
- [Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [方法: ワークシートのセル内のコントロールをサイズ変更する](../vsto/how-to-resize-controls-within-worksheet-cells.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
